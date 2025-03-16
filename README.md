Overview
This project investigates whether sentiment extracted from financial news headlines can predict market movements. By integrating Natural Language Processing (NLP) techniques with time series forecasting methods, the project aims to quantify market narratives and forecast the daily returns of SPY (the S&P 500 ETF). The pipeline includes data collection and preprocessing, entity extraction and sentiment analysis, semantic embedding and clustering, and ARIMAX modeling with rolling validation.

Project Description
Financial markets are influenced by a myriad of factors, among which market sentiment plays a pivotal role. Investors and traders often base their decisions on the prevailing narratives in the news. In this project, we explore the possibility that sentiment extracted from financial headlines can serve as a reliable predictor for market returns. To achieve this, we combined NLP techniques with time series analysis. We collected financial headlines from reputable sources (Reuters, CNBC, and Event Registry) and historical market data from yfinance. After preprocessing the headlines (converting to proper formats, handling missing values, and extracting key entities with spaCy), we applied FINBERT to generate sentiment scores. These scores were then aggregated on a daily basis to form an exogenous sentiment signal. Additionally, we employed SentenceTransformer to generate semantic embeddings, applied clustering via KMeans, and visualized the results using t‑SNE. The final forecasting model, an ARIMAX (SARIMAX) model, incorporated this daily sentiment as an exogenous variable to predict SPY returns.

Installation
To install the required packages, ensure you have Python 3.8+ installed and run the following commands in your terminal:

bash
Copy
git clone [repository_url]
cd [repository_folder]
pip install -r requirements.txt
Additionally, download the spaCy model by executing:

bash
Copy
python -m spacy download en_core_web_md
Data
This project uses two primary datasets:

Financial News Headlines: Collected from Reuters (2018–2020) and supplemented with recent headlines via Event Registry. The headlines are preprocessed and analyzed to extract sentiment and key entities.
Market Data: Historical SPY market data was obtained via yfinance, including open, high, low, close, volume, and computed daily returns. The market data is merged with daily aggregated sentiment scores to form the forecasting dataset.
Methodology
NLP Pipeline and Semantic Analysis
Financial headlines are first preprocessed by converting data types, handling missing values, and applying Named Entity Recognition (NER) using spaCy. We extract and rank key entities to understand the dominant narratives (e.g., US-China trade tensions, the Coronavirus outbreak). FINBERT is used to compute sentiment scores for each headline, which are aggregated by day. To capture the semantic similarity between headlines, we generate dense embeddings using SentenceTransformer. These embeddings are clustered using KMeans and visualized in a two-dimensional space via t‑SNE.
Figure 1: t‑SNE Plot of Reuters Headline Embeddings, with clusters labeled by representative TF‑IDF terms.

Time Series Forecasting with ARIMAX
The core forecasting model is built using ARIMAX (SARIMAX) methodology. The dependent variable is the daily return of SPY, and the model includes the aggregated sentiment score as an exogenous regressor. The SARIMAX(1, 0, 1) model captures both the autoregressive and moving average components of market returns, while rolling validation (using TimeSeriesSplit) ensures that the model is trained on past data and tested on future data.
Figure 2: ARIMAX Forecast of SPY Returns with 95% Confidence Intervals.

Results
The ARIMAX model reveals that the sentiment score is a statistically significant predictor of market returns. A one-unit increase in sentiment is associated with a 0.65 percentage point increase in return, with robust p-values supporting the significance of both the sentiment and the AR/MA components. However, performance metrics such as forecast accuracy and ROC AUC indicate only modest predictive power. The model’s residuals exhibit non-normality and heteroskedasticity, suggesting that additional features and model refinements (e.g., incorporating volatility models like GARCH) may further enhance forecasting accuracy.

Discussion and Future Work
While the integration of NLP and time series analysis provides valuable insights into market narratives and their potential impact on returns, the current model demonstrates limited predictive power when using sentiment as the sole predictor. Future work will focus on enriching the feature set with technical indicators and macroeconomic variables and exploring non-linear models and advanced time series techniques to better capture the complex dynamics of financial markets. Moreover, refining the sentiment analysis process and addressing model residual issues could lead to more robust and accurate predictions.

Concluding Remarks
In conclusion, this project demonstrates that financial headline sentiment has a statistically significant relationship with market returns. However, the modest predictive power of the current model highlights the need for a more comprehensive approach, integrating additional data sources and sophisticated modeling techniques. The findings lay a solid foundation for future research aimed at developing more robust sentiment-based market prediction models. The integration of cutting-edge NLP methods and time series forecasting represents a promising direction for understanding and forecasting market dynamics in an increasingly complex financial landscape.

Requirements
See the requirements.txt file for a complete list of required packages.


Figure 1: t‑SNE Plot of Reuters Headline Embeddings. Clusters are labeled with representative TF‑IDF terms.
![Screenshot 2025-03-15 at 3 53 03 PM](https://github.com/user-attachments/assets/1948be94-2597-4421-9478-892f1f768868)



