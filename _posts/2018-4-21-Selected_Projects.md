---
layout: post
title: Past Projects and Research
---

I spend a lot of my time learning and creating, and I'm trying to be better about documenting the process.
To that end, this post will be a summary of some projects I worked on with colleagues while I was in school and 
when I first began to teach.
<!--more-->


## Project 1: Activity Recognition

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


## Project 2: Cell Detection

This project uses supervised learning algorithms and graph-mining techniques to automatically count and detect embryonic cells as they grow.

Cell detection and counting in the context of biology research is largely a labor-intensive, manual task. A reliable count is of paramount importance as it is often a fundamental step in various growth studies; most commonly in embryonic or cancer cell growth analysis. In this project, we studied the efficacy of SVM and graph-mining algorithms to automatically detect and count embryonic stem cells in fluorescent microscopy images. You can read about the detailed results, [in this paper]({{ site.url }}/assets/embryonic_stem_cells.pdf).

<p align="center"> 
<img src="/assets/cell_detection_svm.png">
</p>

The graph-mining approach was very interesting because it relied on constructing a graph that separated individual cells based on patterns of intensity in a given image. A cell nucleus was very bright, but its edges and the background were darker. So by identifying areas of brightness, after eliminating spurious connections between cells and trying to account for overlap, graph-mining worked well.


## Project 3: Depth Estimation

This project uses pairs of photos taken by an endoscope at slightly different depths and a SIFT algorithm to estimate the depth map for an area of interest.

<p align="center"> 
<img src="/assets/depth_map.png">
</p>

SIFT was used to create feature descriptors for two endoscopic images, taken at different depths. Using the SIFT descriptors, we identified the best-matching points in the pair of images and used those to calculate a transformation between the two images. From this transformation we extracted an estimation for the distance between the end of the endoscope and the objects in the images.


## Project 4: DNA-Based Logic Gates

In my research as an undergraduate, I studied the construction of and uses cases for DNA-based logic gates. These gates operate in the same way as traditional logic gates: producing an output signal, given an input. The flow of a simple gate is pictured below, where A and A* are complimentary strands of DNA.


<p align="center"> 
<img src="/assets/dna_gate2.png">
</p>

## Project 5: DNA-Mediated Lithography

I recorded a [short, Vimeo video](https://vimeo.com/112122612) on lithography done in part by DNA-mediated etching of SiO2.



