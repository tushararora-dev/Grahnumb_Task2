````markdown
# Fine-Tuning LLM for Datetime Extraction (Approach Overview)

## 1. Generate and Prepare Dataset

### ✅ Option 1: ISO Format Dataset  
**File:** `Grahnumb_Task2/ISO_Format_Dataset.jsonl`

```json
{
  "instruction": "Extract exact datetime from this expression assuming today is 2025-08-04.",
  "input": "show it on 26th April at 10",
  "output": {
    "start": "2025-04-26T10:00:00+05:30",
    "end": null
  }
}
```

### 🔁 Option 2: Verbose Structured Output  
**File:** `Grahnumb_Task2/Verbose_Structured_Output.json`

```json
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
```

### 🔹 Final Choice:  
Use **Option 1** — it’s more compact and generalizable for your current LLaMA fine-tuning task.

### Dataset Format Guide

| Format   | Description                             | Best Use Case                        |
|----------|-----------------------------------------|--------------------------------------|
| `.json`  | Standard JSON file as a list            | Human-readable, small datasets       |
| `.jsonl` | JSON Lines (1 object per line)          | Streaming, large datasets, LLMs      |

---

## 2. Model Selection

| Resource                    | Best Choice                   |
|----------------------------|-------------------------------|
| Kaggle Notebook (T4, 16GB) | `microsoft/phi-2`, TinyLlama  |
| Instruction Fine-Tuning    | `Nous Hermes 2`, Mistral-7B   |
| Quick Experiments          | TinyLlama, Gemma-2B           |
| Accurate JSON Generation   | **Mistral-7B** (best consistency) |

### 🔹 Final Choice:  
Try with **Mistral 7B** and **LLaMA2 7B**

---

## 3. Framework for Finetuning

| Tool             | Best For                                | Code Complexity |
|------------------|------------------------------------------|------------------|
| Axolotl          | Quick YAML-based LoRA tuning             | Low              |
| HuggingFace + PEFT | Full control & production setup        | Medium           |
| QLoRA + TRL      | Huge datasets + memory efficiency        | High             |
| LLaMA-Factory    | Large-scale, OpenChat-style models       | Medium           |
| FastChat         | Building ChatBots / APIs                 | High             |

### 🔹 Final Choice:  
Used **Hugging Face + PEFT**

---

## 4. Finetuning Steps

1. Load Model and Tokenizer  
2. Fix Padding Token (especially for Mistral)  
3. Format Dataset  
4. Tokenization  
5. LoRA Configuration  
6. Apply LoRA to Model  
7. Define Training Arguments  
8. Trainer Setup  
9. Start Training  
10. Save Model  

---

## 📤 Model Upload

Upload your fine-tuned model to Hugging Face:

👉 [https://huggingface.co/tusharoclock/finetunellm](https://huggingface.co/tusharoclock/finetunellm)
