---
layout: post
title: Past Projects and Research
---

I spend a lot of my time learning and creating, and I'm trying to be better about documenting the process.
To that end, this post will be a summary of some projects I worked on with colleagues while I was in school and 
when I first began to teach.
<!--more-->


### Project 1: Activity Recognition

Using physiological data collected by wearable technology, such as the acceleration and heat flux of a person's body, 
this project intelligently characterizes the activity a user performed.

Wearable sensor technology has been investigated as a way to regularly monitor a person's health from
watches that track your heart rate during exercise, to wearable devices that use accelerometer data to
check if someone has fallen or not. In this project, we use data, collected by wearable devices, to
classify a person's activity into one of three classes: sleeping, watching TV, and all other activities.

This follows the guidelines of the Physiological Data Modeling Contest (PDMC) contest, and you can
read more about this data and the challenge in [the project paper]({{ site.url }}/assets/activity_recognition.pdf).

To approach this challenge, we compared unsupervised learning algorithms with supervised approaches. 
The thinking was: a supervised algorithm might be the most accurate, but a good, unsupervised algorithm 
would be ideal, since it takes a while to create richly-labeled data for training.

<p align="center"> 
<img src="/assets/activity_rec.png">
</p>

In the image above, you can see an example of data separation done with linear discriminant analysis (LDA).
LDA reduces the feature dimension; the features are the different types of collected sensor data 
like age, acceleration, heat flux, and body temperature. So, for several features, LDA squashes them into 2D space, 
which is how we can visualize these class groupings. Then it separates data points based on the reduced feature space, 
and it models the difference between the three classes.

We did get the best performance using supervised algorithms, but this project did get me thinking about  
how unsupervised approaches might be improved.