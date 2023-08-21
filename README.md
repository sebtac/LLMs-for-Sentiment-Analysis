# LLMs for Sentiment Analysis

FINE-TUNING LLM MODLES for SENTIMENTAL ANALYSIS
- Based On: https://huggingface.co/blog/sentiment-analysis-python
- Using HuggingFace
- LLM: "distilbert-base-uncased"
- Fine-Tune Dataset: "imdb"
- Train Dataset Size: 25000 Reviews
- Test Dataset Size: 25000 Reviews

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
