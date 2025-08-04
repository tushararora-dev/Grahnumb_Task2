```
1. Generate and Prepare Dataset

Option 1: ISO Format Dataset
Name: Grahnumb_Task2/ISO_Format_Dataset.jsonl

{
  "instruction": "Extract exact datetime from this expression assuming today is 2025-08-04.",
  "input": "show it on 26th April at 10",
  "output": {
    "start": "2025-04-26T10:00:00+05:30",
    "end": null
  }
}

Option 2: Verbose Structured Output
Name: Grahnumb_Task2/Verbose_Structured_Output.json

{
  "instruction": "Extract temporal information and return JSON with exact datetime.",
  "input": "yesterday at 14:30",
  "output": {
    "type": "single_time",
    "date": "2025-08-03",
    "time": "14:30",
    "approximate": false
  }
}

Final: Use Option 1 for your current LLaMA finetuning task — it’s more compact and generalizable.

Format           Description                                Best Use Case
.json            Standard JSON file with entire dataset     Human-readable, small datasets
                 as a list

.jsonl           JSON Lines: 1 JSON object per line         Streaming, large datasets, LLMs


2. Selection Model

I need to use LLaMA 3.2, but it's a gated repository and requires 24 hours to get access.
So, I’m exploring other options like:

Resource                        Best Choice
--------------------------------------------------------------
Kaggle Notebook (T4 GPU, 16GB)  microsoft/phi-2 or TinyLlama
Instruction Fine-Tuning         Nous Hermes 2 or Mistral-7B
Quick Experiments               TinyLlama or Gemma-2B
Accurate JSON Generation        Mistral-7B (best token consistency)

Final: I try with Mistral 7b and Llama2 7b


3. Framework for Finetuning

Tool              Best For                              Code Complexity
-----------------------------------------------------------------------------
Axolotl           Quick YAML-based LoRA tuning          Low
HuggingFace + PEFT Full control & production setup      Medium
QLoRA + TRL       Huge datasets + memory efficiency      High
LLaMA-Factory     Large-scale, OpenChat-style models     Medium
FastChat          Building ChatBots / APIs               High

Final: I used HuggingFace + PEFT


4. Steps for Finetuning

1. Load Model and Tokenizer
2. Padding Token Fix (often needed for Mistral)
3. Dataset Formatting
4. Tokenization
5. LoRA Configuration
6. Apply LoRA to Model
7. Define Training Arguments
8. Trainer Setup
9. Start Training
10. Save Model

Upload to Hugging Face:
https://huggingface.co/tusharoclock/finetunellm
```
