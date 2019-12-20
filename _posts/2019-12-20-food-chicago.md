---
layout: post
title: Eat safely in Chicago
subtitle: A short data analysis of the Chicago Food Inspections Database
gh-repo: clairebilat/forensic-data-stories
gh-badge: [star, follow]
tags: [crime, food, chicago]
comments: true
---

# 1. Introduction

## 1.1 About us

We are four students decided to complete a [master's degree in Digital Investigation and Identification](https://www.unil.ch/esc/fr/home/menuinst/enseignement/masters/msc-investigation-numerique.html) at University of Lausanne. As part of this, we found ourselves trying to make a success of an EPFL course intituled "Applied Data Analysis". We were asked to developp a project under the theme *data science for social good*. A variety of datasets were provided by the course's organisators including the [Chicago Food Inspections Database](http://dev.cityofchicago.org/open%20data/data%20portal/2018/06/29/food-violations-changes.html), which we selected for our project. However, as forensic sciences students, we could not miss the opportunity to make everything about criminology, which ultimately led to this study. We indeed added a [database of the crimes in Chicago](https://www.kaggle.com/currie32/crimes-in-chicago) in order to analyse the correlation, for a given community area in Chicago, between the number of crimes committed and the hygiene of the food establishments (among other various things).

## 1.2 About the databases used

The first dataset that we used is the **Chicago Food Inspections Database** linked above and provided by the Chicago department of Public Health's Food Protection Program. It contains informations regarding the inspection reports of food establishments in Chicago from 2010 to the present. Some informations are directly linked to the establishments like their exact location, their type (restaurants, coffee shop, ...) or their license number. Some other informations document the inspections realized like their result (pass, fail, ...) or the violations noticed.

The second dataset used for this project is the **Crimes in Chicago Database** also linked above and provided by the Chicago Police Department's Citizen Law Enforcement Analysis and Reporting. It contains informations regarding the reported incidents of crime that occured in Chicago from 2001 to present, like the primary type of the crime (homicide, burglary...) or its anonymized location.

The third dataset used for this projet is the **[Chicago Business Licenses and Owners Database](https://www.kaggle.com/chicago/chicago-business-licenses-and-owners)** provided by the City of Chicago. It contains informations about the owners of establishments in Chicago and allowed us to link the food establishments of the first dataset to their respective owners.

The fourth and last dataset used for this project is the **[Geographic Boundaries of Community Areas in Chicago Database](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6)** provided by the City of Chicago. This dataset allowed us to link the food establishments of the first dataset to their respective community areas.

## 1.3 About this project

### 1.3.1 Research questions

The main research question was : **where to eat *safely* in Chicago ?**

The adjective `safely` has been chosen wisely because it has multiple meanings: you can eat in a `safe` way making sure that the establishment where you go respects particular **hygiene rules**, but also that the place is `safe` according to the **crime rate** of its district. That said, two scores has been computed per community area : their **hygiene score** based on the food inspections performed in the area and their **crime score** based on the incidents of crime reported in the area. More about the exact calculation of those two scores will be explained later. 

It has been decided that additionally to the **geographic component** of the analysis (based on the geographic delimitations of the community areas) a **temporal component** would be taken into account. Indeed, the field of restoration is known to be in a constant evolution : each year, many establishments are opening while other are closing or changing of owner - especially in big cities. This is why the different calculations and comparisons has been done by year. Also, the main research question (*where to eat* safely *in Chicago*) has been given based on the latest data, considering that it would be the most useful. 

It has also been decided to distribute the facility types into **facility groups** that fall into two main categories :
- The *private* establishments, where it is possible to eat a main course (for example, the places where you can only eat an ice cream    were deleted of our list).
- The *public* establishments like school cafeterias and hospitals.

More about the exact distribution of those facility groups will be explained later.

Some other research questions were added to the project :
- About the **hygiene score** :
  - Are their significant differences of hygiene scores between the community areas ?
  - How is the evolution over time ?
  - Are their significant differences of hygiene scores between the *private* and the *public* establishments ?
  
- About the **management** of food establishments :
  - Is their a relation between the number of establishments that an owner has and the hygiene scores obtained ?
  - In which way a change of owner changes the hygiene score of an establishment ?
 
### 1.3.2 Limits

An important point is to pay attention to the *number of inspected establishments* compared to *the total number of establishments*. It is certain than the variations of this ratio between the community areas has an impact on the results. An explanation of the variations should be purposed. In order to give a complete answer to the main research question, the uninspected establishments have to be taken into account.

# 2. Preprocessing

This part of our project is not the most thrilling so we will not go over every detail of the preprocessing but only mention a few ones that could maybe help the reader to gain a better global comprehension of the project. Please refer to **[our project notebook](https://github.com/clairebilat/ada-2019-project-lost-and-found)** if you have an insatiable curiosity about it.

## 2.1 The Chicago Food Inspections Database

### 2.1.1 The `Facility group`

The Database contains informations about the facility type of the establishments inspected but there were too many different types of facility for the purpose of our project. As explained before, we created two main categories, *private* and *public* establishments, containing a few costum **facility groups** into which the facility types of interest are distributed. Those facility groups are listed below.

- *private* facility groups :
    - restaurant
    - grocery restaurant
    - banquet
    - rooftop restaurant
    - bar restaurant
    - bakery restaurant
    - liquor restaurant
    - catering
    - golden diner
    
 - *public* facility groups :
     - day care
     - school
     - childrens services
     - adulte care
     
### 2.1.2 The `Hygiene score`

In order to compute the **hygiene score** of a community area, we first computed the hygiene score of an inspection. To do so, we took into account the inspection's result and the number of violations detected during the inspection. There is three main possible outcomes of an inspection : either the facility **passes** the inspection or it **passes with conditions** or it **fails**. We attributed an arbitrary score to each of those outcomes :
- **Pass** = 1
- **Pass with conditions** = 2
- **Fail** = 3

The formula used to compute the hygiene score of an inspection is the following :

![img]([img]http://www.sciweavers.org/tex2img.php?eq=NumberViolations%20%2B%20InspectionResult%5E3%0A&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0[/img]){: .center-block :}


## 2.2 The Crimes in Chicago Database


