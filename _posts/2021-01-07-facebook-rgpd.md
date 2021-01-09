---
layout: post
title: Facebook GDPR Timeline in a criminal investigation
subtitle: A small processing and visualization of Facebook-GDPR Database
gh-repo: clairebilat/forensic-data-stories
gh-badge: [star, follow]
tags: [Facebook, GDPR, timeline]
comments: true
---

# Prologue

The GDPR law (General Data Protection Regulation) is "a regulation in EU law on data protection and privacy in the European Union and the European Economic Area. The GDPR's primary aim is to give individuals control over their personal data (...). Data subjects have the right to request a portable copy of the data collected by a controller in a common format, and the right to have their data erased under certain circumstances." [Wikipedia](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation)

It is in this context that Facebook makes available all the data collected on a user via the interface of his account settings, and it is this data that I decided to analyze.

## About me

I am a student who decided to complete a [master's degree in Digital Investigation and Identification](https://www.unil.ch/esc/fr/home/menuinst/enseignement/masters/msc-investigation-numerique.html) at the University of Lausanne. As part of this, I had to choose a personal practical lab theme for which I would take time to practice my theoretical knowledge, produce something useful, and maybe publish my results. After the success my colleagues and I had with our _Eat safely in Chicago_ project performed as part of the EPFL course intituled "Applied Data Analysis" (you will find our amazing results in [the first post of this blog](https://clairebilat.github.io/forensic-data-stories/2019-12-20-food-chicago/)), I could not refrain myself to make everything about data analysis once again. Recently out of an internship in an Office of Police where I found myself having to review manually some Facebook profiles, I chose to try and write a script automating the processing and output of some basic visualizations of Facebook GDPR data to help investigators grab a general idea of one's Facebook profile and its content without having to put too much work into it. 

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
    
4. Go to `Download your information`.
    
    <img src="{{site.github.url}}/assets/img/tuto5.PNG">
    
5. Choose `Request copy`, adjust your parameters (I personally chose the JSON format with a low quality of media), and click on `Create File`.
    
    <img src="{{site.github.url}}/assets/img/tuto6.PNG">
    

## About the purpose of this project


The purpose here is to write a script automating the processing and output of some basic visualizations of Facebook GDPR data to help investigators grab a general idea of one's Facebook profile and its content without having to put too much work into it. That way, they can have leads about which people are the most involved in the Facebook activity of the user, and to which extent the user is active on Facebook. That information can be used to orient the investigation and help prioritize the actions taken.


# Litterature review (or how what I wanted to do had already be done but I did it anyway)

Many people have done similar projects (but it is a real pain trying to find them online because of all the Facebook scandals that pop when searching form terms like _Facebook data analysis_... Quick tip, try with keywords like "Analyze Your Personal Facebook Data" and exclude some keywords like "Analytics" and it will be a little bit better).

1. [How much do you post](https://www.dataquest.io/blog/analyze-facebook-data-python/)
    
    This is a great tutorial that is surprisingly easy to follow, explaining in well-illustrated steps how to plot your monthly post count. It takes five minutes to perform and is a really great way to introduce you to the structure of the data Facebook offers.
    
2. [Natural Language Processing](https://towardsdatascience.com/mapping-my-facebook-data-part-1-simple-nlp-98ce41f7f27d)
    
    This article explains how to discover what words you use most, and basic stats about your data. It is out of the scope of my project but is 100% considered as a prospect.
    
3. [Facebook Messenger Data](https://www.youtube.com/watch?v=z9W2cvmFPuA)
    
    This live stream replay is a video tutorial on how to explore your Facebook Messenger to compare the friends you contacted most and at which frequency. What is nice is that you can follow him coding for almost one hour, which can be easier for beginners.
    
4. [MOOC course](https://www.mooc-list.com/course/analyzing-your-facebook-data-python-leada)
    
    This MOOC course is supposed to guide you through analyzing your Facebook data but was not available at the time I tried to enroll.

# Preprocessing

This part of my project is not the most thrilling so I will not go over every detail of the preprocessing but only mention a few ones that could maybe help the reader to gain a better global comprehension of the project. Please refer to **[my Python script](https://github.com/clairebilat/facebook-GDPR)** if you have an insatiable curiosity about it.

This step definitely was the most painful. First, **there is no official documentation available about the organization of the Facebook download data**, and you just have to deduce it by looking at what you have in front of you. To this day, there are still some files for which I could not extrapolate the meaning of the data they contain. And then, as you think you have a good idea of what the data represents and you want to use it, you will face the next problem. Indeed, every folder that the Facebook download data contains shows a different structure and it is **mostly nested sub-columns in each row** that are still in JSON format. In consequence, I had to manually review each folder individually and study its structure to extract some useful content, and that has not been automated. 
Also, the **Facebook download data is incorrectly encoded**. The original data is UTF-8 encoded but was decoded as Latin-1 (no, it's not just me going crazy, [stackoverflow talks about it](https://stackoverflow.com/questions/50008296/facebook-json-badly-encoded)), which I had to take into account each time I wanted to interpret textual values.
Last but not least, **the data is not well tokenized** and most of them are just strings describing the action resulting in this entry. As an example, I can cite the file containing information about group membership activity (search for the file `groups/your_group_membership_activity.json`). The entries it contains can be at least two of the following strings :

1. "You became a member of group _xy_" 
    
    (in French "Vous êtes devenue membre de _xy_").
    
2. "You stopped being a member of group _xy_" 
    
    (in French "Vous avez arrêté d'être membre de _xy_").

There are three problems with that :

1. You have to manually check every type of entry in the file and apply some regular expressions searches to identify exactly the action corresponding to the entry ("quit" or "joined").
2. It is language-dependent, as the entry is expressed in the language chosen by the user at the time.
3. Depending on the language (and it is the case in French), it is even gender-dependent, so the string will not be the same depending on the individual settings of the user.

It becomes worse (and almost is a joke at this point), as **the string itself changes over time depending on the version of Facebook** and the conventions they are applying at the time, an example being the entries in the file recording the correspondences with Facebook Support, where I found two possible strings describing the anonymous signaling of a publication :

1. "You have anonymously signaled the publication of _xy_ for _abc_ reasons"
    
    (in French "Vous avez signalé anonymement la publication de _xy_ pour _abc_").
    
2. "You have signaled the publication of _xy_ in an anonymous way for _abc_ reasons"
    
    (in French "Vous avez signalé la publication de _xy_ de manière anonyme pour _abc_").

In consequence, the regular expressions used have to be really robust in order to work on every string version of the action one is trying to tokenize.

To conclude, the high variability of formats encountered in the Facebook download data makes it difficult to dig deep in an automated way and must be adapted case-by-case to achieve a high granularity of details. The purpose here being to offer a general understanding of the activity one has on Facebook, I have decided to not lose myself in the management of every case I ran into and did not implement any regular expressions, as it too tightly depends on the account settings of the investigated Facebook user. 

# Results

To see your results, you first have to run my script (available [here](https://github.com/clairebilat/facebook-GDPR)). Just put the file `facebook_script.py` in the folder where you store each Facebook download data folder, open this destination in a terminal, make sure you have `python` and `pip` installed and that they are in the PATH environment variable. Then run the command `pip install pandas datetime plotly`. Lastly, you will just have to run the command `python ./facebook_script.py %folder_name%`, replacing %folder_name% by the name of the Facebook download data folder you want to analyze. The results will be stored in a newly created folder `%folder_name%_results`.

## Dataframes created

After cleaning the data I wanted to use, I saved them into Dataframes and then into `CSV` files. Each of those CSV files can be found in the results folder **if** the corresponding JSON file was available in the Facebook download data folder. Those CSV files and their content are described at the end of this article. Note that I chose to construct Dataframes from the JSON files that I identified as pertinent based on the four Facebook accounts I had at my disposal. It is not an exhaustive list of the information you can retrieve from the Facebook download data and should be adapted to your case.

Each Dataframe created was exploited to create a visualization of the monthly count of actions performed by the user, per type of action (see next section). Some of the Dataframes have also been individually exploited to create more detailed visualizations, for example the monthly count of exchanged messages in privates conversations, per interlocutor (also see next section).

Be careful to choose `65001: Unicode (UTF-8)` as "File origin" when opening the file with Excel, or the text will be displayed with encoding errors. To do so, follow these steps:

1. Open a clean data sheet in Excel.
    
2. Select the `Data` tab and click on `From a text file/CSV`.
    
    <img src="{{site.github.url}}/assets/img/excel1.PNG">
    
3. There, you can select the desired `File origin` and you are ready to go.
    
    <img src="{{site.github.url}}/assets/img/excel2.PNG">


## Vizualisations

To navigate those visualizations, you can zoom in or out to adapt the time range displayed, and you can click on the actions displayed at the right of the graph to select the ones you want to display.

### Monthly count of Facebook actions, per action (std between 1 and 10)

I chose to limit the visualization to the actions showing a standard deviation of monthly count between 1 and 10 so that the visual comparison would be easier. As those are the regular actions that are not performed on a daily basis by the user, it helps to gain a general understanding of the usage of the Facebook profile.

{% include month_count_actions_1-std-10.html %}

### Monthly count of Facebook actions, per action (std higher than 10)

Here are illustrated the actions showing a standard deviation of monthly count higher than 10. Those are the actions performed on a daily basis by the user, and any irregularities in them can be of interest.

{% include month_count_actions_10-std.html %}

Many observations can be made. As you can see when displaying the `msg_requests`action, I have a big peak of message requests in September 2018, and almost none the other months. I checked my inbox by curiosity, and it turns out that, in September 2018, people I did not know added me in a group conversation. Before I had the time to decline the invitation, they sent almost 500 messages in this conversation, and then deleted me from it. That explains this anomaly. When displaying `archived_threads`, you can see that I also have enormous peaks between June and September 2017 and almost nothing in the other months. During this period, I actually quit the associative role that I had since January 2017 and archived the conservations I had with my colleagues, also explaining this anomaly.


### Monthly count of exchanged messages in private conversations, per interlocutor (total count in top10 or one month count in top10)

Here are illustrated the monthly count of messages I exchanged in private conversations (meaning in conversations with only one other person than me). I chose to limit the interlocutors represented to the 10 with whom I exchanged the most messages in total, and/or the 10 with whom I exchanged the most messages in one month. I replaced the names of my interlocutors with numbers for obvious reasons.

{% include inbox_conv_anonymized.html %}

Please be careful to note that the user "Utilisateur de Facebook" in French (probably "Facebook user" in English) often appears in this graph but is only an aggregation of every conversation where the interlocutor deleted his profile, making his name unavailable. 

### Monthly count of exchanged messages in group conversations, per interlocutor (total count in top10 or one month count in top10)

The same has been performed for group conversations.

{% include inbox_group_anonymized.html %}

We can see that I have almost no group conversations, apart from the period of January to September 2017. Again, those conversations are related to the associative role I had at the time and explain this activity. 

### Monthly count of posted messages in groups, per group (total count in top10)

{% include groups_comment_anonymized.html %}

### Monthly count of searched items, per item (total count in top10 or one month in top10)

{% include searches_anon.html %}

What we can observe is for example the 9th searched term being regularly searched for a really long period of time.

---

# Prospects

Analyse de language dans les messages
Attention genre poke est pas une fonction qui a tjrs existé
Utilisateur de Facebook est pas un vrai profil
Par personne avec + de df genre les commentaires et tout
par semaine au lieu de par mois
encodage du texte latin1 utf8
nested structures

---


# Description of the `CSV` files created

1. `apps_and_websites`
    
    This Dataframe contains information about the apps that have been linked to the considered Facebook account. It has forensic value as it can orient the investigator to other sources of traces and potentially valuable information, and it should be manually reviewed.
    
2. `archived_threads`
    
    This Dataframe contains the group discussions that the user has left. It has not been used here for independent visualizations as my account did not have many different deleted group conversations, but if the general overview of the account activity shows that this Dataframe is highly populated, the script could be adapted to take that into account.
    
3. `comments_in_groups`
    
    This Dataframe contains every action (post or comment) the user performed in groups. The group name is already tokenized and has been exploited to produce a visualization of the monthly post/comment count per group (see next section). This can be used to see if the user is very active in some groups that could be related to specific activities (illegal sale, harassment, ...). 
    
4. `comments`
    
    This Dataframe contains every comment the user posted on profiles or pages. It has not been visualized as the action is not tokenized and neither the comment nor the page or the profile can easily be extracted.
    
5. `event_invitations`, `events_declined`, `events_interested`, `events_joined` and `events_visited`
    
    These Dataframes contain information about the events the user has been invited to, the ones he declined, the ones he expressed his interest in, the ones he joined, and the ones whose event page he visited. Those have forensic value to check if the user expressed interest in events planning illegal activities and should be manually reviewed by the investigator.
    
6. `filtered_threads`
    
    These Dataframe contains message requests that have been declined by the user. It has not been used here for independent visualizations as my account did not have many different deleted group conversations, but if the general overview of the account activity shows that this Dataframe is highly populated, the script could be adapted to take that into account.
    
7. `followed_pages`
    
    This Dataframe contains the pages that the user follows.
    
8. `following`
    
    This Dataframe contains the people that the user follows.
    
9. `friends`
    
    This Dataframe contains the user's friends.
     
10. `groups_joined`
    
    This Dataframe contains the groups in which the user has taken part. Be careful, if the user has left the group, only one entry remains in the Dataframe and the timestamp corresponds to the departure.
    
11. `groups_visited`
    
    This Dataframe contains the groups whose pages the user has displayed.
    
12. `inbox`
    
    This Dataframe contains the messages that the user exchanged in conversations. Two visualiztions have been made based on this Dataframe; one illustrating the monthly exchanged message count per group conversation and the other one per private conversations (see next section).
    
13. `liked_pages`
    
    This Dataframe contains information about the pages the user has liked. Those have forensic value to check if the user expressed interest in specific topics regarding the investigation and should be manually reviewed by the investigator.
    
14. `liked_posts_and_comments`
    This Dataframe contains every Facebook reaction (HAHA, LIKE, LOVE, WOW, etc.) the user selected on various posts. 
    
15. `msg_requests`
    
    This Dataframe contains every message sent as a request from people that were not on the user's friends list. 
    
16. `people`
    
    To be honest, I don't really know what represents this Dataframe...
    
17. `pokes`
    
    This Dataframe contains every poke exchanged by the user. Please note that `poking` is a functionality that did not exist on Facebook for very long and it can explain why the "poke activity" of a user suddenly stops.
    
18. `received_friend_requests`
    
    This Dataframe contains the friend requests the user received. Please note that once they have been accepted or denied, they are not present in this Dataframe anymore. The data represents therefore the pending requests.
    
19. `rejected_friend_requests`
    
    This Dataframe contains the friend requests the user rejected. 
    
20. `removed_friends`
    
    This Dataframe contains the friend the user removed. 
    
21. `search_history`
    
    This Dataframe contains every search performed by the Facebook user. I have exploited this to plot the monthly count of searches per typed text (see next section).
    
22. `sent_friend_requests`
    
    This Dataframe contains the friend requests the user sent. 
    
23. `support`
    
    This Dataframe contains every request the user made to Facebook support, including anonym denunciations of posts or comments. It has forensic value in some cases like online harassment and should be manually reviewed by the investigator.
    
24. `unfollowed_pages`
    
    This Dataframe contains every page the user unfollowed.
    
25. `visites_de_profil`
    
    To be honest, I don't really know what represents this Dataframe...
    
26. `visites_sur_la_page`
    
    To be honest, I don't really know what represents this Dataframe...
     
27. `voir_en_premier`
    
    This Dataframe contains every profile the user chose to see first in his feed. This could be of interest depending on the case and should be manually reviewed by the investigator.
    
28. `voir_moins`
    
    This Dataframe contains every profile the user chose to see last in his feed. This could be of interest depending on the case and should be manually reviewed by the investigator.
    
29. `your_pages`
    
    This Dataframe contains every page where the user is an administrator. That has high forensic value and should be manually reviewed by the investigator.
    
