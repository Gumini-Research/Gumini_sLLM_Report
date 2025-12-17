# 🐻 Gumini 1B - 1.5B Open Source Release
---
<h3 align="center">🤗 Hugging Face Models</h3>

<p align="center">
  <a href="https://huggingface.co/GuminiResearch/Gumini-1.5B-Base" target="_blank">
    <img src="https://img.shields.io/badge/Gumini--1.5B--Base-HuggingFace-yellow?logo=huggingface&logoColor=black" style="margin-right:8px;" />
  </a>
  <a href="https://huggingface.co/GuminiResearch/Gumini-1B-Base" target="_blank">
    <img src="https://img.shields.io/badge/Gumini--1B--Base-HuggingFace-yellow?logo=huggingface&logoColor=black" />
  </a>
</p>
<p align="center">
  <img src="https://img.shields.io/badge/Parameters-1.54B-blue" alt="Parameters">
  <img src="https://img.shields.io/badge/Training%20Tokens-3.14B-green" alt="Training Tokens">
</p>
<p align="center">
  <a href="https://linkedin.com/in/devgumin" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-Gumin%20Kwon-0A66C2?logo=linkedin&logoColor=white" style="display:inline-block; margin-right:6px;" />
  </a>

  <a href="https://x.com/Gumini_Research" target="_blank">
    <img src="https://img.shields.io/badge/X-@Gumini__Research-black?logo=x&logoColor=white" style="display:inline-block; margin-right:6px;" />
  </a>

  <a href="https://www.instagram.com/gumini_research/" target="_blank">
    <img src="https://img.shields.io/badge/Instagram-gumini__research-E4405F?logo=instagram&logoColor=white" style="display:inline-block;" />
  </a>
</p>

> **5,700× less data, better performance.**  
> Gumini-1.5B achieves Korean PPL 8.49 with only 3.14B tokens, outperforming Qwen-1.5B (18T tokens, PPL 8.84).

## 🔥 Key Results

| Model | Params | Training Tokens | Korean PPL ↓ | Rank |
|-------|--------|-----------------|--------------|------|
| Qwen-2.5-7B | 7.62B | 18T | 6.39 | #1 |
| Gemma-2B | 2.0B | 2T | 8.15 | #2 |
| **Gumini-1.5B (Ours)** | **1.54B** | **3.14B** | **8.49** | **#3** |
| Qwen-2.5-1.5B | 1.5B | 18T | 8.84 | #4 |
| Llama-3.2-3B | 3.21B | 9T | 9.47 | #5 |
| EXAONE-3.5-2.4B | 2.4B | ~6.5T | 9.80 | #6 |

## 📊 Data Efficiency

| vs Model | Their Tokens | Gumini Tokens | Efficiency |
|----------|--------------|---------------|------------|
| Qwen-2.5 | 18T | 3.14B | **5,732×** less |
| Llama-3.2 | 9T | 3.14B | **2,866×** less |
| EXAONE-3.5 | ~6.5T | 3.14B | **~2,070×** less |

## 🏗️ Model Architecture

| | Gumini-1.5B | Gumini-1B |
|---|-------------|-----------|
| Parameters | 1.54B | 1.08B |
| Layers | 16 | 10 |
| Hidden Dim | 2048 | 2048 |
| Attention Heads | 16 | 16 |
| Vocab Size | 151,936 | 151,936 |
| Training Tokens | 3.14B | 393M |

## 🎓 Training Method: Inheritune

We use **progressive layer growth** with **knowledge distillation**:

```
Stage 0: 10 layers → Stage 6: 16 layers
Teacher: Qwen-2.5-3B
Total: 3.14B tokens across 7 stages
```

| Stage | Layers | Tokens | Cumulative |
|-------|--------|--------|------------|
| 0 | 10 | 393M | 393M |
| 1 | 11 | 393M | 786M |
| 2 | 12 | 393M | 1.18B |
| 3 | 13 | 393M | 1.57B |
| 4 | 14 | 393M | 1.97B |
| 5 | 15 | 393M | 2.36B |
| 6 | 16 | 786M | **3.14B** |

## 📈 Evaluation

### Datasets

| Dataset | Type | Description |
|---------|------|-------------|
| **KoBEST BoolQ** | Standard | Korean Boolean QA benchmark (test split) |
| **Wikipedia KO** | Held-out | Latest Korean Wikipedia dump |

### Metrics

- **Perplexity (PPL)**: Lower is better. Measures how well the model predicts text.
- **Top-k Accuracy**: Percentage of correctly predicted next tokens.

## 🚀 Quick Start

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model = AutoModelForCausalLM.from_pretrained("GuminiResearch/Gumini-1.5B-Base")
tokenizer = AutoTokenizer.from_pretrained("GuminiResearch/Gumini-1.5B-Base")

text = "<|im_start|>user\n너는 누구야?<|im_end|>\n<|im_start|>assistant\n"
inputs = tokenizer(text, return_tensors="pt")
outputs = model.generate(**inputs, max_new_tokens=50)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

## 📦 Models

| Model | HuggingFace |
|-------|-------------|
| Gumini-1.5B-Base | [GuminiResearch/Gumini-1.5B-Base](https://huggingface.co/GuminiResearch/Gumini-1.5B-Base) |
| Gumini-1B-Base | [GuminiResearch/Gumini-1B-Base](https://huggingface.co/GuminiResearch/Gumini-1B-Base) |
| Gumini-1.5B-Base-i1-GGUF | [GuminiResearch/Gumini-1.5B-Base-i1-GGUF](https://huggingface.co/GuminiResearch/Gumini-1.5B-Base-i1-GGUF) |
| Gumini-1B-Base-i1-GGUF | [GuminiResearch/Gumini-1B-Base-i1-GGUF](https://huggingface.co/GuminiResearch/Gumini-1B-Base-i1-GGUF) |

## 📄 Citation

```bibtex
@misc{gumini2025,
  title={Gumini-1.5B: Bilingual Korean-English Language Model via Inheritune},
  author={Gumin Kwon},
  year={2025},
  note={Built with Qwen. Trained with Inheritune progressive layer growing.},
  url={https://huggingface.co/GuminiResearch/Gumini-1.5B-Base}
}
```
