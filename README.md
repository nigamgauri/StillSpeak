# Chatbot for Mental Health

Built by **Gauri Nigam**, a **third-year B.Tech student**. I created this project as part of my research work and open-sourced the scripts so others can learn from end-to-end chatbot implementations in Python.

## Updates (2024)
- Fixed issues caused by outdated library versions/methods in Python scripts
- Added `requirements.txt` for easy installation of dependencies

**Python version:** Use Python **3.8** (≤ 3.8 is safest) because some libraries (e.g., TensorFlow) require it.

I developed this as a research project under a faculty mentor at my university using a **self-scraped dataset**. Because that dataset is confidential, this repo includes a **sample Kaggle dataset** instead. I’m sharing the code openly to compile different **chatbots from scratch in Python**, which I personally found hard to locate while doing my research.

## Motivation

The National Mental Health Survey (2017) reported that one in seven people in India suffer from mental disorders, including depression and anxiety. Access and affordability remain major challenges, especially for low- and middle-income communities. This project aims to make mental-health support more accessible; the conversational agent can complement clinicians to improve reach and effectiveness.

## Classifications of Chatbots

Chatbots can be classified along several dimensions. My research focused on the **design approaches**: rule-based, retrieval-based, and generative-based.
<img src="https://github.com/nigamgauri/StillSpeak/blob/986a3c29e7ee418b1c5bd849157fb0a0f59dc151/classification.png"
width="500" height="600">


1. **Rule-based Chatbots**: Use rule/pattern matching to pick a response from predefined text (no new text generation).
2. **Retrieval-based Chatbots**: Use ML/DL models to select the best response from a fixed pool (also do not generate new text).
3. **Generative-based Chatbots**: Generate new responses from scratch (e.g., seq2seq/MT-style models).

## Overview of the Bots Trained

The sample dataset comes from Kaggle: **[Mental Health FAQ](https://www.kaggle.com/narendrageek/mental-health-faq-for-chatbot)** with 98 FAQs (columns: `QuestionID`, `Questions`, `Answers`).  
> Note: To train the retrieval chatbot, I manually converted the CSV to JSON. Since this is not my original research dataset, I used only the first 20 rows for demonstration.

This repo includes three notebooks—one per chatbot type:

1. **Rule-based**: TF-IDF with NLTK tokenization for preprocessing; evaluated via cosine similarity.
2. **Retrieval-based**: Trained multiple models:
   - Vanilla RNN
   - LSTM
   - Bi-LSTM
   - GRU
   - CNN

   Retrieval models were trained on the **JSON** format. With regularization and validation, the **CNN** architecture performed best (Embedding → CNN → Fully Connected).

3. **Generative-based**: An **encoder–decoder (seq2seq) LSTM** model trained on the CSV. In simple terms, the model predicts the next word based on the probability of likely sequences, enabling it to produce a full response.

### JSON vs. CSV (Why both?)
- **JSON** is hierarchical and better suited for retrieval-based bots that rely on **tags/contexts** to map inputs to a finite set of predefined responses. The model predicts a tag from the user’s context and returns one of the mapped replies.
- **CSV** is convenient for **generative** models, which don’t need tags—typically just two columns (input text, output text) are sufficient and easy to maintain.

## Future Goals

I plan to extend the generative chatbot with **attention mechanisms** on top of LSTM to better capture long-range dependencies in the decoder and improve response quality.
