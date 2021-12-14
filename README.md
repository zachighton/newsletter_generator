# Data Driven - a Data Science Newsletter made using Python

## Table of Contents
- [The Idea](#The-Idea)
- [Process & Tools](#Process-&-Tools)
- [Visualizations](#Visualizations)
- [Key Take Aways](#Key-Take-Aways)
- [Next Steps](#Next-Steps)

## The Idea

The idea was to create a newsletter about data science and related topics, which could be semi-automated in Python to reduce production time.

For the content of the newsletter, I scrape articles from the internet, filter them for relevancy and then automatically generate summaries in Python. I am also able to generate useful information such as the read time and approximate difficulty level for each article.

On top of that, I get back local weather information and current stock prices to augment the newsletter.

## Process & Tools

### Python

The majority of the process was carried out in Python. 

**Getting articles:**

I used a Python library named Newspaper3k to scrape a list of data science and technology websites and get back their most recent articles. I then included these articles in a Pandas dataframe with relevant information including title, the main text, author(s), link to the article, keywords and the first image in the article.

**Cleaning:**

I then cleaned the articles to remove any unneccesary characters and cleaned up website links. I dropped any particulary short articles, where there was a risk that the whole article had not been scraped and also removed articles which the summariser would not deal well with.

**Filtering for relevancy:**

I used NLTK, a natural language processing library, to get back the most common word pairs (collocations) for each article.

I then filtered out any articles which did not contain relevant keywords or word pairs.

**Assessing difficulty level:**

To assess the difficulty level of each article, I determined three lists of data science keywords. One which I felt were likely to be included in 'beginner' articles, one for an 'intermediate' difficulty and finally 'advanced'.

I then searched the articles for these keywords and came back with the relative number of keywords present in the article from each list. If over 30% of the keywords were from the advanced category, the article would be categorised as advanced. If however, this was not the case, but 50% of the keywords were from the intermediate list, then the article would be marked as 'intermediate' else it would be marked as 'beginner'.

Though not a perfect system it certainly helps to give the reader a general idea of how complex the ideas contained within an article are likely to be.

**Generating Summaries:**

To generate the summaries I use BART. I am using a form of BART which has been pretrained on the CCN/DailyMail dataset, which contains just over 300k unique news articles written by journalists at CNN and the Daily Mail. BART is trained by corrupting these articles with an arbitrary noising function and then learning a model to reconstruct the original text.

I am running this model using the Transformers library alongside PyTorch.

By using this model, the program can generate relativley accurate summaries of the articles at the length required. In this case, to be short enough to fit into a newsletter, the summaries are of around 120 words in length. Given that the length is so short, it is generally not possible to generate a full summary of the article, however an introduction can be provided to give the reader an idea of the contents of the full article if they were to read it.

**Additional Features:**

I used 

The program calculates the average read time of the article.

## Visualizations


## Key Take Aways

With the data we currently have access to, we were  not able to accurately predict whether customers were 'good' or 'bad' for the bank.

Using the accuracy_score metric from sklearn, the model achieved a score of 88%. This appears to be a good result. However, when we look at the confusion matrix, we can see that although the model is good at predicting 'good' customers, it also often misassigns 'bad' customers as 'good' customers (a false positive).

This is reflected in the AUC score of 73%, which although not a very bad score, shows that there is room for improvement.

The issue here appears to be that since there are many more 'good' customers at the bank than 'bad' customers, the model is over prioritising that group.

## Next Steps

The obvious next step would be to re-run the model having done some sampling techniques. If we were to over or under sample from the original data to even out the number of 'good' and 'bad' customers that the model recieves, we may be able to get fewer false negatives.

Having access to more data on the customers of the bank would also lead to a more accurate model.
