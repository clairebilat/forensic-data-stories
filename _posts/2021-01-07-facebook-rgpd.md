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

# Litterature review (or how what I wanted to do had already be done but I did it anyway)

Many people have done similar projects (but it is a real pain trying to find them online because of all the Facebook scandals that pops when searching form terms like _Facebook data analysis_... Quick tip, try with keywords like "Analyze Your Personal Facebook Data" and exclude some keywords like "Analytics" and it will be a little bit better).

1. [How much do you post](https://www.dataquest.io/blog/analyze-facebook-data-python/)
    
    This is a great tutorial that is surprisingly easy to follow, explaining in well illustrated steps how to plot your monthly post count. It takes five minutes to perform and is a really great way to introduce you to the structure of the data Facebook offers.
    
2. [Natural Language Processing](https://towardsdatascience.com/mapping-my-facebook-data-part-1-simple-nlp-98ce41f7f27d)
    
    This article explains how to discover what words you use most, words count, and basic stats about your data. It is out of the scope of my project but is 100% considered as prospect.
    
3. [Facebook Messenger Data](https://www.youtube.com/watch?v=z9W2cvmFPuA)
    
    This livestream replay is a video tutorial on how to explore your Facebook Messenger in order to compare the friends you contacted most and at which frequency. What is nice is that you can follow him coding for almost one hour, which can be easier for beginners.
    
4. [MOOC course](https://www.mooc-list.com/course/analyzing-your-facebook-data-python-leada)
    
    This MOOC course is supposed to guide you through analyzing your Facebook data, but was not available at the time I tried to enroll.

# Preprocessing

This part of my project is not the most thrilling so I will not go over every detail of the preprocessing but only mention a few ones that could maybe help the reader to gain a better global comprehension of the project. Please refer to **[my Python script](https://github.com/clairebilat/facebook-GDPR)** if you have an insatiable curiosity about it.

This step definitely was the most painful. First, **there is no official documentation available about the organization of the Facebook download data**, and you just have to deduce it by looking at what you have in front of you. To this day, there are still files which I have not been able to extrapolate the meaning of the data they contain. But as you think you have a good idea of what the data represent and you want to use it, you will face the next problem. Indeed, every folder that the Facebook download data contains shows a different structure and it is **mostly nested sub-columns in each row** that are still in JSON format. In consequence, I had to manually review each folder individually and study its structure to extract some useful content, and that has not been automated. 
Also, the **Facebook download data is incorrecly encoded**. The original data is UTF-8 encoded but was decoded as Latin-1 (no, it's not just me going crazy, [stackoverflow talks about it](https://stackoverflow.com/questions/50008296/facebook-json-badly-encoded)), which I had to take into account each time I wanted to interpret textual values.
Last but not least, **the data is not well tokenized** and most of them are just strings describing the action resulting in this entry. As an example, I can cite the file containing informations about group memmbership activity (search for the file `groups/your_group_membership_activity.json`). The entries it contains can be two of the following strings :

1. "You became member of group _xy_" 
    
    (in French "Vous êtes devenue membre de _xy_").
2. "You stopped being member of group _xy_" 
    
    (in French "Vous avez arrêté d'être membre de _xy_").

There are three problems with that :

1. You have to manually check every type of entry in the file and apply some regular expressions searches in order to identifiy exactly the action corresponding to the entry ("quit" or "joined").
2. It is langage-dependent, as the entry is expressed in the langage chosen by the user at the time.
3. Depending on the langage (and it is the case in French), it is even gender-dependent, so the string will not be the same depending on the individual settings of the user.

It becomes worse (and almost is a joke at this point), as **the string itself changes over time depending on the version of Facebook** and the conventions they are applying at the time, an example being the entries in the file recording the correspondences with Facebook Support, where I found two possible strings describing the anonymous signaling of a publication :

1. "You have anonymously signaled the publication of _xy_ for _abc_ reasons
    
    (in French "Vous avez signalé anonymement la publication de _xy_ pour _abc_).
2. "You have signaled the publication of _xy_ in an anonymous way for _abc_ reasons
    
    (in French "Vous avez signalé la publication de _xy_ de manière anonyme pour _abc_).

In consequence, the regular expressions used have to be realy robust in order to work on every string version of the action one is trying to tokenize.

To conclude, the high variability of formats encountered in the Facebook download data makes it difficult to dig deep in an automated way and must be adapted case-by-case to achieve a high granularity of details. The purpose here being to offer a general understanding of the activity one has on Facebook, I have decided to not loose myself in the gestion of every case I ran into, and did not implement any regular expressions, as it too tightly depends on the account settings of the investigated Facebook user. 

# Dataframes created



# Results

The **corr** function gives the Pearson Coefficient between the `CrimeScores` and the `Community Areas`.

{% include month_count_actions_1-std-10.html %}

{% include month_count_actions_10-std.html %}

{% include inbox_conv_anonymized.html %}

{% include inbox_group_anonymized.html %}



---

# Prospects

Analyse de language dans les messages
Attention genre poke est pas une fonction qui a tjrs existé
Utilisateur de Facebook est pas un vrai profil
Par personne avec + de df genre les commentaires et tout
par semaine au lieu de par mois
encodage du texte latin1 utf8
nested structures
