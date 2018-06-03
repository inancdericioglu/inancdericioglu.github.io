---
layout: post
title: Convolutional Neural Networks
---

Image classification is a challenging task for computers. Convolutional neural networks represent one data-driven approach to this challenge. This post will be about image representation and the layers that make up a convolutional neural network. 
<p align="center">
<img src="/assets/cnn_intro/CNN_ex.png" alt="A CNN that sees an image of a car and outputs a class." width="600" >
</p>

<!--more-->


---

## Neural Network Structure

This post is the second in a series about understanding how neural networks learn to separate and classify visual data. In the last post, I went over why neural networks work: they rely on the fact that most data can be represented by a smaller, simpler set of features. Neural networks are made of many nodes that learn how to best separate training data into classes, or other specified groups, and many layers of nodes can create more and more complex boundaries for separating and grouping this data.

<p align="center">  
<img src="/assets/intro_nn/complete_nn.png" alt="Complete neural network."  width="500" >
</p>


---

## Image Classification

In the case of image classification, we want a neural network that looks at an image and outputs the correct class for that image. Let's take an image of a car as an example.

<p align="center">  
<img src="/assets/cnn_intro/image_classification.png" alt="Image classification pipeline."  width="500" >
</p>

It's simple for us to look at this image and identify the car, but when we give a neural network this image, what does it see? 

### Images as Grids of Pixels

An image is seen by a neural network (and by computers) as a grid of numerical values. Below, you'll see a zoomed in portion of a grayscale image of a car. The image is broken up into a fine grid, and each of the grid cells is called a pixel. For grayscale images, each pixel has a value between 0 and 255, where 0 is black and 255 is white; shades of gray are anywhere in between.

<p align="center">  
<img src="/assets/cnn_intro/grayscale_image.png" alt="Grayscale pixel values 0-255."  width="400" >
</p>

For a standard color image, there are red, green, and blue pixel values for each (x,y) pixel location. We can think of this as a stack of three images, one for each of the red, green, and blue color components. You may see a color pixel value written as a list of three numerical values. For example, for an RGB pixel value,  `[255,0,0]` is pure red and `[200,0,200]` is purple. In this way, we can think of any image as a 3D volume with some width, height, *and* color depth. Grayscale images have a color depth of 1.

<p align="center">  
<img src="/assets/cnn_intro/color_image.png" alt="Color image in x-y space, with a depth of 3 for 3 RGB color channels."  width="600" >
</p>

To creat an image classifier, we need an algorithm that can look at these pixel values and classify this image as a car. We also want a classifier to be able to detect this car under varying ight conditions (at night or during a sunny day), and we want the classifier to generalize well, so that it can recognize a variety of cars in different environments and in different poses.

<p align="center">  
<img src="/assets/cnn_intro/var_cars.png" alt="Variety of images of a car in different scenarios."  width="600" >
</p>

If you look at just a small sample of car images, you can see that the pixel values are *really* different for each of these images. So, the challenge becomes: how can we create a classifier that, for any of these grids of pixel values, will be able to classify each one of them as a car.

### Data-Driven Approach

Since there is no clear way to create a set of rules about pixel values that make up a car, we’ll instead take a data-driven approach:

> 1. Collect a set of images with *true* class labels. 
> 2. Train a model to produce an accurate, *predicted* class label.


<p align="center">  
<img src="/assets/cnn_intro/training_data.png" alt="True and predicted class labels for a car image."  width="600" >
</p>

In this example, we'll plan to train a convolutional neural network. As this network trains, it should learn what parts of a car are important to recognize, such as wheels and windows, and it should be general enough to recognize cars in a variety of positions and environments.


---

## Convolutional Neural Network

To approach this image classification task, we’ll use a convolutional neural network (CNN), a special kind of neural network that can find and represent patterns in 3D image space. Many neural networks look at individual inputs (in this case, individual pixel values), but convolutional neural networks can look at groups of pixels in an area of an image and learn to find spatial patterns.

Every CNN is made up of multiple layers, the three main types of layers are convolutional, pooling, and fully-connected, as pictured below. Typically, you’ll see CNN's made of many layers, especially convolutional and pooling layers. Each of these layers is made of nodes that look at some input data and produce an output, so let's go over what each of these layers does!

<p align="center">
<img src="/assets/cnn_intro/CNN_ex.png" alt="A CNN that sees an image of a car and outputs a class." width="600" >
</p>

### Convolutional Layer

The convolutional layer can be though of as the *feature extractor* of this network, it learns to find spatial features in an input image. This layer is produced by applying a series of many different image filters, also known as convolutional kernels, to an input image. These filters a very small grids of values that slide over an image pixel-by-pixel, and produce a filtered output image that will be about the same size as the input image. Multiple kernels will produce multiple filtered, output images.

<p align="center">
<video controls="controls" width="500" height="300" 
name="Video Name" src="/assets/cnn_intro/conv_layer.mov"></video>
</p>

Say we have four different convolutional kernels, these will produce four different, filtered images as output. The idea is that each filter will extract a different feature from an input image and these features will eventually help to classify that image, for example, one filter might detect the edges of objects in that image and another might detect unique patterns in color. These filters, stacked together, are what make up a convolutional layer.


---

## High-pass Filter

Let’s take a closer look at one type of convolutional kernel: a high-pass image filter. High-pass filters are meant to detect abrupt changes in intensity over a small area. So, in a small patch of pixels, a high-pass filter will highlight areas that change from dark to light pixels (and vice versa). I'll be looking at patterns of intensity and pixel values in a grayscale image.

<p align="center">
<img src="/assets/cnn_intro/filtered_ex.png" alt="Filtered image of a car." width="500" >
</p>

For example, if we put an image of a car through a high-pass filter, we expect the edges of the car, where the pixel values change abruptly from light to dark, to be detected. The edges of objects are often areas of abrupt intensity change and, for this reason, high-pass filters are sometimes called "edge detection filters."

#### Convolution Kernels

The filters I’ll be talking about are in the form of matrices, often called convolution kernels, which are just grids of numbers that modify an image. Below is an example of high-pass filter, a 3x3 kernel that does edge detection.

<p align="center">
<img src="/assets/cnn_intro/edge_detection_filter.png" alt="3x3 edge detection filter with row values [0,-1,0], [-1,4,-1], [0,-1,0]." width="200" >
</p>

You may notice that all the elements in this 3x3 grid sum to zero. For an edge detection filter, it’s important that all of it's' elements sum to zero because it's computing the difference or change between neighboring pixels. If these pixel weights did not add up to zero, then the calculated difference would be either positively or negatively weighted, which has the effect of brightening or darkening the entire filtered image, respectively.

### Convolution

To apply this filter to an image, an input image, F(x,y), is convolved with the kernel, K. Convolution is represented by an asterisk (not to be mistaken for multiplication). It involves taking a kernel, which is our small grid of numbers, and passing it over an image, pixel-by-pixel, creating another edge-detected output image whose appearance depends on the kernel values.

<p align="center">
<video controls="controls" width="500" height="300" 
name="Video Name" src="/assets/cnn_intro/filter_animation.mov"></video>
</p>

I’ll walk through a specific example, using the 3x3 edge detection filter.
 To better see the pixel-level operations, I’ll zoom in on the image of the car. 

<p align="center">
<img src="/assets/cnn_intro/zoomed_corner.png" alt="Zoomed in pixel area near the top-right edge of the car." width="600" >
</p>

For every pixel in this grayscale image, we place our kernel over it, so that the selected pixel is at the center of the kernel, and perform convolution. In the below image, I'm selecting a center pixel with a value of 200, as an example.

<p align="center">
<img src="/assets/cnn_intro/pixel_selection.png" alt="Kernel overlaid on a 3x3 pixel area." width="500" >
</p>

The steps for a complete convolution are as follows:
1. Multiply the values in the kernel with their matching pixel value. So, value in the top left of the 3x3 kernel (0), will be multiplied by the pixel value in that *same* corner in our image area (150).
2. Sum all these multiplied pairs of values to get a new value, in this case, 175. This value will be the new pixel value in the filtered output image, at the same (x,y) location as the selected center pixel.

<p align="center">
<video controls="controls" width="500" height="300" 
name="Video Name" src="/assets/cnn_intro/convolution_steps.mov"></video>
</p>

This process repeats for every pixel in the input image, until we are left with a complete, filtered output.

#### Weights 

Before we move on, I want to add a bit of terminology. The values inside a kernel, which are multiplied by their corresponding pixel value, are called **weights**. This is because they determine how important (or how weighty) a pixel is in forming a new, output image. You’ll notice that the center pixel has a weight of 4, which means it is heavily, positively weighted. Out of all the pixels in a 3x3 patch, the center pixel will be the most important in determining the value of the pixel in the output, filtered image.

<p align="center">
<img src="/assets/cnn_intro/weights.png" alt="3x3 kernel weight values are highlighted." width="500" >
</p>

The kernel also contains negative weights with a value of -1. These correspond to the pixels that are directly above and below, and to the left and right, of the center pixel. These pixels are closest to the center pixel and, because they are symmetrically distributed around the center, we can say that this kernel will detect any change in intensity around a center pixel on its left and right sides *and* on its top and bottom sides.

#### Image Borders

The only pixels for which convolution doesn't work are the pixels at the borders of an image. A 3x3 kernel cannot be perfectly placed over a center pixel at the edges or corners of an image. In practice, there are a few of ways of dealing with this, the most common ways are to either pad this image with a border of 0’s (or another grayscale value) so that we can perfectly overlay a kernel on all the pixel values in the original image, or to ignore the pixel values at the borders of the image, and only look at pixels where we can completely overlay the 3x3 convolutional kernel.

<p align="center">
<video controls="controls" width="500" height="300" 
name="Video Name" src="/assets/cnn_intro/edge_handling.mov"></video>
</p>

Often, there is not a lot of useful information at the border of an image, but if you do choose to ignore this information, every filtered image will be just a little bit smaller that the original input image. For a 3x3 kernel, we’ll actually lose a pixel from each side of an image, resulting in a filtered output that is two pixels smaller in width and in height than the original image. You can also choose to make larger filters. 3x3 is one of the smallest sizes and it’s good for looking at small pixel areas, but if you are analyzing larger images you may want to increase the area and use kernels that are 5x5, 7x7, or larger. Usually, you want an odd number so that the kernel nicely overlays a center pixel.

<p align="center">
<img src="/assets/cnn_intro/horizontal_filter.png" alt="3x3 horizontal edge detection filter." width="500" >
</p>

Above is another type of edge detection filter; this filter is computing the difference around a center pixel but it’s only looking at the bottom row and top row of surrounding pixel values. The result is a horizontal edge detector. In this way, you can create oriented edge detectors!

<p align="center">
<img src="/assets/cnn_intro/CNN_ex.png" alt="A CNN that sees an image of a car and outputs a class." width="600" >
</p>

So, these convolutional kernels, when applied to an image, make a filtered image and *several* filtered images make a convolutional layer. Up next: the pooling layer; the most common type of pooling layer is a *maxpooling* layer.


---

## Maxpooling Layer 

A pooling layer will also look at the pixel values in an image, so I'll focus on a small pixel area, again. First it breaks an image into smaller patches, often 2x2 pixel areas.

<p align="center">
<img src="/assets/cnn_intro/patches.png" alt="2x2 pixel patches." width="300" >
</p>

Let’s zoom in even further on four of these patches. A maxpooling layer is defined by the patch size, 2x2, and a stride. The patch can be thought of as a 2x2 window that the maxpooling layer looks at to select a maximum pixel value. It then moves this window by some stride across and down the image. For a patch of size 2x2 and a stride of 2, this window will perfectly cover the image. A smaller stride would see some overlap in patches and a larger stride would miss some pixels entirely. So, we usually see a patch size and a stride size that are the same.



<p align="center">
<video controls="controls" width="400" height="200" 
name="Video Name" src="/assets/cnn_intro/stride.mov"></video>
</p>

For each 2x2 patch, a maxpooling layer looks at each value in a patch and selects only the maximum value. In the red patch it selects 140, in the yellow, 90, and so on, until we are left with four values from the four patches.

<p align="center">
<img src="/assets/cnn_intro/maxpool.png" alt="2x2 pixel patches." width="500" >
</p>

Now, you might be wondering why we would use a maxpooling layer in the first place. This layer is discarding pixel information. We use a maxpooling layer for a couple of reasons. First, dimensionality reduction;  As an input image moves forward through a CNN, we are taking a fairly flat image in x-y space and expanding its depth dimension while decreasing its height and width. The network distills information about the content of an image and squishes it into a representation that will make up a reasonable number of inputs that can be seen by a fully-connected layer. Second, maxpooling makes a network resistant to small pixel value changes in an input image. Imagine that some of the pixel values in a small patch are a little bit brighter or darker. Even if a patch has some slightly different pixel values, the maximum value, if it is a large enough maximum, should be the same.


---

## PyTorch Code Examples

If you'd like to see how to create these kinds of CNN layers using PyTorch code, I have a [public, tutorial repository](https://github.com/cezannec/intro-computervision). There are instructions for setting up a local environment and running this code, or you can just look at the code and its output. The layers in this post correspond to the first notebook: **1. Convolutional NN Layers, Visualization**.

<p align="center">
<img src="/assets/cnn_intro/all_layers_code.png" alt="Output of all CNN layers executed in PyTorch code." width="600" >
</p>

Note that, in the first notebook, I've initialized and explicitly defined the weights of the convolutional layer. However, when we get to training a neural network on image data, the network will have to *learn* the best weights for convolutional kernels that extract features from an input image. These learned features will be used to separate different classes of data.


---

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/cezannecam) or connect with me on [LinkedIn](https://www.linkedin.com/in/cezanne-camacho-422823b2/).


