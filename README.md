# Generating-Rate-Features-For-Mobile-Applications

[PDF Link](https://dl.acm.org/doi/pdf/10.1145/3647632.3647986)

### Premise
Mobile app stores currently utilize a "one-size-fits-all" rating mechanism, consisting of five-star scales and free-text reviews. This approach fails to capture the specific operational characteristics of different application domains. For example, a user looking for a mental health app cares about "treatment effectiveness" and “finding with mental health experts.” A ride-hailing user cares about "wait times" and “safe drivers.” However, current app rating frameworks often require users to navigate brief, subjective, or one-dimensional app reviews when attempting to make informed choices, such as install an app or recommend an app to close friends. 


### Proposal
In this paper, we propose an automated, unsupervised solution to represent a large volume of app reviews as "**Rate Features**." A rate feature is a neutral, domain-specific trait that nudges users to provide better feedback. 


### Research Gap
Existing solutions for mining app reviews rely on general-purpose text analysis techniques, such as Latent Dirichlet Allocation (LDA) for topic modeling, or various supervised classification methods. Generally, developers leverage these techniques to extract maintenance-related tasks like bug reports, requests for enhancing existing features or new feature requests. As a result, these outcomes tend to overlook the more nuanced, user-centric quality traits present within the reviews. In particular, the current methods having following gaps:
- _Context Loss_: LDA often generates redundant topics or loses the context of the original review. In this framework, a topic is defined as a cluster of unique words with the highest probability of co-occurrence within the sampled reviews.
- _Abstraction_: Extant literature on text summarization are frequently used to generate technical, context-preserving reports focusing on Non Functional requirements (e.g., security). However, these reports are too abstract for average app users, who prioritize domain-specific objectives like “fraud prevention” and “personal identity safety”. 
- _Scalability_: Supervised techniques require extensive manual labeling and cannot keep up with the rate of innovation in the app market. According to a Statista report from 2024, the top 100 apps in each popular category receive an average of over 1k daily reviews. Furthermore, apps evolve their functionalities over time, which subsequently alters user experiences and the nature of their feedback. 


### Proposed Architecture
To generate Rate Features from a set of reviews for an app, we proposed the following two tasks:
1. **Extractive Summarization**: We used a Hybrid TF-IDF algorithm combined with GloVe word embeddings to extract salient, representative sentences from thousands of reviews while filtering out noise. We found some **users even submit their feedback in the form of poems within app reviews**!
2. **LLM Abstraction**: Then, we employed the GPT-3.5 model (specifically gpt-3.5-turbo) to abstract the extractive summaries into "User Goals." Through prompt engineering, we demonstrated that prompting for "neutral user goals" outperformed prompts for adjectives or generic NFRs.


### Empirical Evaluation & Key Findings
- **Dataset**: Analyzed 90 popular apps across three domains: Ride-hailing, Mental Health, and Investing (totaling over 167,000 reviews).
- **Performance**: The proposed algorithm achieved nearly 100% recall for the top 3 Rate Features in all domains compared to manual annotation.
- **Comparison**: The LLM-based approach successfully identified domain-specific nuances (e.g., "Patient Drivers" for ride-hailing) that baseline topic modeling (LDA) failed to capture.


### Technical Limitations
- **External Validity**: The analysis was limited to three specific application domains, which may impact generalizability to other app categories.
- **Dependency**: The quality of the output depends on the specific hyperparameters and version of the LLM used (GPT-3.5).


### Future Research Directions
- **Human Evaluation**: Conducting Randomized Controlled Trials (RCTs) to measure if displaying these Rate Features positively influences users in their app reviewing behavior. The goal is to test the "Nudge Theory" interface in a live app store environment to see if it impacts app-install decisions.


### Tools, Techs, and Methods 
- **LLM & Prompt Engineering**: OpenAI API (GPT-3.5), Zero-shot learning, and hyperparameter tuning (temperature, max_tokens).
- **NLP & Machine Learning**: NLTK for text preprocessing, Gensim for LDA topic modeling, GloVe embeddings for semantic similarity.
- **Data Analysis**: Qualitative thematic analysis for ground-truth generation.
Python Libraries: Pandas, NumPy, Scikit-learn.

