Overview

This project applies Natural Language Processing (NLP) to financial news headlines to extract sentiment and key narratives, which are then used as exogenous inputs in an ARIMAX model to forecast market returns for SPY (the S&P 500 ETF). The pipeline includes data preprocessing, sentiment analysis with FINBERT, semantic clustering with SentenceTransformer and t‑SNE, and time series forecasting with ARIMAX.

Installation

Clone the repository and install the required packages:

git clone [repository_url]

cd [repository_folder]

pip install -r requirements.txt

python -m spacy download en_core_web_md

Usage

Run the provided scripts to:

Preprocess news headlines and extract sentiment.
Generate semantic embeddings and visualize headline clusters.
Forecast market returns using the ARIMAX model with sentiment as an exogenous variable.
