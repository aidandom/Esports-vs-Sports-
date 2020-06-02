# Esports vs Sports! 
## A project using web APIs & NLP

### Problem Statement

Should esports be considered a sport?


---

### Overview

For this project, I used the reddit pushhift API to scrape user posts from the r/Sports and r/Esports subreddits. This data included subreddit labels, post title, and post selftext. I wanted to analyze the similarities and overlap between traditional sports and esports. I cleaned and preprocessed the data and explored it, looking at similarities and differences between the two subreddits.

### Dataset Features

|Feature|Type|Description|
|---|---|---|
|**subreddit**|*obj*|subreddit label|
|**selftext**|*obj*|selftext for each reddit post|
|**title**|*obj*|title and main body for each reddit post|

### Model Features
The features for the model included 500 of the Count Vectorized features of the Lemmatized title feature.


### Procedure / Methodology
For this project, I began by using the reddit pushshift API to scrape reddit post data from the r/Esports and r/Sports subreddits.  I started with NLP Preprocessing: I generated a data frame with 2000 posts (1000 from r/Esports and 1000 from r/Sports). I then tokenized and lemmatized each of the post to cut down redundancies. I then dropped 13 entries which didn't have entries in the post title. 

After cleaning the data, I started my EDA. I began my analysis by generating word and character counts for each subreddit class and found that r/Esports posts averaged more words and characters per post than those of r/Sports. I then applied a `CountVectorizer` to the `title` feature and assessed the top words from both subreddit. Using these top words, I created a list of words that overlapped between the two.

---
Below is a table of the top 10 most frequent unique words for each subreddit.

|Subreddit|Top 10 Words| 
|-----|-------| 
|**sports**|sport, amp, player, best, year, nfl, team, game, draft, coronavirus|
|**esports**|esports, league, team, valorant, game, coronavirus, tournament, csgo, player, new|


Comparing the unique words in each, the following overlapping words were prevalent.


|Overlapping Words|
|-----|
|league, team, game, coronavirus, player, new, sport, covid|

---
For the modeling process, I split the data into training and testing sets. I then fit 5 different classifications models: `Logistic Regression`, `KN`, `MultinomialNB`, `GaussianNB`, and `SVM Polynomial Kernel`. For each, I used a grid search with cv=10 to optimize transformers and pipeline parameters. The best performing model was Multinomial Naive Bayes with a training score of `0.851006711409396`and a testing score of `0.8812877263581489`. 

After modeling, I produced a confusion matrix with ROC curve. I resulting Sensitivity was `0.8947368421052632` and the resulting Specificity was `0.864`. The ROC AUC score was `0.941`.

### Conclusion
After analyzing the data and looking for similarities and differences between the two subreddits, I found that there were no significant differences between the two. The main differences involved keywords unique to each field, such as game/sports titles and influential figures and players. Surprisingly, the model misclassified more sports posts for esports posts than it misclassified esports posts for sports posts. This is evidence of their overlap and similarities. As a result of the model's Sensitivity and Specificity and the overlapping and unique words, I would recommend that esports be considered a real sport and grouped with traditional sports


### Data Sources

https://www.reddit.com/search/?q=sports

https://www.reddit.com/search/?q=esports
