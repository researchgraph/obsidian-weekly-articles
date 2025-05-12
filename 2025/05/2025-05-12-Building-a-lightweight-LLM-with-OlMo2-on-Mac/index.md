# From Zero to Classifier: Building a Lightweight LLM with OLMo 2 on Your Laptop

Author: Yao Chen (ORCID:0009-0007-1385-3343)

## 1 Overview

OLMo 2 1B is a new generation of open source language model launched by the Allen Institute for AI, with a parameter scale of about 1 billion. It provides excellent natural language understanding and generation capabilities while maintaining a small size, and is suitable for a variety of downstream tasks.

In this post, we will complete process of installation, fine-tuning, and evaluating the `OLMo-2-0425-1B` model from AllenAI. We explore how to use LoRA (Low-Rank Adaptation) to fine-tune the model efficiently and evaluate its sentiment classification ability with a custom dataset, all running locally with MPS acceleration.

## 2 About the Model: OLMo-2-0425-1B

[`OLMo-2-0425-1B`](https://huggingface.co/allenai/OLMo-2-0425-1B) is a 1.1 billion parameter decoder-only language model released by [AllenAI](https://allenai.org/) on May 1,2025. As part of the OLMo series, it is trained from scratch using high-quality, open-source datasets with a strong emphasis on transparency, reproducibility, and research accessibility.

Key characteristics of the model include:

- **Architecture**: GPT-style causal decoder (transformer) model
- **Size**: 1.1B parameters — light enough to run inference and fine-tune on a local
  laptop
- **Tokenizer**: BPE (Byte-Pair Encoding) with a vocabulary of ~50k tokens
- **Training corpus**: Built from a curated mixture of open datasets, including deduplicated versions of books, web text, StackExchange, and academic papers

OLMo-2-0425-1B is not instruction-tuned or chat-optimized by default. Instead, it is designed as a **research-friendly base model**—ideal for experimenting with new downstream tasks such as classification, summarization, or dialogue systems. So it is  easily tested on local computer, we because:

- It’s small enough to fit on consumer hardware;
- It uses an open license and model weights are freely available;
- It is a strong candidate for parameter-efficient fine-tuning techniques like LoRA.

## 3 Environment Setup

- **Hardware**: MacBook Pro with Apple Silicon (M3, 36GB RAM)
- **Frameworks**: PyTorch, Hugging Face Transformers, Datasets, PEFT
- **Virtual Environment**:
  We strongly recommend that you create a new virtual environment to avoid the confliction between the required version of packges and your old veriosns in your environment.

```bash
conda create -n olmo-fresh python=3.10 -y
conda activate olmo-fresh
pip install torch torchvision torchaudio
pip install transformers datasets peft gradio
```

And if you keep meeting the problem like this

```python
RuntimeError: operator torchvision::nms does not exist
```

or

```python
OMP: Error #15: Initializing libomp.dylib, but found libomp.dylib already initialized.
```

It means you may manually install torch / torchvision from different sources or multiple libraries loaded different versions of the OpenMP (libomp) dynamic library, causing conflicts. We recomend you to uninstall torch/torchvision or create a new virtual environment this is the quickest way to solve these kind of problem.

---

## 4 Installation

OLMo 2 1B is supported in transformers v4.48 or higher:

```python
pip install transformers>=4.48
```

You can use OLMo with the standard HuggingFace transformers library:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
olmo = AutoModelForCausalLM.from_pretrained("allenai/OLMo-2-0425-1B")
tokenizer = AutoTokenizer.from_pretrained("allenai/OLMo-2-0425-1B")
message = ["Language modeling is "]
inputs = tokenizer(message, return_tensors='pt', return_token_type_ids=False)
# optional verifying cuda
# inputs = {k: v.to('cuda') for k,v in inputs.items()}
# olmo = olmo.to('cuda')
response = olmo.generate(**inputs, max_new_tokens=100, do_sample=True, top_k=50, top_p=0.95)
print(tokenizer.batch_decode(response, skip_special_tokens=True)[0])
```

After running the script above you will see the output like this:

```
Language modeling is**  **a type of language learning methodology that is concerned with acquiring linguistic competence without having the necessary raw input in the target language (L2).

** **2) Natural language processing (NLP) is the study of techniques for computers to process, understand, and manipulate human languages. Natural language processing is a broad discipline that also focuses on aspects of language acquisition.

** **3) Translation models is a type of software program used in translation to translate text from one language to another. The most popular translation model is statistical
```

## 5 Fine-Tuning OLMo-2-1B with LoRA

As we mentioned before OLMo-2-0425-1B is designed as a **research-friendly base model**, so we want to test a new task **Sentiment Classification** on OLMo-2-0425-1B. We want to classify the sentiment contained in a given sentence as positive or negative. Here is an example

Input sentence:

```
"I really hated the service at this restaurant."
```

Output:

```
Negative
```

Here is the source code :[Git repository](https://github.com/CHeN-Ya0/Olmo2_Sentiment-Classification.git)

### What is Fine-Tuning?

Fine-tuning is the process of adapting a pretrained language model to a specific downstream task—such as sentiment classification—by continuing its training on a smaller, task-specific dataset. Instead of training a model from scratch (which is computationally expensive and data-hungry), fine-tuning allows us to leverage the general linguistic knowledge already captured by large-scale pretrained models.

However, full fine-tuning of large language models (LLMs) like OLMo-2-1B can be resource-intensive, especially when running on consumer hardware.

### Why LoRA?

LoRA (Low-Rank Adaptation of Large Language Models) offers a solution to this challenge. It is a parameter-efficient fine-tuning technique that:

* **Freezes the original model weights** and inserts a small number of trainable** ****low-rank matrices** into key layers (e.g., query/key/value projections in attention).
* **Significantly reduces the number of trainable parameters**—often by 95% or more—while maintaining competitive performance.
* **Speeds up training** and **reduces memory usage**, making it ideal for laptops and edge devices.

In our case, LoRA allowed us to fine-tune OLMo 2 1B on a MacBook Pro using MPS acceleration without running out of memory.

### How LoRA Works

Here's a simplified visual of how LoRA operates within a transformer layer:

```
W (frozen)
        + A @ B  ← (trainable low-rank adapters)
        ---------
            ↓
       Modified Attention Output
```

Where:

- W is the original weight matrix (frozen)
- A and B are small trainable matrices with rank r (e.g., r=8)

### Dataset Construction

We use GPT-4o to generate a small synthetic sentiment classification dataset, for each sentence we give it a lable, here is the one example data in the dataset:

```json
{
  "text": "I absolutely loved the product.",
  "label": "positive"
}
```

- 100 positive examples
- 100 negative examples
- Split as `train.json`(160 data) and `val.json` (40 data)for training and validation.

---

### LoRA Fine-Tuning

We used PEFT to apply LoRA to the OLMo model and fine-tuned it on our sentiment dataset. Here is my full project path:

```bash
Olmo/
├── data/
│   ├── full.json          # full dataset
│   ├── train.json         # training subset
│   ├── val.json           # validation subset
├── train.py               # main LoRA fine-tuning script
├── infer.py               # inference script
├── test.py                # accuracy evaluation
├── train_loss_log.json    # training loss record (JSON)
├── split_data.py          # utility to split full.json
├── visualize.py           # loss plotting script
├── olmo-lora-adapter/     # saved LoRA adapter
├── checkpoints/           # chech point save dir
```

### Key Configurations:

```python
peft_config = LoraConfig(
    r=8,
    lora_alpha=16,
    task_type=TaskType.CAUSAL_LM,
    lora_dropout=0.1,
    bias="none",
    target_modules=["q_proj", "k_proj", "v_proj", "o_proj", "gate_proj", "up_proj", "down_proj"]
)
```

### TrainingArguments:

```python
training_args = TrainingArguments(
    output_dir="./checkpoints",
    per_device_train_batch_size=1,
    per_device_eval_batch_size=1,
    eval_strategy="epoch",
    save_strategy="epoch",
    num_train_epochs=10,
    learning_rate=2e-4,
    logging_steps=10,
    report_to="none",
    fp16=False
)
```

We also defined a `LossLoggerCallback` to track and save loss during training:

```json
[
  {"step": 10, "loss": 12.3},
  {"step": 20, "loss": 9.1},
  ...
]
```

Saved as `train_loss_log.json`. And here is the loss curve
![Train Loss](https://github.com/CHeN-Ya0/Images/blob/main/loss_curve.png?raw=true)

---

### Inference

We defined an `infer.py` script to evaluate single sentences:

```python
prompt = f"<|user|>\nClassify the sentiment of this sentence: \"{sentence}\"\n<|assistant|>\n"
inputs = tokenizer(prompt, return_tensors="pt").to(device)
outputs = model.generate(**inputs, max_new_tokens=5)
```

Predicted label is extracted from the generated output.Here is one example:
![Infer example](https://github.com/CHeN-Ya0/Images/blob/main/infer.png?raw=true)

---

### Evaluation

An evaluation script was used to compute classification accuracy on the `val.json`:

```python
correct = 0
for example in val_set:
    predicted = classify(example["text"])
    if predicted == example["label"]:
        correct += 1
accuracy = correct / len(val_set)
```

We find the accuracy is 1 and here is the confusion matrix:
![Train vs Val Loss](https://github.com/CHeN-Ya0/Images/blob/main/confusion_matrix_eval.png?raw=true)
The model was able to correctly classify a large portion of examples after just 10 epochs.

---

### Benefits Observed

* ✅ We were able to train the model for 10 epochs on a small dataset without GPU acceleration.
* ✅ Training time was under 15 minutes.
* ✅ The model quickly converged and achieved good accuracy on sentiment classification.
* ✅ Final model size remained compact, with only LoRA adapters saved.

---

## Conclusion

Through this experiment, we tested the real-world usability of **OLMo-2-0425-1B**, a 1.1B-parameter language model developed by AllenAI, in a local fine-tuning and inference setting. Rather than evaluating it solely as a pretrained base model, we explored how well it could adapt to a specific downstream task—sentiment classification—under resource-limited conditions.

Our results show that OLMo is a practical and flexible foundation model. With the help of parameter-efficient fine-tuning (LoRA), we were able to achieve reasonable performance using a custom dataset, all on a MacBook Pro without GPU. The model converged quickly, produced intelligible outputs, and showed a steady improvement in validation loss and classification accuracy over multiple epochs.

However, the testing also revealed some limitations. While OLMo handles structured prompts well, its output format can sometimes drift without proper formatting or prompt engineering. Additionally, compared to larger instruction-tuned models, it may require more task-specific guidance to maintain robustness in edge cases.

Overall, **OLMo-2-0425-1B** proved to be both efficient and adaptable, making it a strong candidate for researchers or developers looking to experiment with open models locally. Our testing confirms that even without cloud-scale hardware, OLMo can deliver meaningful results when paired with the right tools and training strategies.

