---
title: Deploying a Dash App to Huggingface
date: 2024-01-09 07:00:00 -0000 # Note the offset of -0000 is optional
categories: [project, data visualisation]
tags: [plotly, dash]  # TAG names should always be in lowercase
---

# Introduction
This post covers the steps to host a Dash App on Huggingface using Docker.

## What is HuggingFace?

Huggingface is a Machine Learning and Data Science platform and community that enables users to build and deploy applications.

## Why Deploy to Huggingface?
Huggingface provides free hosting using docker to enable apps to be demonstrated to others.

## Steps to Deploy a Dash App in Huggingface

## Create a New Space

Once you have created your Huggingface account,  you will create a new Space using Docker as per the image below. Give your Space a name, select Docker, use a blank Docker template and click Create Space.

[//]: # "Need to update impage alt text and caption."
![Create new Space page](/post_images/2024-01-09-Deploy-Dash-Huggingface/DashDocker.PNG "Create new Huggingface Space with Docker")

### Clone the Huggingface Repository

Once you have created your space you will be given the details to clone the Huggingface GIT repository. I clones the repository to my local drive and used VSCode to to create files, commit and sync.
![Clone Repository](/post_images/2024-01-09-Deploy-Dash-Huggingface/DashDocker2.PNG "Clone repository and Dockerfile details")

### Create the Docker file.
In your cloned Huggingface repository create a file called Docker (no extension) and copy the sample provided (as per the image above).
```docker
# read the doc: https://huggingface.co/docs/hub/spaces-sdks-docker
# you will also find guides on how best to write your Dockerfile

FROM python:3.9

WORKDIR /code

COPY ./requirements.txt /code/requirements.txt

RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

COPY . .

# Change the Docer command to run the app.py
CMD ["python", "app.py", "--host", "0.0.0.0", "--port", "7860"]
```
Note that the CMD code has been altered to run a python file named app.py

### Create app.py
For simplicity I created a file called app.py in my cloned Huggingface Repository using the simple callback example from the [Dash tutorial](https://dash.plotly.com/basic-callbacks) site.

```python
from dash import Dash, dcc, html, Input, Output, callback

app = Dash(__name__)

app.layout = html.Div([
    #Heading
    html.H1("Change the value in the text box to see callbacks in action!"),
    # Input Section
    html.Div([
        "Input: ",
        dcc.Input(id='my-input', value='test value', type='text')
    ]),
    # Section break
    html.Br(),
    #Output value
    html.Div(id='my-output'),

])


@callback(
    Output(component_id='my-output', component_property='children'),
    Input(component_id='my-input', component_property='value')
)
#this is the input function
def update_output_test(nomatter):
    return f'Output: {nomatter}'


if __name__ == '__main__':
    #Update host and port to match dockerfile
    app.run(debug=True, host='0.0.0.0', port=7860)
```
Note the app.run code has been updated to include the host and port to match the Dockerfile.

### Create requirements.txt
In your cloned Huggingface repository create a requirements.txt file with the following:
```text
dash
```

### Commit and Sync
In VScode just add a Commit message, Commit the change and sync the repository. Once Huggingface has built the app you will be able to interact.

## Conclusion
The running app can be found here in my  [Huggingface Space](ttps://huggingface.co/spaces/iFiveZero/SimpleDashApp).
