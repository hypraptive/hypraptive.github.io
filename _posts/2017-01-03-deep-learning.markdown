---
layout: post
title:  "Diving into Deep Learning"
author: Ed
date:   2017-01-03 17:00:00
excerpt: "How we got into deep learning."
---
### Some Background

At hypraptive, we've been working on a number of different projects over the years. Projects we have been/are involved with include an Android app that helps improve driving milage, a website to rate specific dishes at restaurants and an automatic photo curator and slideshow video creator. It was only recently that I decided to start blogging about some of the projects. For now I'll be focusing on a deep learning project we started in 2016, but perhaps in the future we will include other topics. I'll spend the next few blogs catching up to where were are today.

### Coming Up to Speed

In mid-2016, my partner and I started to get interested in deep learning. Actually, I've had an interest in [artificial intelligence](https://en.wikipedia.org/wiki/Artificial_intelligence) ever since my days at [CMU](http://www.cmu.edu/) where I worked on neural network projects in cognitive psychology courses. When I graduated, there just weren't many jobs in that area, so I lost track of the space for quite a while. In the past few years, AI has made a significant comeback, especially under the guise of deep learning and autonomous driving. I thought it was time to get involved.

To get our feet wet, we went through the father of all [Cousera](https://www.coursera.org/) courses, [Machine Learning](https://www.coursera.org/learn/machine-learning), taught by Stanford professor and Coursera co-founder (now at Baidu), [Andrew Ng](http://www.andrewng.org/). The course is a pretty good primer on machine learning, covering a variety of topics from [linear regression](https://en.wikipedia.org/wiki/Linear_regression) to [artificial neural networks](https://en.wikipedia.org/wiki/Artificial_neural_network). It took some effort to become re-acquainted with linear algebra and matrices, but unless you are planning to develop your own implementations from scratch, you don't need to be an expert. The programming assignments use [Octave](https://www.gnu.org/software/octave/), a GNU scientific programming platform compatible with [Matlab](https://www.mathworks.com/products/matlab.html). Most of the software framework was provided, so the assignments didn't take too long, but were still quite educational. The course is a little dated at this point, but it's well worth going through if you need a introduction to general machine learning.

Having whet our appetites, we were ready for more. Much of my career has been centered around audio and video technologies and I was keen to dive into [deep learning](https://en.wikipedia.org/wiki/Deep_learning) which could be applied to this space. In the past few years, there have been huge advances in image recognition by applying neural networks. Since 2012, all the winners of the [ImageNet Large Scale Visual Recognition Challenge](http://image-net.org/challenges/LSVRC/2012/index) have been based on [Convolutional Neural Networks](https://en.wikipedia.org/wiki/Convolutional_neural_network) (CNNs). It made sense to start learning more about these CNNs.

We started to get familiar with CNNs by reading articles and blogs. Through this process, we were able to get a basic understanding, but we wanted something more structured. I was basing a lot of my exploration on CNNs used for solving the problems from the [ImageNet](http://image-net.org/) challenges. It turns out, Stanford was offering a course on just this topic: [CS231n: Convolutional Neural Networks for Visual Recognition](http://cs231n.stanford.edu/). There's a complete set of lectures of the Winter 2016 course available on [YouTube](https://www.youtube.com/playlist?list=PLwQyV9I_3POsyBPRNUU_ryNfXzgfkiw2p). We watched most of the videos in this set, but didn't attempt any of the programming assignments (although I believe many of them are available online).

### What Now?

Armed with a reasonable understanding of how CNNs work for image recognition tasks, we decided it was time to start putting our knowledge into practice. We already had a shared interest right under our noses. Could it benefit from deep learning? Let's start exploring in the next blog.
