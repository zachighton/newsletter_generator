# Data Driven - a Data Science Email Newsletter made (mostly) using Python

<img width="522" alt="Screenshot 2021-12-16 at 09 53 09" src="https://user-images.githubusercontent.com/89530964/146339237-0d45b14e-551f-4b4e-b082-49533209b7d0.png">


## Table of Contents
- [The Idea](#The-Idea)
- [Process & Tools](#Process-&-Tools)
- [Conclusion and Next Steps](#Conclusion-and-Next-Steps)

## The Idea

The idea was to create a data science email newsletter which was semi-automated in Python to reduce production time. The newsletter would give you some article suggestions along with a short summary of their contents so you could see whether you wanted to read the full article. It would also display local weather information and stock market data.

In order to create the newsletter, the program

For the content of the newsletter, I scrape articles from the internet, filter them for relevancy and then automatically generate summaries. The notebook also calculates useful information such as the read time and approximate difficulty level for each article.

## Process & Tools

### Python

The majority of the process was carried out in Python. A link to the Jupyter Notebook can be found (here)[link].

**Getting articles:**

I used a Python library named Newspaper3k to scrape a list of data science and technology websites and get back their most recent articles. I then put these articles in to a Pandas dataframe along with relevant information including the title, author(s), a link to the article, keywords and the first image in the article.

**Cleaning:**

I then cleaned the articles to remove any unneccesary characters and ensure website links work. I dropped any particularly short articles where there was a risk that the whole article had not been scraped and also removed articles which the summariser would not deal well with.

**Filtering for relevancy:**

I used NLTK, a natural language processing library, to get back the most common word pairs (collocations) for each article. I then filtered out any articles which did not contain relevant keywords or word pairs.

**Assessing difficulty level:**

To assess the difficulty level of each article, I determined three lists of data science keywords and word pairs. In the first list I included words which I thought were likely to appear in more basic, 'beginner', articles, the second for an 'intermediate' difficulty and the final list for 'advanced'.

I then searched the articles for these keywords and came back with the relative number of keywords present in the article from each list. If over 30% of the keywords were from the advanced category, the article is categorised as advanced. If this was not the case but 50% of the keywords are from the intermediate list, then the article is marked as 'intermediate' else it is marked as 'beginner'.

Though not a perfect system it certainly helps to give the reader a general idea of how complex the ideas contained within an article are likely to be.

**Generating Summaries:**

To generate the summaries I use BART. I am using a form of BART which has been pretrained on the CCN/DailyMail dataset, which contains just over 300k unique news articles written by journalists at CNN and the Daily Mail. BART is trained by corrupting these articles with an arbitrary noising function and then learning a model to reconstruct the original text.

I am running this model using the Transformers library alongside PyTorch.

By using this model, the program can generate relatively accurate summaries of the articles at the length required. In this case, to be short enough to fit into a newsletter, the summaries are of around 120 words in length. Given that the length is so short, it is generally not possible to generate a full summary of the article, however an introduction can be provided to give the reader an idea of the contents of the full article if they were to read it.

**Additional Features:**

I used the OpenWeather API to get back local weather information such as high and low temperature, weather status and sunrise/sunset times. It also brings back an appropriate icon for the weather.

The YahooFinance API allowed me to return the closing postion of the stock markets for the previous day and calculate the percentage difference with the day before.

The program also calculates the average read time of the article.

**Export:**

Once all the information is gathered it is exported in a folder in the correct format alongside an image from the article.

### Canva

It is now a simple process to construct the newsletter. I chose to do this with Canva, but any design software could be used. I have made a template which could be reused daily and quickly updated with that day's articles.

A link to an example of a finished newsletter can be found (here)[link].

## Conclusion and Next Steps

The process of making the newsletter after the notebook has run should be between 5 and 10 minutes. The task of getting back all the information included in the newsletter and reading the articles and writing summaries, could easily take a person several hours. I therefore think that this notebook could represent a huge time save to someone that needed to produce a daily newsletter. The generation of summaries is the greatest time saver, but having weather and stocks information as well as difficulty level and read time all in the desired format adds up, in my opinion, to an enourmous saving in time and energy.

Though I believe the project to be successful, there are ways in which it could be improved. Full automation of the newsletter would be ideal, although it seems difficult to fully automate production and at the same time achieve a nice design. The summaries though good are not perfect and might be improved by further fine tuning of the model, which wasn't withing the scope of this project. Of course, this program could be quickly adapted to a range of topics outside of data science and it would be nice to implement it in other areas.


