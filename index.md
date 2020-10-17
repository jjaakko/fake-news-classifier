---
layout: default
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
This means that disinformation spreads further and faster online than it ever could before.
[Rand.org](www.rand.org), one of the [most influential](https://thebestschools.org/features/most-influential-think-tanks/) [think tanks](https://en.wikipedia.org/wiki/Think_tank) has compiled [a list of all the services that seek to ascertain the accuracy of information](https://www.rand.org/research/projects/truth-decay/fighting-disinformation/search.html#q=&typeOfTool=Verification).
There are fewer than 40 of them in the US, a country with [244 million social media users](https://www.statista.com/statistics/273476/percentage-of-us-population-with-a-social-network-profile/#:~:text=In%20the%20United%20States%2C%20an,exceed%20257%20million%20by%202023.). 
Of the services that assess text (some focus on photos and videos), the gross majority have fewer than 25 employees and do not employ any AI nor machine learning automation in the checking.<br>
<img src="assets/images/me.jpg" alt="Photo" hspace="0" width="100%" align="center"/><br> 
We obtained gold labels for nearly 70000 articles from the three services which we perceived to be the most renouned (based only on our experience).
These articles were labeled as "fake" or "not fake" by [snopes.com](https://www.snopes.com/), [emergent.info](http://www.emergent.info/) or [politifact.com](https://www.politifact.com/).
Human-labeled instances which are presumed to be correct are referred to as "gold labels."<br>
#Include visualization(s) here of the 70000 articles (snopes or emergent or politifact and fake or not fake)
 

## Contact

My email address is of the form first_name.last_name@helsinki.fi. 

## Courses I've Taken

[MATHEMATICS FOR LINGUISTS](https://courses.helsinki.fi/en/kik-lg209/130394667), Spring 2018

[INTRODUCTION TO LANGUAGE TECHNOLOGY](https://courses.helsinki.fi/en/kik-405/130355898), Fall 2019

## Projects
[Repository for setting up this webpage (cmdline-course Github project)](https://github.com/dean-rahman/dean-rahman.github.io)

[Number of births per Finnish maternity clinic nurse, average for maakunta (static map)](https://autogis-2018.github.io/exercise-5-dean-rahman/Exercise_5_Problem_1_static_map_w_basemap.png)

[Interactive map, created in Geopandas](https://autogis-2018.github.io/exercise-5-dean-rahman/Exercise_5_Problem_2_Interactive_Map.html)

## Misc. 

[My favorite activities outside work are learning languages with my wife Elina and swimming with my son Kaleb and daughter Aurora.](https://www.espoo.fi/en-US/Culture_and_sport/Sports/Sports_and_Recreation_Facilities/Swimming_halls/Leppavaara) 