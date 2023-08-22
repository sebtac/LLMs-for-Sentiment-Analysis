# LLMs for Sentiment Analysis

ANALYSIS 1: FINE-TUNING LLM MODLES for SENTIMENTAL ANALYSIS
- Based On: https://huggingface.co/blog/sentiment-analysis-python
- Using HuggingFace
- LLM: "distilbert-base-uncased"
- Fine-Tune Dataset: "imdb"
- Train Dataset Size: 25000 Reviews
- Test Dataset Size: 25000 Reviews
- Analysis File: 
Fine_tune_a_pre_trained_model_for_sentiment_analysis.ipynb

Results:
- Based on 25K/25K and 2 Epochs
- Base model produced 49% Accuracy
- Fine-Tuned (only 2 Epochs on all data) prodcued 93% Accuracy

ToDoS
- Run the test on 10+ Epochs
- Train with LoRA, QLoRA, ...
- Train using big model in Model Distributed mode
- Train with Data Distributed mode
- Train Big Model with LoRA in Model and Data Distributed modes

Notes:
- Once you fine-tune it overwrites the weights of the model specicified in Trainer. thus you need to save a "model-base" copy for comparison analysis or capture or required tests on the HuggingFace model before Fine-Tuning


ANALYSIS 2: COMPARISON OF PERFORMANCE OF DIFFERENT PRE-TRAINED LLMs
- Analysis File: Sentiment-analysis-pre-trained-model-comparison.ipynb
- Models tested:
  - "finiteautomata/bertweet-base-sentiment-analysis" -- tailored for Sentiment Analysis; expected to have the best performance
  - "ProsusAI/finbert" - fine-tuned to specific corpra thus expected to have lower performance on general data
  - "nlptown/bert-base-multilingual-uncased-sentiment" -- MULTILINGUAL... thus it is expected that its performance will be weaker then that of just-english based model
- Main focus on:
  - How sure the model is that POSITIVE/NEGATIVE is indeed such?
  - How is it going to handle the AMBIGUOUS/NEUTRAL statment?
- Test Phrases:
  - "I love you" -- POSITIVE
  - "I hate you" -- NEGATIVE
  - "the product would be great, had it not broke a minute after I purchased it" -- AMBIGUOUS/NEUTRAL
- Results:
  - [{'label': 'POS', 'score': 0.9916695356369019}, {'label': 'NEG', 'score': 0.9806600213050842}, {'label': 'NEU', 'score': 0.5101691484451294}]
  - [{'label': 'neutral', 'score': 0.863226056098938}, {'label': 'negative', 'score': 0.5504229664802551}, {'label': 'positive', 'score': 0.5826259255409241}]
  - [{'label': '5 stars', 'score': 0.8546809554100037}, {'label': '1 star', 'score': 0.6346074342727661}, {'label': '3 stars', 'score': 0.2557951807975769}]
- Findings:
  - The model fine-tuned for general sentiment analysis in english had the strongest performance as seen by the highest values (probabilities) associeted with the correct categories... as expected
  - That model had also the highest value for the AMBIGUOUS/NEUTRAL statment, while the finance-tuned model got that statment completely wrong -- but for me personally still it made lessser error then if it categorised the statement as purely negative!!!
  - Multilingial model got the answrs correclty but with lower probabiliaties (less certain about its choices) this might be caused by the fact that it works with 5 categories (not 3) thus the probabilities it assiges to each category are "distillead" by the presence of more categories (it needs to assign some value to each category, while the sum of values is 1!!!)
