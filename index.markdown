---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: Blog
---

## Introduction
We have built a text classification system for predicting whether a news article is real or fake. 
To learn about our motivation for choosing to work on this kind of system and our longer term vision, please see our promotional [pitch](https://jjaakko.github.io/fake-news-classifier/assets/In_Search_of_the_Real_Fake_News.pdf).
This blog is aimed at our target user who is primarily someone who investigates whether news is fake. But it could also be anyone who reads the news and wants to quickly be able to paste in a story and get an indication of whether it is fake.
<br>
<br>Without going into details on the algorithms we have used, we provide an overview here of how we built our system and explain how we assess its performance. 
We believe that truth investigators would want to understand at this level of detail in order to have the confidence to use our system's automatically generated fakeness assessment.
We propose that they use it at least as a starting point or as a way to prioritize what must be endless work.
For full details on the algorithms we have used, please see our [technical report](https://jjaakko.github.io/fake-news-classifier/resources/).<br>

## For Data, We Gathered News Articles Gold-labeled by Some of Our Target Users
Social media has fundamentally changed information, giving the public direct access to more information than ever before. 
But with the recent proliferation of low-quality or false content, it has become often nearly impossible to discern accurate information. 
The US is a country with [223 million social media users](https://www.statista.com/statistics/278409/number-of-social-network-users-in-the-united-states/) as of 2020.

<div style="text-align: center">
<img src="./assets/images/278409.png" alt="test" hspace="0" vspace="0" width="100%" align="center"/>
</div>

This means that disinformation spreads further and faster online than it ever could before.
[The Rand Corporation](http://www.rand.org), one of the [most influential](https://thebestschools.org/features/most-influential-think-tanks/) [think tanks](https://en.wikipedia.org/wiki/Think_tank), has compiled [a list of all the services that seek to ascertain the accuracy of information](https://www.rand.org/research/projects/truth-decay/fighting-disinformation/search.html#q=&typeOfTool=Verification).
For the 223 million social media users, there are fewer than 40 such services in the US. 
Some of these focus on photos and videos.
Of the services that assess text, the gross majority have fewer than 25 employees and do not employ any AI nor machine learning automation in detecting disinformation.

<div style="text-align: center">
<img src="./assets/images/Slide3.JPG" alt="test" hspace="0" vspace="0" width="100%" align="center"/>
</div>

<br>We obtained gold labels for nearly 70000 articles from the three services (out of the 40) which we perceived to be the most renouned (based only on our own experience).
These articles were labeled as "fake" or "real" mostly by [Snopes](https://www.snopes.com/) (67285 articles), but also by [Emergent](http://www.emergent.info/) (651 articles) and [Politifact](https://www.politifact.com/) (1460 articles).
Human-labeled instances which are presumed to be correct are referred to as "gold labels."

{% include_relative /_includes/html/documents_researched_per_organization.html %}

Below is an interactive frequency bar-chart showing the lengths of the 70000 articles in terms of word count.
Most articles fall in the category of 500 words or fewer. You can hover the over the bars to see the actual numbers.
{% include_relative /_includes/html/histogram.html %}<br>
 
## Simple Explanation of Performance Measures in Natural Language Processing (NLP)
We did this as a project for the course [Introduction to Data Science at University of Helsinki in Fall of 2020](https://studies.helsinki.fi/courses/cur/hy-opt-cur-2021-b449b3af-1ec9-4a04-8a4c-20461c02dbc4), taught by [Prof. Teemu Roos](https://www.cs.helsinki.fi/u/ttonteri/) assisted by [Saska Dönges](https://fuksiwiki.tko-aly.fi/Tuutorit2019#Tutor_Saska_D.C3.B6nges) and [Ioanna Bouri](https://www.linkedin.com/in/ioannabouri/?originalSubdomain=fi).

One of the parameters of the project was to separate out the explanation/message to our target users (i.e. this blog you are reading) from a technical report to our instructors.
This did not mean that the blog had to be completely devoid of quantitative concepts.

For example, if a team were doing a project for better prediction of pregnancy of an individual or if a tumor is malignant, that team would be encouraged to explain to the their target users the concept of a confidence interval from statistics.
While the spread of lies through fake news ultimately leads people to doubt the truth and our project is therefore very serious, it is not so serious at a single moment as someone finding out whether or not they pregrant or will get cancer.

Fortunately, neither are the different measures of accuracy in fake news prediction as difficult for a non-mathematically inclined person as a confidence interval.

Below is a diagram called a ["confusion matrix."](https://en.wikipedia.org/wiki/Confusion_matrix)
It is a funny name, yes, but we hope the reason for it will become clear.
A confusion matrix presents in a table the fundamental measures of performance in NLP (and machine learning in general).

<div style="text-align: center">
<img src="assets/images/Model_A_Confusion.jpg" alt="Photo" hspace="0" vspace="0" width="70%" align="center"/>
</div>

We took a random sample of 6940 out of our nearly 70000 articles and set these aside.
We used the remaining (approximately) 90% of the articles to ["train"](https://en.wikipedia.org/wiki/Machine_learning#Training_models) a model we will call Model-A. 
(There is also a Model-B to be described soon.)
Then we put Model-A to work on the 6940 articles it had never "seen."
* Of the 5175 (i.e. 4180 + 995) articles that had been labeled by Snopes or Emergent as real (Gold Label: 0), 
  * Model-A assessed 
    * 4180 of them correctly as real (Predicted label: 0) and 
    * 995 incorrectly as fake (Predicted label: 1).
* Similarly, of the 1765 (i.e. 559 + 1206) articles that had been labeled by Snopes or Emergent as fake (Gold Label: 1), 
  * Model-A assessed 
    * 559 incorrectly as real (Predicted label: 0) and
    * 1206 correctly as fake (Predicted label: 1).
* The overall "accuracy" of Model-A is then 5386 (i.e. 4180 + 1206) correct divided by all 6940 or 77.61%.
  This simple accuracy is rarely used for scenarios where the gold labels are not split close to 50-50. 
  For example, our dataset had 74.6% (i.e. (4180 + 995)/6940) labeled real (Gold Label: 0) by humans.
  (The training set of articles were in the same proportion of fakes to reals as this testing set).
  So if we had a Model-0 that just always guessed real, we would have an accuracy of 74.6%.
  Compared to this, our Model-A, despite working extremely hard, doesn't seem so impressive.

So we have to dig deeper.
* How many of the gold reals did Model-A assess correctly? 
  80.77% (i.e. 4180/(4180 + 995)). 
  This is the percentage of gold reals Model-A "recalled" correctly, so 80.77% is the recall of Model-A with respect to gold reals.
* What is the recall of Model-A with respect to gold fakes? 
  68.3% (i.e. 1206/(1206 + 559)). 
  Model-0 would have had a recall of 0% for gold fakes because it would have blindly guessed real for all.
  So Model-A is doing a lot better.
* Stating simply "the recall of Model-A" usually refers to recall with respect to the label for which Model-0 would have recalled 0%.
  So the recall of our Model-A is 68.3%

What About [Precision](https://en.wikipedia.org/wiki/Precision_and_recall)?
* Of the times Model-A made an assessment of real, how many times was it correct? 
  88.2% (i.e. 4180/(4180 + 559)).
  This is the precision of Model-A with respect to real.
  Model-0's precision with respect to real would have been the same 74.6% as for accuracy because it guesses real for every article.
* Of the times Model-A made an assessment of fake, how many times was it correct? 
  This is the precision of Model-A with respect to fake.
  54.8% (i.e. 1206/(995 + 1206)).
  This is not great, but it's a lot better than Model O's precision for fake which would have been 0.
* And again, stating simply "the precision of Model-A" usually refers to precision with respect to the label for which Model-0 would have had 0% precision.
  So the precision of our Model-A is 54.8%

The [F1 score](https://en.wikipedia.org/wiki/F1_score) is a way to combine precision and recall together in order to give a sense of how a model is doing using only one number.
* The F1 score of Model-A is 60.8% (i.e. 2 x 68.3% x 54.8%/(68.3% + 54.8%)).

Different measures from this list are important to different members of the NLP field.
For example, [Facebook and Microsoft only report on the precision of their models](https://venturebeat.com/2020/04/07/microsoft-ai-fake-news-better-than-state-of-the-art-baselines/) (i.e. when assessing articles as fake).<br>

## Why Didn't We Use the Articles Labeled by Politifact?
We excluded articles gold labeled by politifact. 
Initially, we thought their rating system was confusing or might be too complicated to train the model on.
This is because the labels (fake or real) did not seem to represent a uniform interpretation of the “fakeness” of a news article across the sources. 
Moreover we had very few articles from Politifact so it made the decision to exclude those articles a little bit easier.
As it turned out, a similar level of complications existed in some of the articles gold-labeled by snopes and emergent as well for other reasons (see the Story of Ghidora below).<br>

## The Story of Ghidora
Below is the typical shape of a diagram showing the most commonly occuring words in a collection of texts such as ours and how often each word occurs.
<div style="text-align: center">
<img src="./assets/images/English_Raw_Top_40.png" alt="test" hspace="0" vspace="0" width="65%" align="center"/>
</div>
The most common words are all boring structural words as shown in this example. 
Then, somewhere in the low frequencies (tens or twenties) are the juicy content words which really give a sense of what the topic is in an article of 500 words.
Lastly, there is the "long tail" of words which make up the majority of words.
They occur only once or just a little more than that.
In our collection of 70000 articles, we had around 40 million 'types' (distinct objects which could be words), even though the English language has fewer than 200000 words.
Most of these 'types' were numerals and user names, etc.
When we took into account the frequencies of all the types, there were 6 billion tokens (picture a token for every word/word-like-object in the bag of all words making up the 70000 articles).
As you can imagine, drawing a random samples of 200 tokens at a time for curiosity, we almost never saw words with frequency higher than 1 or any real words at all.
Except one time, we saw the obscure word 'ghidora.'

We decided that we had to follow the trail and see what article it was in.
This led us to a perfect example which illustrates why an article can be problematic.
<div style="text-align: center">
<img src="assets/images/ghidora.JPG" alt="Photo" hspace="0" vspace="0" width="65%" align="center"/>
</div>
The URL leads not to a single story, but a series of almost unrelated stories by a blogger named [Flea](http://www.ghostofaflea.com/archives/2005_03.html) and 'ghidora' is very far down the series (too far in fact to include in the snapshot above).
This demonstrates that a model can encounter a source which could include both fake and real news.
Moreover, as we found in many, many cases, URLs are likely to have advertising.
Both of these issues greatly burden a model's training and probability of assessing the plain text from a URL correctly.<br> 

## Simple Explanation of Term Frequency–Inverse Document Frequency
To address the above problem, we created Model-A using an algorithm based on something called [term frequency–inverse document frequency (TF-IDF)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).
An explanation of TF-IDF and how we used it can be found in our [technical report](https://jjaakko.github.io/fake-news-classifier/resources/).
However, we want to leave you with an intuition about TF-IDF using the word cloud below which based on Flea's [series of] article[s] [one of] containing ghidora.
<div style="text-align: center">
<img src="assets/images/wordcloud_ghidora.png" alt="Photo" hspace="0" vspace="0" width="100%" align="center"/>
</div>
The intuition behind TF-IDF is that it considers important those words that are common in a particular document but not common in the other documents in the data set. 
The mathematical formulation of TF-IDF produces high scores for these document-specific important words.
The largest words in the word cloud above appear the most in Flea's archive while not appearing so much in the other 70000 articles.
Of course, the word sizes are proportional to the TF-IDF scores which decrease as the word sizes decrease.
Luckily, in this case, Flea is actually a credible underground journalist with a distinct vocabulary and his blog [Ghost of a Flea](http://www.ghostofaflea.com) does not have advertising. 
This may help explain why this article was assessed correctly as real by Model A despite the article's complications.<br>

## What about Model B?
We also created a Model-B using an algorithm based on something called [doc2Vec](https://en.wikipedia.org/wiki/Word2vec#Extensions) which in turn is an extension of [word2vec](https://en.wikipedia.org/wiki/Word2vec).
At first, we trained and tested Model-B in an "unbalanced" way for which the confusion matrix is shown below. 

<div style="text-align: center">
<img src="assets/images/unchanged.png" alt="Photo" hspace="0" vspace="0" width="70%" align="center"/>
</div>

Our unbalanced performance measures for Model-B were Accuracy: 0.747, Precision: 0.608, Recall: 0.104, F1: 0.177.
Finding the recall so low, we prioritized improving it and looked into various ways as to how.
One method we found was to draw samples in a (still random) way which matches the ratios of the real to fake from the 70000 articles in both the training set and testing set.




We subsequently built both Model-A (performance given above) and Model-B in this "balanced" way. 
The confusion matrix for the balanced Model B is shown below.

<div style="text-align: center">
<img src="assets/images/balanced.png" alt="Photo" hspace="0" vspace="0" width="70%" align="center"/>
</div>

Our balanced performance measures for Model-B were: Accuracy: 0.63, Precision: 0.375, Recall: 0.61, F1: 0.465).
This improved our recall dramatically albeit at the cost of precision (and less importantly accuracy), however the overall F1 for the balanced Model-B was also dramatically better.<br>

## Simple Explanation of Word Embeddings Through Visualization

An explanation of doc2Vec and how we used it can be found in our [technical report](https://jjaakko.github.io/fake-news-classifier/resources/).
However, we want to leave you with an intuition about word2vec and by extension doc2vec based on the visualizations below.
They are about the words "gender" and "god" (we have lowercased all words for the models).

Words can be represented as points in high dimensional space.
(We exist in three dimensional space, but mathematically, it is possible to represent an infinite number of dimensions.)
Computationally, we converted all the words from the fake articles to points represented in 300-dimensional space (yes 300)!
These high dimensional points are represented by coordinate combinations called vectors.
We did the same for all the words in the real articles.
For this, we employed a [word embedding model](https://en.wikipedia.org/wiki/Word_embedding). 
Then we compared the similarity of these vectors. 
This is achievable because similar words tend to have similar contexts, and we can then represent relationships between meanings (semantic relations) as geometric relationships (spatial relations).
First, we take a target word, e.g. “gender.” 
The vector for "gender" as used in the fake articles is not exactly the same as the vector for the same word "gender" in the real articles.
We then take the top 10 most similar words to “gender” from both the fake news articles and the real news articles. 
We can plot all of the words, including the fake-news version of “gender” and the real news version of “gender” in two dimensional coordinates using projections.
(Think of a projection as the shadow of the point from 300-dimensional space down onto 2-dimensional space.) 
Let’s see this example play out!

<div style="text-align: center">
<img src="assets/images/gender.bmp" alt="Photo" hspace="0" vspace="0" width="75%" align="center"/>
</div>
As we can see, the word “gender” when talked about in fake articles (at the top middle of the diagram), is closer to words such as sexuality, patriarchy, pronouns and discourses, whereas in real articles, gender (also in the middle but almost at the bottom) is more similar to transgender, intersex, dysphoria and genders. 
We can speculate from this that the real news version of gender is more neutral and scientific, whereas we can see common topics about gender in fake news, such as debating pronouns, etc.

<br>Next, we can see below the different topics that occur with our target word “God.” 
<div style="text-align: center">
<img src="assets/images/god.png" alt="Photo" hspace="0" vspace="0" width="60%" align="center"/>
</div>
Whereas the real news articles are most likely to discuss “God” (near the center of the diagram, offset up and to the left) in a somewhat typical Christian/Western, common or neutral way (for the US), it is pretty clear that the fake-news version of “God” (in the lower right corner) is more often talked about with Islam or Judaism (perhaps to disrespect and condemn minority religions).<br> 

## Future Work
To see more technical next steps, please see our [technical report](https://jjaakko.github.io/fake-news-classifier/resources/). 
The future-work items we can talk about here are as follows:
* We plan to improve our performance.
  * We want to figure out how to extract the relevant story out from other stories (as discussed above with Ghidora) or advertising. 
  All indicators are that this is a project in and of itself but we would be looking to employ existing technologies so we can focus on the stories themselves.

* Increasing scope
  * An easier item will be to test our models or improved versions thereof on the articles labeled by Politifact to check if our concerns were justified.
  * Last, but not least, we hope we have helped you develop the intuition that we need to train and test our models on more articles.
    While we intend to seek new, more recent articles from our current sources, the team _is_ located in Helsinki and we are eager to include Europe in our efforts as alluded to in the first slide of our [pitch](https://jjaakko.github.io/fake-news-classifier/assets/In_Search_of_the_Real_Fake_News.pdf).
    * [EU vs Disinfo](https://euvsdisinfo.eu/) seems like a promising target user.	
    * This will also mean new models for Finnish and other languages.

<img src="./assets/images/https___blogs-images.forbes.com_niallmccarthy_files_2019_06_20190612_Fake_News_Forbes.jpg" alt="test" hspace="0" vspace="0" width="100%" align="center"/>

<br><br>All images are included under [fair use](https://www.socialmediaexaminer.com/copyright-fair-use-and-how-it-works-for-online-images/).