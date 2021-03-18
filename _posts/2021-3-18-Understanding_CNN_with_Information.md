---
layout: post
title: Understanding Deep Learning with Information Theory
---


<p align="center">
<img src="/assets/cnn_text/conv_maxpooling_steps.gif" alt="Convolution then maxpooling over some sequential word embeddings." width="600" >
</p>

<!--more-->


---



In the [code associated with this post](https://github.com/cezannec/CNN_Text_Classification), I am going to use a pre-trained Word2Vec model to create word embeddings for a dataset of movie reviews.

---

 included to account for the height of the kernel. The relationship between padding and kernel size is described in more detail, in a [previous post](https://cezannec.github.io/Convolutional_Neural_Networks/). Below, you can see what the output of a 1D convolution might look like when applied to a short sequence of word embeddings.


---

## Further Learning

As I was writing the text classification code, I found that CNNs are used to analyze sequential data in a number of ways! Here are a couple of papers and applications that I found really interesting:
* CNN for semantic representations and search query retrieval, [[paper (Microsoft)](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/www2014_cdssm_p07.pdf)].
* CNN for genetic mutation detection, [[paper (Nature)](https://www.nature.com/articles/s41467-019-09027-x)].
* CNN for classifying whale sounds via spectogram, [[blog post (Google AI)](https://ai.googleblog.com/2018/10/acoustic-detection-of-humpback-whales.html)].

I encourage you to read more and try to implement an application that interests you! 


---

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/cezannecam) or connect with me on [LinkedIn](https://www.linkedin.com/in/cezanne-camacho-422823b2/).


