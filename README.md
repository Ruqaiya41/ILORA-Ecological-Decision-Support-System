# ILORA Ecological Decision Support System

An open-source AI toolkit for querying invasive alien species 
data using Retrieval-Augmented Generation (RAG) and 
[Llama 3.2 3B Instruct](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct) 
*(Llama 3.2 Community License)*.

Built on the ILORA database India's first comprehensive 
database of 1,747 alien vascular plant species.

---

## What This Project Does

Forest officers, researchers, and policymakers need quick, 
reliable answers about invasive species. General-purpose AI 
tools hallucinate. This system answers only from verified 
ILORA data and explicitly says so when data is unavailable.

---

## Notebooks

| Notebook | Description | Open in Colab |
|---|---|---|
| `ILORA_Notebook1_DataPipeline.ipynb` | 16 ILORA tables to 1,747 text chunks | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Il0fmfOuZmcxH8Beh6YJf6JaI_Q_IGVO?usp=sharing) |
| `ILORA_Notebook2_RAG_System.ipynb` | RAG chatbot + few-shot classifier + Gradio | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Io3FGdGiSA9LTTSIidHDGlW5buTiDpp9?usp=sharing) |

---

## Key Results

| System | Result |
|---|---|
| RAG Chatbot | Grounded answers, guardrail verified |
| Few-Shot Classifier | 79.17% accuracy, no fine-tuning |
| Anti-Hallucination | Refuses to answer when data unavailable |

---

## System Architecture

```
ILORA Corpus (1,747 chunks from Notebook 1)
            ↓
    Sentence Embeddings
    (all-MiniLM-L6-v2)
            ↓
    FAISS Vector Index
            ↓
    ┌───────────────────────────────────────┐
    │                                       │
    ↓                                       ↓
RAG Chatbot                        Few-Shot Classifier
    ↓                                       ↓
Retrieve top-3 chunks                 8-shot prompt
    ↓                                       ↓
Build grounded prompt               Predict category
    ↓                                       ↓
Llama 3.2 3B generates                Return label
    ↓
Gradio Chatbot UI
```
---

## Tech Stack

| Component | Tool |
|---|---|
| Data Processing | pandas |
| Embeddings | sentence-transformers/all-MiniLM-L6-v2 |
| Vector Search | FAISS IndexFlatIP |
| Language Model | Llama 3.2 3B Instruct (4-bit) |
| Interface | Gradio |
| Hardware | Google Colab T4 GPU |
| License | MIT / Apache 2.0 |

---

## Setup

1. Clone this repository
2. Upload data CSVs to Google Drive at `ILORA_PoC/data/`
3. Open notebooks in Google Colab with T4 GPU
4. Run Notebook 1 first then Notebook 2

---

## Data

Built on the ILORA database:
> Pant, V. et al. (2021) ILORA: A Database of Alien Vascular 
> Flora of India. Ecological Solutions and Evidence.

---

## Limitations

- State-level distribution only - no district level data
- No management strategy data in ILORA
- English only - no multilingual support yet
- Classifier accuracy 79.17% - fine-tuning needed for deployment

---

## License

Code: MIT License
Data: Subject to ILORA database terms of use

