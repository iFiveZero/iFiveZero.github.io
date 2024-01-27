---
title: Deploying an EmbedChain App to Huggingface
date: 2024-01-22 07:00:00 -0000 # Note the offset of -0000 is optional
categories: [project, LLM]
tags: [embedchain, gradio, huggingface]  # TAG names should always be in lowercase
---

# Deploy EmbedChain App to Huggingface using Gradio

Embedchain streamlines deploying RAG apps with support for both conventional and configurable approaches. This OpenSource Framework offers a seamless process for managing various types of unstructured data. Embedchain segments data into manageable chunks, generates embeddings and stores n a vector database for optimised retrieval.

Embedchain provides a Quickstart app which is used in this article. [[insert link]]. We will use the free Huggingface LLM with Sentence Transformers as the Open source embeddings model.

Gradio is an OpenSource Python package that enables machine learning models to be quickly and easily built and shared using built-in features. 

The local environment for this project is Windows 10 with WSL.

## Preparing the Environment
This project used an anaconda environment, to create and activate the conda environment run the following:

```bash
conda create --name <my-env>
conda activate <my-env>
```
Install the dependencies:

```bash
conda install conda-forge::gradio
pip install embedchain sentence_transformers
```

## Create a Hugginface Access Key

To access the Mistral model from your code you will need a Huggingface Access Token. Click on your profile at the top right and select Settings and Access Tokens. Create a New token and give the token a name. In this example the Access Token is named "EmbedChain".

## Creating the Huggingface Space

Create a Hugginface space with Gradio. Give the Space a name, select a license and select Gradio as the Space SDK.

## Managing Secrets with Space Variables

We will set the Huggingface Access key as an environment Secret to avoid hard coding the key into our code. Click on the space settings and scroll down to Variables and Secrets and select a New Secret. We have called this secret "EmbedChain" and paste in the Access Token created earlier.

## Cloning the Environment Locally

Click on the Space and select the 3 dots on the right and select Clone Repository. Follow the instructions and install lfs and clone the repository.

## Create A Windows Environment Variable

To replicate the Space environment Secret we will create a Windows Environment Variable with the same name as used in the Space. This enables the app to be run locally and then uploaded via Git into the Space without modification.

From the Windows search bar enter "Control Panel" and then in the top right of the Control Panel search variable and click on "Edit environment variables for your account.

Select "New" and enter the name "EmbedChain" and paste in the Huggingface Access Token as the Value. 

Save the value and reboot your PC.

## Create App

Embedchain provides a feature to create a Gradio app, but it is just as easy to create the app in a python script as follows:

```python
import os
import gradio as gr

from embedchain import App

os.environ["HUGGINGFACE_ACCESS_TOKEN"] = os.environ.get("EmbedChain")

app = App.from_config("mistral.yaml")
app.add("https://www.forbes.com/profile/elon-musk")
app.add("https://en.wikipedia.org/wiki/Elon_Musk")

def query(message, history):
    return app.chat(message)

demo = gr.ChatInterface(query, title="Embed Chain Quickstart App Implemented with Gradio")

demo.launch()
```

## Create json file

```json
{
    "provider": "gradio.app"
}
```

## Create yaml
This example uses the free Huggingface Mistral model.

```yaml
llm:
  provider: huggingface
  config:
    model: 'mistralai/Mistral-7B-v0.1'
    top_p: 0.5
embedder:
  provider: huggingface
  config:
    model: 'sentence-transformers/all-mpnet-base-v2'
```

## Create requirements.txt

List the pre-requisites required to run the app on Huggingface.

```text
gradio==4.11.0
embedchain
sentence_transformers

```

## The Importance of Gitignore

If you run the app locally a vector database will be created which needs to be excluded from the git sync. If the file is included Huggingface will reject the sync due to an executable being uploaded.

```text
/db
*sqlite3
```

## Running Locally
To run the app locally:

```bash
python app.py
```

## Running on Huggingface
Commit and sync the changes to Huggingface using VScode.
