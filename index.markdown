---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
We have built a text classification system for predicting whether a news article is real or fake. 
To learn about our motivation for choosing to work on this kind of system and our longer term vision, please see our promotional [pitch](LINK to pitch).
This blog is aimed at our target user who is primarily someone who investigates whether news is fake but also anyone who reads the news and wants to quickly be able to paste is a story and get an indication whether it is fake.
Without going into details on the algorithms we have used, we provide an overview here of how we built our system and explain how we assess its performance. 
We believe that truth investigators would want to understand at this level of detail in order to have confidence to use our system's automatically generated truth assessment as a starting point or a way to prioritize their work.
For full details on the algorithms, please see our [technical report](link to technical report).

## We gathered data from our target users
Social media has fundamentally changed information, giving the public direct access to more information than ever before. 
But with the recent proliferation of low-quality or false content, it has become often nearly impossible to discern accurate information. 
This means that disinformation spreads further and faster online than it ever could before.
[Rand.org](www.rand.org), one of the [most influential](https://thebestschools.org/features/most-influential-think-tanks/) [think tanks](https://en.wikipedia.org/wiki/Think_tank), has compiled [a list of all the services that seek to ascertain the accuracy of information](https://www.rand.org/research/projects/truth-decay/fighting-disinformation/search.html#q=&typeOfTool=Verification).
There are fewer than 40 such services in the US--a country with [223 million social media users](https://www.statista.com/statistics/278409/number-of-social-network-users-in-the-united-states/). 
Of the services that assess text (some focus on photos and videos), the gross majority have fewer than 25 employees and do not employ any AI nor machine learning automation in the checking.

<img src="./assets/images/Slide3.JPG" alt="test" hspace="0" vspace="0" width="100%" align="center"/>

We obtained gold labels for nearly 70000 articles from the three services (out of the 40) which we perceived to be the most renouned (based only on our experience).
These articles were labeled as "fake" or "not fake" by [snopes.com](https://www.snopes.com/), [emergent.info](http://www.emergent.info/) or [politifact.com](https://www.politifact.com/).
Human-labeled instances which are presumed to be correct are referred to as "gold labels."<br>
#Include visualization(s) here of the 70000 articles (snopes or emergent or politifact and fake or not fake)
 
## Simple explanation of performance measures in natural language processing (NLP)
We did this as a project for the course [Introduction to Data Science at University of Helsinki in Fall of 2020](https://studies.helsinki.fi/courses/cur/hy-opt-cur-2021-b449b3af-1ec9-4a04-8a4c-20461c02dbc4), taught by [Prof. Teemu Roos](https://www.cs.helsinki.fi/u/ttonteri/) assisted by [Saska Dönges](https://fuksiwiki.tko-aly.fi/Tuutorit2019#Tutor_Saska_D.C3.B6nges) and [Ioanna Bouri](https://www.linkedin.com/in/ioannabouri/?originalSubdomain=fi).
One of the parameters of the project was to separate out the explanation/message to our target users (i.e. this blog you are reading) from a technical report to our instructors.
This did not mean that the blog had to be completely devoid of quantitative concepts.
For example, if a team were doing a project for better prediction of pregnancy of an individual or if a tumor is malignant, that team would be encouraged to explain to the their target users the concept of a confidence interval from statistics.
While the spread of lies through fake news ultimately leads people to doubt the truth and our project is therefore very serious, it is not so serious at a single moment as someone finding out whether or not they pregrant or will get cancer.
Fortunately, neither are the different measures of accuracy in fake new prediction as difficult for a non-mathematically inclined person as a confidence interval.<br>
<br> Below is a diagram called a ["confusion matrix"](https://en.wikipedia.org/wiki/Confusion_matrix).
A funny name, yes, but we hope the reason for it will become clear.
A confusion matrix presents in a table the fundamental measures of performance in NLP (and machine learning in general).
<img src="assets/images/Model_A_Confusion.jpg" alt="Photo" hspace="0" vspace="0" width="50%" align="left"/>

We took a random sample of 6940 out of our nearly 70000 articles and set these aside.
We used our the remaining (approximately) 90% of the articles and used them to ["train"](https://en.wikipedia.org/wiki/Machine_learning#Training_models) a model we will call Model-A. 
(There is also a Model-B to be described soon.)
Then we put Model-A to work on the 6940 articles it had never "seen."
Of the 5175 articles (i.e. 4180 + 995) that had been labeled by Snopes or Emergent as not fake (True label: 0), Model-A assessed 4180 of them correctly as not fake (Predicted label: 0) and 995 incorrectly as fake (Predicted label: 1).


To see the exact formula for calculating F1 based on accuracy and precision, please see our [technical report](link to technical report).  
Different measures from this list are important to different members of the NLP field.
For example, Facebook and Microsoft only report on the precision of their models when assessing an article as fake.

## Looking at the data
Word frequencies.
Below you can find how different articles are distributed in terms of word count.
From the picture it's easy to see that most articles fall in the category of 500 words or less. You can hover the pointer over the image to see the actual numbers.
{% include_relative /_includes/html/histogram.html %}

<br><br>All images are included under [fair use](https://www.socialmediaexaminer.com/copyright-fair-use-and-how-it-works-for-online-images/).