# Eat safely in Chigago : A short data analysis of the Chicago Food Inspections Database

A nice data story helping to visualize the results of our project can be found there :

https://clairebilat.github.io/forensic-data-stories/2019-12-20-food-chicago/

The preprocessing and analysis performed can be found in the notebook of the following project (Milestone-3.ipynb):

https://github.com/clairebilat/ada-2019-project-lost-and-found

# Abstract
The Chicago department of Public Health’s Food Protection Program provides a database containing the information about inspections' reports of restaurants and other food establishments in Chicago from 2010 to the present. It contains many information about the establishments, like their type (groceries’ stores, restaurants, coffee shop, …) and their locations. There is also many information about the violations listed in the database, like their description and their causes and the reason that led to the inspection.

In our project we endeavor to visualize the healthiness of public food establishments according to their type of facility, their ward and the date of the inspection. An analysis of the violations’ types according to these three parameters will also be conducted. The impact of two other factors on the healthiness of food facilities in Chicago will be analyzed : first the correlation between the owner of an establishment and its healthiness will be studied ; we want to know if all establishements owned by an unhealthy owner are unhealthy or if those two factors are not correlated. Then we want to study the correlation between the healthiness of the establishments in Chicago and crime (according to the amount and gravity of crime in each ward).  

The purpose of the project is to help the consumer to easily choose where to eat in Chicago and to provide them an interactive and intuitive way to browse the different places offered to them. Also, it could help the Chicago department of Public Health’s Food Protection Program to adapt their methods relying on the situation described by the findings of the analysis (for example, if a prevention program should be proposed for a specific area or type of facility).

# Research questions
 
 The principal questions we'll answer are : 
 
    - Which wards of Chicago are the most healthy/unhealthy ? 
    - Which types of facilities tend to be less healthy ? 
    - Are the 'public' facilities (schools or hospitals) healthier than the 'privat' ones (restaurants) ?
    - Did the healthiness of the food in Chicago increase or decrease from 2010 until now ?
    - Do all establishments owned by the same person tend to have the same level of healthiness ?
    - Is the level of crime of an area correlated with the healthiness of the food in the same area ?

# Dataset

The first dataset that we used is the **[Chicago Food Inspections Database](http://dev.cityofchicago.org/open%20data/data%20portal/2018/06/29/food-violations-changes.html)** provided by the Chicago department of Public Health's Food Protection Program. It contains informations regarding the inspection reports of food establishments in Chicago from 2010 to the present. Some informations are directly linked to the establishments like their exact location, their type (restaurants, coffee shop, ...) or their license number. Some other informations document the inspections realized like their result (pass, fail, ...) or the violations noticed.

The second dataset used for this project is the **[Crimes in Chicago Database](https://www.kaggle.com/currie32/crimes-in-chicago)** provided by the Chicago Police Department's Citizen Law Enforcement Analysis and Reporting. It contains informations regarding the reported incidents of crime that occured in Chicago from 2001 to present, like the primary type of the crime (homicide, burglary...) or its anonymized location.

The third dataset used for this projet is the **[Chicago Business Licenses and Owners Database](https://www.kaggle.com/chicago/chicago-business-licenses-and-owners)** provided by the City of Chicago. It contains informations about the owners of establishments in Chicago and allowed us to link the food establishments of the first dataset to their respective owners.

The fourth and last dataset used for this project is the **[Geographic Boundaries of Community Areas in Chicago Database](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6)** provided by the City of Chicago. This dataset allowed us to link the food establishments of the first dataset to their respective community areas.
# Prospect

Analyzing other elements that can have an impact on the healthiness of food facilities in Chicago : the quality of life in different wards (or community area), the tourism repartition in Chicago,...

# Beautiful Jekyll

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.me/daattali/20)
[![Gem Version](https://badge.fury.io/rb/beautiful-jekyll-theme.svg)](https://badge.fury.io/rb/beautiful-jekyll-theme)

> *Copyright 2019 [Dean Attali](https://deanattali.com)*

**Beautiful Jekyll** is a ready-to-use template to help you create an awesome website quickly. Perfect for personal sites, blogs, or simple project websites.  [Check out a demo](https://deanattali.com/beautiful-jekyll) of what you'll get after just two minutes.  You can also look at [my personal website](https://deanattali.com) to see it in use, or see examples of websites other people created using this theme [here](#showcased-users-success-stories).

**If you enjoy this theme, please consider [supporting me](https://www.paypal.me/daattali/20) for developing and maintaining this template.**

<p align="center">
  <a href="https://www.paypal.me/daattali">
    <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" />
  </a>
</p>


## Showcased users (success stories!)

To my huge surprise, Beautiful Jekyll has been used in over 500 websites in its first 6 months alone! Here is a hand-picked selection of some websites that use Beautiful Jekyll.

Want your website featured here? [Contact me](https://deanattali.com/aboutme#contact) to let me know about your website.

### Project/company websites

| Website | Description |
| :------ |:----------- |
| [repidemicsconsortium.org/](https://www.repidemicsconsortium.org/) | R Epidemics Consortium |
| [vaccineimpact.org](https://www.vaccineimpact.org/) | Vaccine Impact Modelling Consortium |
| [derekogle.com/fishR](http://derekogle.com/fishR/) | Using R for Fisheries Analyses |
| [bigdata.juju.solutions](http://bigdata.juju.solutions) | Creating Big Data solutions Juju Solutions |
| [joecks.github.io/clipboard-actions](http://joecks.github.io/clipboard-actions/) | Clipboard Actions - an Android app |
| [deanattali.com/shinyjs](http://deanattali.com/shinyjs/) | shinyjs - an R package |
| [blabel.github.io](http://blabel.github.io) | Library for canonicalising blank node labels in RDF graphs |
| [reactionic.github.io](http://reactionic.github.io) | Create iOS and Android apps with React and Ionic |
| [ja2-stracciatella.github.io](http://ja2-stracciatella.github.io) | Jagged Alliance 2 Stracciatella |
| [ddocent.com](http://ddocent.com/) | RADSeq Bioinformatics and Beyond |
| [guitarlessons.org](https://www.guitarlessons.org/) | Free online guitar lessons for all |
| [terremotocentroitalia.info](https://www.terremotocentroitalia.info/) | Information about the 2016 Italy earthquake |


### Personal websites

| Website | Who | What |
| :------ |:--- | :--- |
| [deanattali.com](https://deanattali.com) | Dean Attali | Creator of Beautiful Jekyll |
| [ouzor.github.io](http://ouzor.github.io) | Juuso Parkkinen | Data scientist |
| [derekogle.com](http://derekogle.com/) | Derek Ogle | Professor of Mathematical Sciences and Natural Resources |
| [melyanna.github.io](http://melyanna.github.io/) | Melyanna | Shows off her nice art |
| [chauff.github.io](http://chauff.github.io/) | Claudia Hauff | Professor at Delft University of Technology |
| [kootenpv.github.io](http://kootenpv.github.io/) | Pascal van Kooten | Data analytics |
| [sjackman.ca](http://sjackman.ca) | Shaun Jackman | PhD candidate in bioinformatics |
| [anudit.in](http://www.anudit.in/) | Anudit Verma | Engineering student |
| [sharepointoscar.github.io](http://sharepointoscar.github.io) | Oscar Medina | Independent Hacker |
| [ocram85.com](https://ocram85.com) | Marco Blessing | A personal blog about PowerShell and automation |
| [khanna.cc](https://khanna.cc/) | Harry Khanna | Law and software |
