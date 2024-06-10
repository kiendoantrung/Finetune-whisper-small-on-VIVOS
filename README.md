# Introduction

Whisper is a general-purpose speech recognition model developed by OpenAI. It is designed to handle a variety of tasks including multilingual speech recognition, speech translation, and language identification. This repository contains the fine-tuned version of the Whisper Small model, optimized for specific speech recognition tasks.

# Model Overview

Dataset_tags: "AILAB-VNUHCM/vivos"

Dataset: "VIVOS",

Language: "vi",

Model_name: "kiendt/whisper-small-vivos",

Finetuned_from: "openai/whisper-small",

Tasks: "automatic-speech-recognition",

Word Error Rate (WER): 16.3818 after 5,000 training steps

# Setup

```bash
pip install --upgrade --quiet datasets[audio] transformers accelerate evaluate jiwer tensorboard gradio
```

# Usage

Use from the Transformers library:

```bash
from transformers import pipeline

pipe = pipeline("automatic-speech-recognition", model="kiendt/whisper-small-vivos")
```

Inference on Gradio:

```bash
from transformers import pipeline
import gradio as gr

pipe = pipeline(model="kiendt/whisper-small-vivos")

def transcribe(audio):
    text = pipe(audio)["text"]
    return text

iface = gr.Interface(
    fn=transcribe,
    inputs=gr.Audio(type="filepath"),
    outputs="text",
    title="Whisper Small Vietnamese",
    description="Realtime demo for Vietnamese speech recognition using a fine-tuned Whisper small model.",
)

iface.launch()
```
