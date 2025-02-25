# Evaluating Mathematical Reasoning Abilities in Large Language Models

## Overview
This project investigates various approaches to enhancing mathematical reasoning in Large Language Models (LLMs). We explore techniques such as fine-tuning, N-shot prompting, and a novel multi-agent framework. The study evaluates the performance of multiple models on the **GSM8K** dataset, a benchmark designed to test the ability of LLMs to solve grade-school-level math problems.

## Models Evaluated
We experimented with the following open-source LLMs:
- **Llama-3.2-3B-Instruct**
- **Llama-3.1-8B-Instruct**
- **Mistral-7B-Instruct-v0.2**
- **Gemma-2-9B-IT**

These models vary in scale and architecture, enabling a comparative analysis of their reasoning performance across different prompting and fine-tuning strategies.

---

## Methodology
### 1. Base Model (Zero-shot Evaluation)
- The model is evaluated directly on the test set without explicit **Chain of Thought (CoT)** prompting.
- Establishes a baseline for inherent reasoning capabilities.

### 2. Fine-tuning + COT
- The models were fine-tuned on **GSM8K** and then tested with **Chain-of-Thought** prompting.
- Fine-tuning parameters used:
  - **Batch size**: 8
  - **Gradient accumulation steps**: 4
  - **Epochs**: 3
  - **Max sequence length**: 512

### 3. N-shot Prompting + COT
- The models were provided with **8-shot** examples before solving a math problem.
- This technique helps smaller models improve performance using in-context learning.

### 4. Multi-Agent Framework
- A novel approach where two LLMs are assigned distinct tasks:
  1. **Problem formulation**: One LLM converts a problem into mathematical equations.
  2. **Computation & Solution**: Another LLM performs reasoning based on the equations.
  3. **Evaluation**: GPT-4o assesses the correctness of the answer and reasoning.

---

## Results

### **1. Zero-Shot Performance**
| Model | Correct Answer | Correct Reasoning |
|--------|----------------|------------------|
| Gemma-2-9B-IT | 88.63% | 87.49% |
| Llama-3.1-8B | 78.60% | 77.74% |
| Mistral-7B | 46.85% | 46.93% |
| Llama-3.2-3B | 75.59% | 73.54% |

### **2. Fine-Tuning Performance**
| Model | Accuracy |
|--------|-----------|
| Gemma-2-9B-IT | 43.37% |
| Llama-3.1-8B | 33.25% |
| Mistral-7B | 38.30% |
| Llama-3.2-3B | 9.00% |

### **3. N-shot Prompting Performance**
| Model | Accuracy (8-shot) |
|--------|-----------|
| Gemma-2-9B-IT | 86.8% |
| Llama-3.1-8B | 81.2% |
| Mistral-7B | 42.9% |
| Llama-3.2-3B | 70.1% |

### **4. Multi-Agent Framework Performance**
| Model Pair | Accuracy | Joint (Correct Reasoning & Answer) | Answer Only | Reasoning Only | Incorrect |
|------------|---------|-----------------------------|-------------|----------------|------------|
| Gemma + Llama 3.1 | 55.28% | 49.95% | 5.30% | 8.74% | 35.98% |
| Gemma + Mistral v2 | 51.01% | 48.06% | 2.95% | 13.28% | 35.70% |
| Gemma + Llama 3.2 | 33.85% | 32.30% | 1.55% | 25.98% | 40.17% |

---

## Observations
- **Zero-shot performance** was unexpectedly high, surpassing fine-tuned models in some cases.
- **Fine-tuning led to worse performance**, likely due to formatting and parsing issues.
- **8-shot prompting showed moderate improvement**, with Llama-3.1-8B benefiting the most.
- **Multi-Agent Framework provided mixed results**, with improvements in reasoning but not always in final answer accuracy.

## Challenges
- **Computational Limitations**: Training large models required high-performance GPUs.
- **Fine-tuning Issues**: Formatting inconsistencies impacted model evaluation.
- **Lengthy Prompts in N-shot**: Some models struggled with longer context windows.

## Future Work
- Further fine-tuning experiments with better parsing strategies.
- Exploring **Gemma-Gemma** model combinations in the multi-agent framework.
- **Human evaluation** of responses to complement GPT-4o's automated assessment.

---

## License
This project is licensed under the **MIT License**.

