---
layout: post
title: Introduction to Neural Networks
---

How and why do neural networks work?
The first in a series about understanding how neural networks learn to separate and classify visual data. 
<p align="center">
<video controls="controls" width="500" height="300" 
name="Video Name" src="/assets/intro_nn/neuron_inout.mov"></video>
</p>

<!--more-->


---

## What Are Neural Networks?

Neural networks are made up of neurons, sometime called nodes. One neuron is responsible for processing some input data and producing an output. This is modeled after the neurons in our brain, which process input signals and produce output signals. For a neural network that processes visual data, such as a set of images, these inputs will be either spatial information or color information. When these color components or shapes are combined, which happens inside a neuron in the form of an equation (ex. 0.5\*red and 0.5\*blue = 1\*purple), it produces an output signal that can do something like help classify the initial input!

<p align="center"> 
<img src="/assets/intro_nn/simple_nodes.png" alt="Images of shapes and colors that make up a handwritten 6 and the color purple, respectively." width="500" height="300" >
</p>

By looking at many many combinations of both shapes and colors, a neural network can recognize more and more complex patterns in images. You'll often see neural networks represented by figures like these:

<p align="center"> 
<img src="/assets/intro_nn/nn_example.png" alt="Two images of layers that make up neural networks." >
</p>

These neural nets have some input data and some output, and in between they have many layers. The layers are made of nodes and the output of one node acts as the input of another node down the line; each of these nodes can *learn* to extract information about the colors and shapes that make up an image, and use a combination of those things to produce something like a class for an input image.


---

## Why Do Neural Networks Work?

Now, why exactly do neural networks work? This wasn’t exactly clear to me when I first started learning about them, and it doesn't help that NN's' are often described as “black boxes” or some kind of “magic,” but *why* they work can be concisely explained. 

> 1. Any set of data, such as a set of images, can be represented by a smaller, simpler **model**.
> 2. A model is made of a combination of visual **features**: a few colors and/or shapes.

The idea is that *if* a set of image data can be broken down into a finite set of shape and color features, then we can learn how to group and classify any image based on which of these features it contains! The big assumption here is that any set of data can be represented by a smaller model. This is true of any set of data with one exception. The only case where a set of data cannot be broken down in to a simpler mode is in the case of random data; for any other kind of data there will be some pattern that can be detected.


---

## Classifying Colors

Let’s see how creating a model works by building one ourselves and creating a model for color classification.

<p align="center"> 
<img src="/assets/intro_nn/rainbow_classes.png" alt="Rainbow colors." width="500" height="300" >
</p>

Say, we are given the rainbow above as training data and this corresponding, discrete list of color classes. We want to create a model that will correctlty classify all of these given colors *and* which will be able to classify any new colors that we may see into one of these classes.

I’m going to start by looking at a smaller set of colors, as an example, red, blue, and purple.

<p align="center">  
<img src="/assets/intro_nn/red_blue.png" alt="Red, blue, and purple."  width="500" height="200" >
</p>

We know that purple is a combination of red and blue and so, I can plot each of these colors on an axis that has red on one axis and blue on the other. A purely red color will fall on the red axis, and purely blue will fall only on the blue axis.

<p align="center">  
<img src="/assets/intro_nn/red_blue_axis.png" alt="Red and blue color plot."  width="200" height="200" >
</p>

Any color that falls somewhere on this graph has some red component and some blue component, and we can classify any new color that we see by looking at our discrete class options and seeing which of those options best describes that new color.

<p align="center">  
<img src="/assets/intro_nn/new_color.png" alt="Classifying a new color as red."  width="500" height="200" >
</p>

Each new color that we see, should fall into one of our three color classes. In sorting the above pink-ish color into the red class, I’ve implied that I have some idea of what qualities separate the three color classes. In my head, I've actually constructed some thresholds. In the image below, the red and blue axes represent a measure of color strength; how strong the red and blue components of a color are. Strength is a numerical value with a range from 0-1, where 0 is the lowest and 1 is the highest saturation of a color. The thresholds I’ve thought of are at the half-strength mark. For example, any color with more that 0.5 strength for red and *less* than 0.5 strength for blue is going to be classified as red.

<p align="center">  
<img src="/assets/intro_nn/strength_threshold.png" alt="Red and blue threshold lines."  width="500" height="200" >
</p>

What I’ve done here is to define threshold lines that look at the levels of red and blue in a color and then, for any given color, I classify it into one of three color classes based on where it falls on either side of these lines! So, the pinkish color that you saw earlier, would fall into the red classification area. One thing to note is that I’ve chosen these threshold lines based on what looks reasonable to my eye, but the job of a neural network is to *learn* the best threshold lines; maybe a network would learn that red can be captured by a lower threshold.

Keeping these 0.5 strength thresholds in mind, we can write these class-defining thresholds down and make a complete classification model for these colors! Notice that each of the three color classes is defined by only two colors: red and blue, and these are the smaller set of features that make up our color classification model.

<p align="center">  
<img src="/assets/intro_nn/red_blue_threshold_list.png" alt="Red, blue, and purple defining thresholds."  width="500" height="300" >
</p>




---

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/cezannecam) or connect with me on [LinkedIn](https://www.linkedin.com/in/cezanne-camacho-422823b2/).


