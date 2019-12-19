---
layout: post
title: Eat safely in Chicago
subtitle: A short data analysis of the Chicago Food Inspections Database
gh-repo: clairebilat/forensic-data-stories
gh-badge: [star, follow]
tags: [crime, food, chicago]
comments: true
---

# Introduction

## About this project

We are four students decided to complete a [master's degree in Digital Investigation and Identification](https://www.unil.ch/esc/fr/home/menuinst/enseignement/masters/msc-investigation-numerique.html) at University of Lausanne. As part of this, we found ourselves trying to make a success of an EPFL course intituled "Applied Data Analysis". We were asked to developp a project under the theme *data science for social good*. A variety of datasets were provided by the course's organisators including the [Chicago Food Inspections Database](http://dev.cityofchicago.org/open%20data/data%20portal/2018/06/29/food-violations-changes.html), which we selected for our project. However, as forensic sciences students, we could not miss the opportunity to make everything about criminology, which ultimately led to this study. We indeed added a [database of the crimes in Chicago](https://www.kaggle.com/currie32/crimes-in-chicago) in order to analyse the correlation, for a given community area in Chicago, between the number of crimes committed and the hygiene of the food establishments (among other various things).

## About the databases used

The first dataset that we used is the Chicago Food Inspections Database linked above and provided by the Chicago department of Public Health's Food Protection Program. It contains informations regarding the inspection reports of food establishments in Chicago from 2010 to the present. Some informations are directly linked to the establishments like their exact location, their type (restaurants, coffee shop, ...) or their license number. Some other informations document the inspections realized like their result (pass, fail, ...) or the violations noticed.

The second dataset used for this project is the Crimes in Chicago Database also linked above and provided by the Chicago Police Department's Citizen Law Enforcement Analysis and Reporting. It contains informations regarding the reported incidents of crime that occured in Chicago from 2001 to present, like the primary type of the crime (homicide, burglary...) or its anonymized location.

The third 

**Here is some bold text**

## Here is a secondary heading

Here's a useless table:

| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |

test3

<div>
  <iframe src="https://github.com/clairebilat/forensic-data-stories/blob/master/frames/timtest.html"></iframe>
</div>

How about a yummy crepe?

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg)

It can also be centered!

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg){: .center-block :}

Here's a code chunk:

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
