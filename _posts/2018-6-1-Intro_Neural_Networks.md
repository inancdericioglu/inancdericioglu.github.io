---
layout: post
title: Introduction to Neural Networks
---

How and why do neural networks work?

The first in a series about understanding how neural networks learn to separate and classify visual data. 

<p align="center">
<video controls="controls" width="400" height="300" 
name="Video Name" src="/assets/intro_nn/neuron.mov"></video>
</p>

<!--more-->

---

## What Are Neural Networks?

Neural networks are made up of neurons, sometime called nodes. One neuron is responsible for processing some input data and producing an output. This is modeled after the neurons in our brain, which process input signals and produce output signals. For a neural network that processes visual data, such as a set of images, these inputs will be either spatial information or color information. When these color components or shapes are combined, which happens inside a neuron in the form of an equation (ex. 0.5*red and 0.5*blue = 1*purple), it produces an output signal that can do something like help classify the initial input!

<p align="center"> 
<img src="/assets/intro_nn/simple_nodes.png" alt="Images of shapes and colors that make up a handwritten 6 and the color purple, respectively." >
</p>

By looking at many many combinations of both shapes and colors, a neural network can recognize more and more complex patterns in images. You'll often see neural networks represented by figures like these:

<p align="center"> 
<img src="/assets/intro_nn/nn_example.png" alt="Two images of layers that make up neural networks." >
</p>

These neural nets have some input data and some output, and in between they have many layers. The layers are made of nodes and the output of one node acts as the input of another node down the line; each of these nodes can actually *learn* to extract information about the colors and shapes that make up an image, and use a combination of those things to produce something like a class for an input image.


---

## Why Do Neural Networks Work?




---

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/cezannecam) or connect with me on [LinkedIn](https://www.linkedin.com/in/cezanne-camacho-422823b2/).


