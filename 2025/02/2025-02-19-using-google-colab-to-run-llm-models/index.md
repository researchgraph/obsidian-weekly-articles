---
title: "Using Google Colab to run LLM Models"
date: 2025-02-19
categories: 
  - "artificialintelligence"
tags: 
  - "generative-ai-tools"
  - "google-colab"
  - "gpu"
  - "large-language-models"
coverImage: "0H4QME3upnxIJxnBm.jpg"
---

## A step-by-step tutorial[](https://medium.com/@researchgraph?source=post_page---byline--8c308cac6efa--------------------------------)

<figure>

![](images/0H4QME3upnxIJxnBm.jpg)

<figcaption>

Created by using Pixlr

</figcaption>

</figure>

In the field of Artificial Intelligence, large language models (LLMs) are transforming the landscape of what machines can achieve. These sophisticated models excel at tasks like summarising text, generating human-like content, translating languages, and answering complex questions. However, the computational resources required to run such models can be prohibitive for many individuals and small teams. Let’s enter the world of Google Colab. Colab is a Python platform by Google. It provides a game-changing solution by offering a free cloud-based environment that supports Python code execution. This allows you to leverage powerful hardware, including GPUs, without the financial burden of expensive infrastructure. We can run the LLM models on the free version of Google Colab using their free T4 GPU. Here’s how you can utilise Google Colab to run LLMs effectively.

# 1\. Introduction to Google Colab

Google Colab simplifies the execution of Python code in your browser with no setup required. It democratises access to advanced computational resources, making it feasible to run LLMs without hefty costs. Key features include:

- **Free GPU Access:** Boosts computational efficiency.

- **Google Drive Integration:** Easy access and saving of files.

- **User-Friendly Interface:** Simplifies complex workflows.

# 2\. Setting Up Your Environment

## 2.1 Creating a New Notebook

Start by opening Google Colab:

1. Visit [Google Colab](https://colab.google/).

3. Click “New Notebook” to create a new Python 3 environment.

## 2.2 Selecting GPU Runtime and Enabling GPU Acceleration

Ensure that you are using a GPU for enhanced performance:

Navigate to Runtime > Change runtime type. Select GPU under Hardware accelerator.

<figure>

![](images/0Izgox0b7Gx263uYj.png)

<figcaption>

Created from Google Colab Jupyter Notebook by Tohfa Siddika Barbhuiya

</figcaption>

</figure>

<figure>

![](images/0kZPZWcsvI5xupOtV.png)

<figcaption>

Created from Google Colab Jupyter Notebook by Tohfa Siddika Barbhuiya

</figcaption>

</figure>

Then click on Connect

## 2.3 Installing Required Libraries

For LLMs, you’ll need libraries like `transformers`. Install it using the following code:

```
# install dependencies
!pip install transformers
!pip install einops
!pip install accelerate
```

# 3\. Mounting Google Drive (if the user wants to)

Google Drive integration allows easy data management. Here’s how to mount your drive:

```
from google.colab import drive
drive.mount('/content/drive')
```

Follow the instructions:

Click on the link that appears. Choose your Google account. Copy the authorisation code provided. Paste the authorisation code back into Colab:

After pasting the code, your Google Drive will be mounted. You can now access your Google Drive files directly from your Colab notebook.

# 4\. Running Large Language Models

Now, let’s run a large language model using Hugging Face’s transformers library. For this demonstration, the Open Source LLM Modle Falcon-7b-Instruct Model (TII) is used. Here is a basic example for sentiment analysis:

```
from transformers import AutoTokenizer, AutoModelForCausalLM
import transformers
import torch

# load model
model = "tiiuae/falcon-7b-instruct"
tokenizer = AutoTokenizer.from_pretrained(model)falcon_pipeline = transformers.pipeline("text-generation",
                                        model=model,
                                        tokenizer=tokenizer,
                                        torch_dtype=torch.bfloat16,
                                        trust_remote_code=True,
                                        device_map="auto"
                                        )

# define completion function
def get_completion_falcon(input):
  # prompt = f"You are an expert Physicist. Your job is to explain complex Physics concepts in simple words. \n{input}"
  # print(prompt)
  system = f"""
  You are an expert Physicist.
  You are good at explaining Physics concepts in simple words.
  Help as much as you can.
  """
  prompt = f"#### System: {system}\n#### User: \n{input}\n\n#### Response from falcon-7b-instruct:"
  print(prompt)
  falcon_response = falcon_pipeline(prompt,
                                    max_length=500,
                                    do_sample=True,
                                    top_k=10,
                                    num_return_sequences=1,
                                    eos_token_id=tokenizer.eos_token_id,
                                    )

  return falcon_response

# let's prompt
prompt = "Explain to me the difference between nuclear fission and fusion."
# prompt = "Why is the Sky blue?"
response = get_completion_falcon(prompt)
print(response[0]['generated_text'])
```

You will get a surprising output. Check your notebook after running it.

```
print(response[0]['generated_text'])
```

Uncomment the next prompt and run. Again you will get a surprising output from the response. Also, you can connect to Ollama remotely through Google Colab as well.

# 6\. Conclusion

Google Colab provides a versatile and accessible platform for running large language models, removing the barriers of expensive hardware and complex setups. By offering free GPU access, seamless Google Drive integration, and a user-friendly interface, Colab empowers individuals and small teams to explore and utilise the capabilities of advanced AI models like Falcon-7B-Instruct, running Ollama remotely and running LLM Models. This democratisation of technology enables more people to engage in cutting-edge AI research and applications, making powerful computational tools available to a wider audience. Start using Google Colab today to unlock the potential of LLMs in your projects.

# References

- T. I. Institute, “Falcon-7B-Instruct,” Hugging Face, 2023. \[Online\]. Available: [https://huggingface.co/tiiuae/falcon-7b-instruct](https://huggingface.co/tiiuae/falcon-7b-instruct). \[Accessed: 31-July-2024\].
