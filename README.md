# Data Driven - a Data Science Email Newsletter made (mostly) using Python

<img width="567" alt="Screenshot 2021-12-16 at 15 46 46" src="https://user-images.githubusercontent.com/89530964/146393288-9f20494d-51bc-4b14-a65a-d5b01adb4485.png">

## Table of Contents
- [Useful Links](#Useful-Links)
- [The Aim](#The-Aim)
- [Process and Tools](#Process-and-Tools)
- [Conclusion and Next Steps](#Conclusion-and-Next-Steps)

## Useful Links

- [Newsletter Example](https://github.com/zachighton/newsletter_generator/blob/main/newsletter_final.ipynb)
- Juptyer Notebook
- Slides

## The Aim

The idea was to create a data science email newsletter which was semi-automated in Python to reduce production time. The newsletter would give you some article suggestions along with a short summary of their contents so you could see whether you wanted to read the full article. It would also display local weather information and stock market data.

In order to create the newsletter, the program scrapes data science and technology websites and brings back recent articles. It then filters them for relevancy and automatically generates summaries. The notebook also calculates useful information such as the read time and approximate difficulty level for each article.

## Process and Tools

### Python

The majority of the process is carried out in Python. The Jupyter Notebook can be found [here](https://github.com/zachighton/newsletter_generator/blob/main/newsletter_final.ipynb).

**Getting articles:**

The program uses a Python library named Newspaper3k to scrape a list of data science and technology websites and get back their most recent articles. It then puts these articles into a Pandas dataframe along with relevant information including the title, author(s), a link to the article, keywords and the first image in the article.

**Cleaning:**

The articles are then cleaned to remove any unneccesary characters and ensure website links work. Any particularly short articles are dropped where there is a risk that the whole article has not been scraped. Articles which the summariser would not deal well with are also removed.

**Filtering for relevancy:**

NLTK, a natural language processing library, is used to get back the most common word pairs (collocations) for each article. I then filter out any articles which do not contain relevant keywords or word pairs.

**Assessing difficulty level:**

To assess the difficulty level of each article, I determined three lists of data science keywords and word pairs. In the first list I included words which I thought were likely to appear in more basic, 'beginner', articles, the second for an 'intermediate' difficulty and the final list for 'advanced'.

The program searches the articles for these keywords and returns the relative number of keywords present in the article from each list. If over 30% of the keywords are from the advanced category, the article is categorised as advanced. If this is not the case but 50% of the keywords are from the intermediate list, then the article is marked as 'intermediate' else it is marked as 'beginner'.

Though not a perfect system, it certainly helps to give the reader a general idea of how complex the ideas contained within an article are likely to be.

**Generating Summaries:**

To generate the summaries I use BART. I am using a form of BART which has been pretrained on the CCN/DailyMail dataset, which contains just over 300k unique news articles written by journalists at CNN and the Daily Mail. BART is trained by corrupting these articles with an arbitrary noising function and then learning a model to reconstruct the original text.

I am running this model using the Transformers library alongside PyTorch.

By using this model, the program can generate relatively accurate summaries of the articles at the length required. In this case, to be short enough to fit into a newsletter, the summaries are of around 120 words in length. Given that the length is so short, it is generally not possible to generate a full summary of the article, however an introduction can be provided to give the reader an idea of the contents of the full article if they were to read it.

**Additional Features:**

The program calculates the average read time of each of the articles. It does this based on the fact that on average people can read 238 words per minute.

The OpenWeather API is used to get back local weather information such as high and low temperature, weather status and sunrise/sunset times. It also brings back an appropriate icon for the weather.

The YahooFinance API allows the program to return the closing postion of the stock markets for the previous day and calculate the percentage difference with the day before.

**Export:**

Once all the information is gathered, the program exports all the article summaries with their title, difficulty level and read time. Accompanying the articles is the top image from the article website. The weather and stock information is also exported in an appropriate format.

<img width="409" alt="Screenshot 2021-12-16 at 15 04 54" src="https://user-images.githubusercontent.com/89530964/146386444-6c845597-94ac-4564-980b-fc8053ece02d.png">


### Canva

It is now a simple process to construct the newsletter. I chose to do this with Canva, but any design software could be used. I have made a template which could be reused daily and quickly updated with that days articles.

An example of a finished newsletter can be found [here](link).

## Conclusion and Next Steps

The process of making the newsletter after the notebook has run should be between 5 and 10 minutes. This represents a large amount of time saved compared to doing the same steps manually. The task of getting back all the information included in the newsletter, reading the articles and writing summaries, could easily take a person several hours. 

The generation of summaries is the greatest time saver, but having weather and stocks information as well as difficulty level and read time all in the desired format adds up to an enourmous amount of time and energy saved.

Though I believe the project to be successful, there are ways in which it could be improved. Full automation of the newsletter would be ideal, although it seems difficult to fully automate production and at the same time achieve a nice design. The summaries though good are not perfect and might be improved by further fine tuning of the model, training it on only data science articles, which wasn't withing the scope of this project. Finally, this program could be quickly adapted to a range of topics outside of data science and it would be nice to implement it in other areas.


