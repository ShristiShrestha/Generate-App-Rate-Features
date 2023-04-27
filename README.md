# Generating-Rate-Features-For-Mobile-Applications
---

This repository contains the replication package for my ASE'23 paper. 

The repository is split into four notebooks.

- [1__data_cleaning](code/data_cleaning.ipynb) - contains the code for processing the app reviews and includes methods such as noise removal, tokenization and lemmatization.
- [2__extractive_summarization](code/extractive_summarization.ipynb) - contains the code for extractive summarization using Hybrid TFIDF.
- [3__ChatGPT_label_generation](code/ChatGPT_label_generation.ipynb) - contains the code for label generation using ChatGPT API. 
The method feeds prompt input  and top ten summary reviews from extractive summarization to the GPT-3.5 Turbo model via OpenAI API.
- [4__ChatGPT_label_selection](code/ChatGPT_label_selection.ipynb) - contains the code for label selection generated using ChatGPT API. 
The method uses the most frequently occurring labels as the rate features for the apps.

### Additional files are added as below
- [`data/raw reviews/*.csv`](data/raw%20reviews) contains csv files for the raw reviews.
- [0__extract_top_rate_features_sampling](code/extract_top_rate_features_sampling.ipynb) - contains the code for top five rate feature extraction from the sample raw reviews.

### Full replication requirements
- Install dependencies using `pip install -r requirements.txt`
- The four methods mentioned above are neither time nor space costly. 
  - Lemmatization process took slightly more time (on average 5 minutes) depending on the review size. Other than that, summarization also takes couple of minutes to complete. 
  - In most cases, the outputs are written to a csv file. 
  - A normal system with 8-16 GB RAM with 1GB works fine.
  - To use OpenAI models, you need an API key for authorization. 
    - For pricing, see the [pricing link](https://openai.com/pricing)
    - For selecting the model, see the [available models here](https://platform.openai.com/docs/models)
    - For prompt engineering (finding the best way to ask GPT), see the [articles here](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api)
   
