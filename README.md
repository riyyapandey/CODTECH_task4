Name: Riya Pandey

Company: CODTECH IT SOLUTIONS

ID: CT6WDS1269

Domain: Data Analytics

Duration: July to August 2024

Mentor: Muzammil AHMED

Overview of this Project

Project: Social Media Sentiment Analysis

This project focuses on performing sentiment analysis on social media captions to understand the overall sentiment trends over time. Here’s a detailed overview of the project:

Objectives:
1. Preprocess the Text Data:
   - Clean and preprocess the text data to prepare it for sentiment analysis.

2. Perform Sentiment Analysis:
   - Use NLTK's VADER sentiment analyzer to calculate sentiment scores for each caption.

3. Analyze Sentiment Trends:
   - Calculate the average sentiment score.
   - Visualize sentiment trends over time with a plot, including the average sentiment line.

Steps:

1. Download Required NLTK Resources:
   - Ensure that the `vader_lexicon` is downloaded for sentiment analysis.

   
   import nltk
   nltk.download('vader_lexicon')
   ```

2. Define Preprocessing Function:
   - Create a function to clean and preprocess the text data by converting to lowercase, removing URLs, mentions, hashtags, punctuation, digits, and leading/trailing whitespace.

   
   import re

   def preprocess_text(text):
       text = text.lower()
       text = re.sub(r'http\S+|www\S+', '', text)
       text = re.sub(r'@\w+', '', text)
       text = re.sub(r'#', '', text)
       text = re.sub(r'[^\w\s]', '', text)
       text = re.sub(r'\d+', '', text)
       text = text.strip()
       return text
   ```

3. Define Sentiment Analysis Function:
   - Create a function to perform sentiment analysis using VADER and return the compound sentiment score.

   
   from nltk.sentiment.vader import SentimentIntensityAnalyzer

   def perform_sentiment_analysis(text):
       sia = SentimentIntensityAnalyzer()
       sentiment = sia.polarity_scores(text)['compound']
       return sentiment
   ```

4. Load and Preprocess Data:
   - Load the dataset from a CSV file, preprocess the text data, and perform sentiment analysis on the preprocessed text.

   
   import pandas as pd

   # Load data from CSV file
   df = pd.read_csv('tweets.csv', encoding='latin-1')

   # Preprocess text and perform sentiment analysis
   df['clean_text'] = df['Caption'].apply(preprocess_text)
   df['sentiment'] = df['clean_text'].apply(perform_sentiment_analysis)
   ```

5. Calculate Average Sentiment Score:
   - Compute the average sentiment score across all captions.

   
   average_sentiment = df['sentiment'].mean()
   print(f'Average Sentiment Score: {average_sentiment:.2f}')
   ```

6. Visualize Sentiment Trends:
   - Plot sentiment scores over time and add a line indicating the average sentiment.

   
   import matplotlib.pyplot as plt

   plt.figure(figsize=(10, 6))
   plt.plot(df.index, df['sentiment'], marker='o', linestyle='-', color='b', label='Sentiment Score')
   plt.axhline(y=average_sentiment, color='r', linestyle='--', label='Average Sentiment')
   plt.title('Sentiment Analysis of Captions Over Time')
   plt.xlabel('Caption Index')
   plt.ylabel('Sentiment Score')
   plt.legend()
   plt.grid(True)
   plt.tight_layout()
   plt.show()
   ```

Results:
The plot displays the sentiment scores of individual captions over time with a blue line. The red dashed line represents the average sentiment score across all captions. This visualization helps identify patterns and trends in sentiment over time, providing insights into the overall sentiment of the social media captions analyzed.



