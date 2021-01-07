---
layout: post
title: Facebook GDPR Timeline in criminal investigation
subtitle: A small processing and vizualisation of Facebook-GDPR Database
gh-repo: clairebilat/forensic-data-stories
gh-badge: [star, follow]
tags: [facebook, GDPR, timeline]
comments: true
---

# Prologue

## About me

I am a student who decided to complete a [master's degree in Digital Investigation and Identification](https://www.unil.ch/esc/fr/home/menuinst/enseignement/masters/msc-investigation-numerique.html) at University of Lausanne. As part of this, I had to choose a personal practial lab theme for which I would take time to practice my theorical knowledge, produce something useful and maybe publish my results. After the success my colleagues and I had with our _Eat safely in Chicago_ project performed as part of the EPFL course intituled "Applied Data Analysis" (you will find our amazing results in [the first post of this blog](https://clairebilat.github.io/forensic-data-stories/2019-12-20-food-chicago/)), I could not refrain myself to make everything about data analysis once again. Recently out of an internship in an Office of Police where I found myself having to review manually some Facebook profiles, I chose to try and write a script automating the processing and output of some basic vizualisations of Facebook GDPR data to help investigators grab a general idea of one's Facebook profile and its content without having to put too much work into it. 

## About the databases used

The dataset used is the one I downloaded from Facebook containing a copy of my information. You can find yours following these steps :

1. First, go to [Facebook](https://www.facebook.com/) and log in. Then, click on the `Account` button.

<img src="{{site.github.url}}/assets/img/tuto1.PNG">

2. Go to `Settings & privacy`.

<img src="{{site.github.url}}/assets/img/tuto2.PNG">

3. Go to `Settings`.

<img src="{{site.github.url}}/assets/img/tuto3.PNG">

4. Go to `Your Facebook information`.

<img src="{{site.github.url}}/assets/img/tuto4.PNG">

4. Go to `Download your infromation`.

<img src="{{site.github.url}}/assets/img/tuto5.PNG">

5. Choose `Request copy`, adjust your parameters (I personnally chose the JSON format with a low quality of media), and click on `Create File`.

<img src="{{site.github.url}}/assets/img/tuto6.PNG">


## About the purpose of this project


The main research question was : **where to eat *safely* in Chicago ?**

The 

# Litterature review (or how it has already be done better than this but I did it anyway)

Many people have done similar projects (but it is a real pain trying to find them online because of all the Facebook scandals that pops when searching form terms like _Facebook data analysis_... Quick tip, try with keywords like "Analyze Your Personal Facebook Data" and it will be a little bit better).

1. [How much do you post](https://www.dataquest.io/blog/analyze-facebook-data-python/)

This is a great tutorial that is surprisingly easy to follow, explaining in well illustrated steps how to plot your monthly post count. It takes five minutes to perform and is a really great way to introduce you to the structure of the data Facebook offers.

2. [Natural Language Processing](https://towardsdatascience.com/mapping-my-facebook-data-part-1-simple-nlp-98ce41f7f27d)

This article explains how to discover what words you use most, words count, and basic stats about your data. It is out of the scope of my project but is 100% considered as prospect.

3. [Facebook Messenger Data](https://www.youtube.com/watch?v=z9W2cvmFPuA)

This livestream replay is a video tutorial on how to explore your Facebook Messenger in order to compare the friends you contacted most and at which frequency. What is nice is that you can follow him coding for almost one hour, which can be easier for beginners.



# Preprocessing

This part of our project is not the most thrilling so we will not go over every detail of the preprocessing but only mention a few ones that could maybe help the reader to gain a better global comprehension of the project. Please refer to **[my project notebook](https://github.com/clairebilat/facebook-GDPR)** if you have an insatiable curiosity about it.

It may not be the most thrilling part but it definitely was the most painful. ome of our columns have nested sub-columns in each row that are still in JSON format. 




### Correlation

The **corr** function gives the Pearson Coefficient between the `CrimeScores` and the `Community Areas`.

{% include Corr_crime.html %}


**The CrimeScore appears to be very related to the place.**

---

# Prospects

Analyse de language dans les messages
