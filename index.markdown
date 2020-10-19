---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
## Introduction
We have built a text classification system for predicting whether a news article is real or fake. 
To learn about our motivation for choosing to work on this kind of system and our longer term vision, please see our promotional [pitch](LINK to pitch).
This blog is aimed at our target user who is primarily someone who investigates whether news is fake but also anyone who reads the news and wants to quickly be able to paste is a story and get an indication whether it is fake.
Without going into details on the algorithms we have used, we provide an overview here of how we built our system and explain how we assess its performance. 
We believe that truth investigators would want to understand at this level of detail in order to have confidence to use our system's automatically generated truth assessment as a starting point or a way to prioritize their work.
For full details on the algorithms, please see our [technical report](link to technical report).

## We gathered data from our target users
Social media has fundamentally changed information, giving the public direct access to more information than ever before. 
But with the recent proliferation of low-quality or false content, it has become often nearly impossible to discern accurate information. 
The US is a country with [223 million social media users](https://www.statista.com/statistics/278409/number-of-social-network-users-in-the-united-states/)


<img src="./assets/images/278409.png" alt="test" hspace="0" vspace="0" width="100%" align="center"/>

This means that disinformation spreads further and faster online than it ever could before.
[Rand.org](www.rand.org), one of the [most influential](https://thebestschools.org/features/most-influential-think-tanks/) [think tanks](https://en.wikipedia.org/wiki/Think_tank), has compiled [a list of all the services that seek to ascertain the accuracy of information](https://www.rand.org/research/projects/truth-decay/fighting-disinformation/search.html#q=&typeOfTool=Verification).
For the 223 million social media users, there are fewer than 40 such services in the US. 
Some of these focus on photos and videos.
Of the services that assess text, the gross majority have fewer than 25 employees and do not employ any AI nor machine learning automation in the checking.

<img src="./assets/images/Slide3.JPG" alt="test" hspace="0" vspace="0" width="100%" align="center"/>

We obtained gold labels for nearly 70000 articles from the three services (out of the 40) which we perceived to be the most renouned (based only on our experience).
These articles were labeled as "fake" or "not-fake" by [snopes.com](https://www.snopes.com/), [emergent.info](http://www.emergent.info/) or [politifact.com](https://www.politifact.com/).
Human-labeled instances which are presumed to be correct are referred to as "gold labels."<br>
#Include visualization(s) here of the 70000 articles (snopes or emergent or politifact and fake or not-fake)
 
## Simple explanation of performance measures in natural language processing (NLP)
We did this as a project for the course [Introduction to Data Science at University of Helsinki in Fall of 2020](https://studies.helsinki.fi/courses/cur/hy-opt-cur-2021-b449b3af-1ec9-4a04-8a4c-20461c02dbc4), taught by [Prof. Teemu Roos](https://www.cs.helsinki.fi/u/ttonteri/) assisted by [Saska Dönges](https://fuksiwiki.tko-aly.fi/Tuutorit2019#Tutor_Saska_D.C3.B6nges) and [Ioanna Bouri](https://www.linkedin.com/in/ioannabouri/?originalSubdomain=fi).
One of the parameters of the project was to separate out the explanation/message to our target users (i.e. this blog you are reading) from a technical report to our instructors.
This did not mean that the blog had to be completely devoid of quantitative concepts.
For example, if a team were doing a project for better prediction of pregnancy of an individual or if a tumor is malignant, that team would be encouraged to explain to the their target users the concept of a confidence interval from statistics.
While the spread of lies through fake news ultimately leads people to doubt the truth and our project is therefore very serious, it is not so serious at a single moment as someone finding out whether or not they pregrant or will get cancer.
Fortunately, neither are the different measures of accuracy in fake new prediction as difficult for a non-mathematically inclined person as a confidence interval.<br>
<br> Below is a diagram called a ["confusion matrix"](https://en.wikipedia.org/wiki/Confusion_matrix).
A funny name, yes, but we hope the reason for it will become clear.
A confusion matrix presents in a table the fundamental measures of performance in NLP (and machine learning in general).<br>
<img src="assets/images/Model_A_Confusion.jpg" alt="Photo" hspace="0" vspace="0" width="50%" align="center"/>

<br>We took a random sample of 6940 out of our nearly 70000 articles and set these aside.
We used our the remaining (approximately) 90% of the articles and used them to ["train"](https://en.wikipedia.org/wiki/Machine_learning#Training_models) a model we will call Model-A. 
(There is also a Model-B to be described soon.)
Then we put Model-A to work on the 6940 articles it had never "seen."
* Of the 5175 (i.e. 4180 + 995) articles that had been labeled by Snopes or Emergent as not-fake (True label: 0), 
  * Model-A assessed 
   * 4180 of them correctly as not-fake (Predicted label: 0) and 
   * 995 incorrectly as fake (Predicted label: 1).
* Similarly, of the 1765 (i.e. 559 + 1206) articles that had been labeled by Snopes or Emergent as fake (True label: 1), 
  * Model-A assessed 
    * 559 incorrectly as not-fake (Predicted label: 0) and
    * 1206 correctly as fake (Predicted label: 1).
* The overall "accuracy" of Model-A is then 5386 (i.e. 4180 + 1206) correct divided by all 6940 or 77.61%.
  This simple accuracy is rarely used for scenarios where the outcome is not close to 50-50. 
  For example, our dataset had 74.6% (i.e. (4180 + 995)/6940) labeled not-fake 0 by humans.
  (The training set of articles were in the same proportion of fakes to not-fakes as this testing set).
  So all we had to do is have a Model-0 that just always guessed not-fake and we would have an accuracy of 74.6%.
  Compared to this, our Model-A, who was working extremely hard, doesn't seem so impressive.

So we have to dig deeper.
* How many of the not-fakes did Model-A assess correctly? 
  80.77% (i.e. 4180/(4180 + 995)). 
  This is the percentage of not-fakes Model-A "recalled" correctly, so 80.77% is the recall of Model-A with respect to not-fakes.
* What is the recall of Model-A with respect to fakes? 
  68.3% (i.e. 1206/(1206 + 559)). 
  Model-0 would have had a recall of 0% for fakes because it would have blindly guessed not-fake for all.
  So Model-A is doing a lot better.
* Stating simply "the recall of Model-A" usually refers to recall with respect to the label for which Model-0 would have recalled 0%.
  So the recall of our Model-A is 68.3%

What about [precision](https://en.wikipedia.org/wiki/Precision_and_recall)?
* Of the times Model-A made an assessment of not-fake, how many times was it correct? 
  88.2% (i.e. 4180/(4180 + 559)).
  This is the precision of Model-A with respect to not-fake.
  Model-0's precision with respect to not-fake would have been the same 74.6% as for accuracy because it guesses not-fake for every article.
* Of the times Model-A made an assessment of not-fake, how many times was it correct? 
  This is the precision of Model-A with respect to fake.
  54.8% (i.e. 1206/(995 + 1206)).
  This is not great, but it's a lot better than Model O's precision for fake which, again, would have been 0.
* And again, stating simply "the precision of Model-A" usually refers to precision with respect to the label for which Model-0 would have had 0% precision.
  So the precision of our Model-A is 54.8%

The [F1 score](https://en.wikipedia.org/wiki/F1_score) is a way to combine precision and recall together in order to give a sense of how a model is doing using only one number.
* The F1 score of Model-A is 60.8% (i.e. 2 x 68.3% x 54.8%/(68.3% + 54.8%)).

Different measures from this list are important to different members of the NLP field.
For example, [Facebook and Microsoft only report on the precision of their models](https://venturebeat.com/2020/04/07/microsoft-ai-fake-news-better-than-state-of-the-art-baselines/) (i.e. when assessing an article as fake).

## Why didn't we use the articles labeled by Politifact?

## The Story of Ghidora
# Need a visual of word frequencies.
Below you can find how different articles are distributed in terms of word count.
From the picture it's easy to see that most articles fall in the category of 500 words or less. You can hover the pointer over the image to see the actual numbers.
{% include_relative /_includes/html/histogram.html %}

## What about Model B?
(Balanced: Accuracy: 0.63, Precision: 0.375, Recall: 0.61, F1: 0.465, 
Unbalanced Accuracy: 0.747, Precision: 0.608, Recall: 0.104, F1: 0.177)

## Future work
We plan to improve our performance.
To see more technical next steps, please see our [technical report](link to technical report). 
The future work items we can talk about here are as follows:
* We want to figure out how to extract the relevant story out from other stories (as discussed above with Ghidora) or advertising. 
  All indicators are that this is a project in and of itself but we would be looking to employ existing technologies so we can focus on the stories themselves.
* Our hypothesis is that one way we can improve the models with respect to the stories is to exclude all the words the occured only once.
  If this is successful, we will push the threshold frequency for words to exclude (e.g. all words with frequency less than 10 or 20, etc. will be excluded as features).
* An easier item will be to rerun our models or improved versions thereof with the articles labeled by Politifact.
* Last, but not least, we hope we have helped you develop the intuition that we need to train and test our models on more articles.
  While we intend to seek new, more recent articles from our current sources, the team _is_ located in Helsinki and we are eager to include Europe in our efforts as alluded to in the first slide of our pitch.
  * [EU vs Disinfo](https://euvsdisinfo.eu/) seems like a promising target user.	
  * This will also mean new models for Finnish and other languages.
<img src="./assets/images/https___blogs-images.forbes.com_niallmccarthy_files_2019_06_20190612_Fake_News_Forbes.jpg" alt="test" hspace="0" vspace="0" width="100%" align="center"/>

<br><br>All images are included under [fair use](https://www.socialmediaexaminer.com/copyright-fair-use-and-how-it-works-for-online-images/).