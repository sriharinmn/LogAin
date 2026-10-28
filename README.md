# LogAin

An incident assistant for telecom network operations centres (NOCs), built at the **Dataset 24** hackathon.

Given an incident ID, LogAin pulls the incident's network measurements, predicts the likely root cause with a trained classifier, and has an LLM write a step-by-step remediation report grounded in a reference document. It also includes a chat assistant for NOC engineers and a map dashboard of affected areas.

## Features

- **Root-cause prediction**: a scikit-learn model (`model.pkl`) classifies incidents from jitter, latency, packet loss and signal strength.
- **Remediation reports**: retrieval-augmented generation over the PDFs in `dataset/` (FAISS + `all-MiniLM-L6-v2` embeddings, Gemma 2 9B through Groq). The report is exported as a PDF.
- **Hand-off continuity**: engineers record the actions taken so far and the issues hit, and the next report picks up from there.
- **NOC chat assistant** (`pages/Chatbot.py`): a conversational assistant that keeps per-session history.
- **Dashboard** (`pages/Dashboard.py`): prototype map views of incident impact and network load, drawn from generated sample points.

The incident data in `dataset.csv` is synthetic.

## Run it

```bash
git clone https://github.com/sriharinmn/LogAin.git
cd LogAin
pip install -r requirements.txt
cp .env.example .env        # then add your Groq, Hugging Face and LangChain keys
streamlit run main.py
```

## Tech stack

Python, Streamlit, scikit-learn, LangChain, Groq, Hugging Face sentence-transformers, FAISS, FPDF.
