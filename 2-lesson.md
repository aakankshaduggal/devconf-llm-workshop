---
title: Guide
nav: true
---

# Workshop Guide

Now that you've deployed the RAG application, it's time to try out an application on your own.
You will deploy an audio-to-text application that utilizes whisper-cpp.


## Step 1: Navigate to the Audio to Text Application Directory

Navigate to the specific directory for the  application. This directory contains all the necessary code and resources for setting up the audio-to-text application.

`cd ai-lab-recipes/recipes/audio/audio_to_text/app`

## Step 2: Install Requirements

We will need to install all the packages, libraries and dependencies required to run the application. These are defined in the `requirements.txt` file.

Let's first start a Python virtual env and install the dependencies within this virtual env.

```python
python3 -m venv venv
source ./venv/bin/activate
```

Now, lets install all the packages:

`pip install -r requirements.txt`

## Step 3: Download Model

If you've already downloaded `granite-7b`, skip this step.

For this workshop, we recommend using the `granite-7b` lab model. It’s a well performing open sourced mid-sized model licensed under Apache-2.0 and served in the GGUF format.

Navigate to the models directory and download the recommended model as follows:

```python
cd ../../../../models 
curl -sLO https://huggingface.co/instructlab/granite-7b-lab-GGUF/resolve/main/granite-7b-lab-Q4_K_M.gguf
```

This step will take a couple of minutes. After downloading, you will see the model in your directory, ready to be used in the setup.


## Step 4: Start the Model Service

In order to deploy the model service, first, open a new terminal and navigate to the ai-labs-recipe repository that you have cloned.
The model service is responsible for processing and generating text based on inputs and retrieved documents. We will use the llamacpp_python model service for this. Navigate to the model service directory:

`cd ai-lab-recipes/model_servers/llamacpp_python`

Build the model service

```python
podman build -t llamacppserver -f ./base/Containerfile .
```

Deploy the model service

The `podman run` command  below requires you to substitute the absolute path to the models folder for `<PATH>`. To find the value for `<PATH>`, run

```bash
cd ../../ # you should now be in the ai-lab-recipes directory
pwd # copy this output to paste into the command below
```


```python
podman run --rm -it \
        -p 8001:8001 \
        -v <PATH>/models:/ai-lab-recipes/models:ro,Z \
        -e MODEL_PATH=/ai-lab-recipes/models/granite-7b-lab-Q4_K_M.gguf \
        -e HOST=0.0.0.0 \
        -e PORT=8001 \
        llamacppserver

```

## Step 5: Build the Audio to Text Application

Now that the Model Service is running we'll build and deploy our AI Application. Use the provided Containerfile to build the AI Application
image from the [`audio-to-text/`](./) directory.


```bash
# from path recipes/audio/audio_to_text from repo containers/ai-lab-recipes
podman build -t audio-to-text app
```

### Step 6: Deploy the AI Application

Make sure the Model Service is up and running before starting this container image.
When starting the AI Application container image we need to direct it to the correct `MODEL_ENDPOINT`.
This could be any appropriately hosted Model Service (running locally or in the cloud) using a compatible API.
The following Podman command can be used to run your AI Application:


```bash
podman run --rm -it -p 8501:8501 -e MODEL_ENDPOINT=http://10.88.0.1:8001/inference audio-to-text
```

### Interact with the AI Application

Once the streamlit application is up and running, you should be able to access it at `http://localhost:8501`.
From here, you can upload audio files from your local machine and translate the audio files as shown below.

By using this recipe and getting this starting point established,
users should now have an easier time customizing and building their own AI enabled applications.

#### Input audio files

Whisper.cpp requires as an input 16-bit WAV audio files.
To convert your input audio files to 16-bit WAV format you can use `ffmpeg` like this:

```bash
ffmpeg -i <input.mp3> -ar 16000 -ac 1 -c:a pcm_s16le <output.wav>
```

#### Congrats!! You have now successfully setup a LLM application locally on your laptop using containerization techniques 🥳
#### Give yourself a pat on the back!! 👏









