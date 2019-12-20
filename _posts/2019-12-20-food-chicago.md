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

The first dataset that we used is the Chicago Food Inspections Database linked above and provided by the Chicago department of Public Health's Food Protection Program. It contains informations regarding the inspection reports of food establishments in Chicago from 2010 to the present. Some informations are directly linked to the establishments like their exact location, their type (restaurants, coffee shop, ...) or their license number. Some other informations document the inspections realized like their result (pass, fail, ...) or the violations noticed.

The second dataset used for this project is the Crimes in Chicago Database also linked above and provided by the Chicago Police Department's Citizen Law Enforcement Analysis and Reporting. It contains informations regarding the reported incidents of crime that occured in Chicago from 2001 to present, like the primary type of the crime (homicide, burglary...) or its anonymized location.

The third dataset used for this projet is the [Chicago Business Licenses and Owners Database](https://www.kaggle.com/chicago/chicago-business-licenses-and-owners) provided by the City of Chicago. It contains informations about the owners of establishments in Chicago and allowed us to link the food establishments of the first dataset to their respective owners.

The fourth and last dataset used for this project is the [Geographic Boundaries of Community Areas in Chicago Database](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6) provided by the City of Chicago. This dataset allowed us to link the food establishments of the first dataset to their respective community areas.

## 1.3 About this project

The main research question was : **where to eat safely in Chicago ?**



<div>
 <iframe src="https://github.com/clairebilat/forensic-data-stories/blob/master/frames/timtest2.html" name="test" width="500" height="300">
 </iframe>
</div>
