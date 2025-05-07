---
title: "How to use Hugging Face API"
date: 2025-02-17
categories: 
  - "artificialintelligence"
tags: 
  - "hugging-face"
  - "image-recognition"
  - "llm"
coverImage: "1KD729-z4Up6D_7waUXfGpg.png"
---

## Getting started to join the Hugging Face community[](https://medium.com/@researchgraph?source=post_page---byline--2942ea9da32a--------------------------------)

<figure>

![](images/1KD729-z4Up6D_7waUXfGpg.png)

<figcaption>

Created using DALLE on July 18, 2024

</figcaption>

</figure>

# Introduction

The Hugging Face Hub is a collaborative open-source platform that hosts a vast array of models, datasets, and demos for the machine learning community. With its diverse range of accessible models, it caters to various daily work needs. This article will introduce step-by-step instructions on how to use the Hugging Face API and utilise models from the platform in your own applications.

# Hugging Face API Tutorial

To use models from the Hugging Face platform in a local application or service with Hugging Face API, users can perform complex natural language processing tasks without needing to delve into the details of model implementation or large-scale dataset training processes. Here, we will give an image-to-text model from Hugging Face Hub as an example to show you how to use it with Hugging Face API.

## Step 1: Get your API Token

To get started, register or log in to your Hugging Face account first. Next, go to the settings page and click **Access Tokens**. Next, click **Create New Token**.

<figure>

![](images/1*dRIeDAZ08YoAKce7M546Tw.png)

<figcaption>

Hugging Face account settings — create your Access Tokens

</figcaption>

</figure>

Choose the token type you need. In this example, you can choose read-only access because it is sufficient to open pull requests. Then type your token name in the blank space. Here, we type “image-to-text” as our token’s name since we will use an image-to-text model in this example later.

<figure>

![](images/1qTyN2XPa21ZjWx4lbT57RQ.png)

<figcaption>

Select and name your new Access Token

</figcaption>

</figure>

After the token is created, don’t forget to copy your API token and save it to a safe place. You won’t be able to access it again after you click **done**.

<figure>

![](images/1c6vLS0F98XN75yzraxQV2g.png)

<figcaption>

Copy and save your Access Token

</figcaption>

</figure>

You can find the created token here.

<figure>

![](images/1KC6FrEVa2Il7Xq6itwznmw.png)

<figcaption>

Access Tokens example — an image-to-text token

</figcaption>

</figure>

## Step 2: Choose a model you like

Go to the main page of Hugging Face, then click **Models**.

<figure>

![](images/19hpmWCrvrtjTk2FgmWnrug.png)

<figcaption>

Hugging Face homepage — select the Models section

</figcaption>

</figure>

On the next page, there are thousands of different models you can use. You can sort the models based on the function you need on the left side. You also can type the names of models to search for them.

<figure>

![](images/1dj0La5VmlcxzHtQ9E0-hmA.png)

<figcaption>

Find a model you like — sorting and search options on the left side

</figcaption>

</figure>

Here, we use an image-to-text model called “blip-image-captioning-base” as an example. This AI model can describe the content of the image you provide. You can also use other models you like.

<figure>

![](images/1*xRCSTK2AIidnevhkqKI53w.png)

<figcaption>

Image-to-text model example — BLIP image captioning base

</figcaption>

</figure>

## Step 3: Run the model in your application.

Using this model in your own app is quite easy. Here, we need to set up the API in your code. On Hugging Face, the model will provide the direct code to use it. First, you need to click **Deploy** on this page then click **Inference API (serverless)**.

<figure>

![](images/1Lqcx3Bwuu4Ll90RlQhpvqA.png)

<figcaption>

Select ‘Inference API (serverless)’ from the ‘Deploy’ dropdown box

</figcaption>

</figure>

In the next window, you can choose any programming language you like. In this example, we choose Python as an example.

<figure>

![](images/13dPf9RwhxlZK7TBXdudx0A.png)

<figcaption>

Using Python as an example — choose a programming language and copy it

</figcaption>

</figure>

Here is the code we use. You need to replace the “hf\_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx” token with yours. Then, you can insert this code into your own program.

```
import requests

API_URL = "https://api-inference.huggingface.co/models/Salesforce/blip-image-captioning-base"headers = {"Authorization": "Bearer hf_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"}def query(filename):    with open(filename, "rb") as f:
        data = f.read()
    response = requests.post(API_URL, headers=headers, data=data)
    return response.json()

output = query("yourphoto.jpg")
print(output)
```

In this example, we used this cat photo as our input.

<figure>

![](images/18yeESHg2Gfsls8-DzNUuvA.jpg)

<figcaption>

A cat photo as input (downloaded from Pexels on 17 Jul 2024)

</figcaption>

</figure>

Then run the code using the command below and get the result from our Hugging Face model. Don’t forget to change “app” to your file name. The result says “a cat sitting on a couch looking at the camera”, which is an accurate and good description.

```
py app.py
```

<figure>

![](images/1CZJAMyFnZEbWKrTOFWUbVQ.png)

<figcaption>

The result generated by this image-to-text model

</figcaption>

</figure>

Of course, we can enhance the input for our model by incorporating a UI, making it more visually appealing and user-friendly. However, the primary goal of this article is to share how to use the Hugging Face API, so we will not delve further into this topic.

# Conclusion

The Hugging Face API offers a powerful and efficient tool, enabling us to integrate thousands of pre-trained, mature models into our own software applications. This article provides a detailed guide on how to use the API, aiming to enhance the productivity of our user community. However, since anyone or any institution can upload their models to the platform, it is important to be mindful of the quality and accuracy of the models you choose, as they might impact your results.

# References

- _Technical Support Documentation for Hugging Face — Get Started._ [Read me](https://huggingface.co/docs/api-inference/en/quicktour#overview).
