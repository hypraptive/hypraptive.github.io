---
layout: post
title:  "Find the Bears: dlib"
author: Ed
date:   2017-02-02 16:00:00
excerpt: "Looking for a quick and simple object detector we can train for bear faces, we give dlib's HOG based detector a try."
---
Last time, in [Find the Bears: YOLO](/2017/01/29/find-the-bears-yolo.html), we talked about [transfer learning](http://cs231n.github.io/transfer-learning/) and [Region-based CNN](https://github.com/rbgirshick/rcnn) (or R-CNN). We also discussed our attempt to use [YOLO: Real-Time Object Detection](http://pjreddie.com/darknet/yolo/), but we were unable to train any models on our CPU-only computer (training was only supported on a GPU system). We decided to go back to the article that introduced us to the FaceNet pipeline, [Modern Face Recognition with Deep Learning](https://medium.com/@ageitgey/machine-learning-is-fun-part-4-modern-face-recognition-with-deep-learning-c3cffc121d78), and check out the face detection method described there. This method uses [Histogram of Oriented Gradients (HOG)](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients) from the [dlib](http://dlib.net/) toolkit.

### Histogram of Oriented Gradients (HOG)

Object detection has been a key computer vision problem for quite a long time. Digital images are simply a sequence of pixels, each of which records the color intensities for a specific location in the image. Unfortunately, this series of numbers doesn't mean much to a computer without some context. Before deep learning really took off, rather than trying to teach the context to the computer, computer vision experts created features which could be more easily interpreted by a computer. One of these features is the Histogram of Gradients, or HOG for short.

![HOG Example](/assets/find-the-bears/hog-example.png){: figure }

As [Modern Face Recognition with Deep Learning](https://medium.com/@ageitgey/machine-learning-is-fun-part-4-modern-face-recognition-with-deep-learning-c3cffc121d78) describes, HOG has been around since 2005 and is is a pretty capable object detector. The idea behind HOG is to add up the gradients (rate of change) between a pixel and all of its immediate neighbors. The article gives a pretty good description on how this is used for face detection. You can see what an image looks like after HOG is applied in the example above (taken from [scikit-image HOG Page](http://scikit-image.org/docs/dev/auto_examples/plot_hog.html)). This view really highlights the areas of the image where a lot is going on, such as edges and point. You can see the eyes really stand out in the HOG image. Check out the article for more details.

### Dlib Toolkit

> Dlib is a modern C++ toolkit containing machine learning algorithms and tools for creating complex software in C++ to solve real world problems.

[Dlib](http://dlib.net/) has a bunch of cool tools, one of which enables you to easily create HOG based object detectors. It is implemented in C++, but there are also python bindings available. The dlib HOG trainer uses a built in structural [Support Vector Machine (SVM)](https://en.wikipedia.org/wiki/Support_vector_machine) training algorithm. At the end of training you should end up with a nice, general feature descriptor which can be used to detect similar objects in new images.

#### Installing and Building dlib

We downloaded the latest [dlib](http://dlib.net/) (currently version 19.2) and got started. I ran into some problems building and running dlib on my MacBook Pro. Rather than waste time fixing the issues, we decided to use a virtual machine running Linux since we'll eventually build a Linux server for this project. We're running [Ubuntu 14.04](http://releases.ubuntu.com/14.04/) on [VirtualBox](https://www.virtualbox.org/) (mainly because we already had the VM). To build dlib on the VM, I needed to install a few packages (`cmake`, `libx11-dev`, `cmake-qt-gui`, `opencv`), then I was able the execute the following (see [How to Compile](http://dlib.net/compile.html)).

```
tar xf dlib-19.2.tar.bz2
cd dlib-19.2/example
mkdir build
cd build/
cmake ..
cmake --build . --config Release
```

#### Making an Object Detector with dlib

To get started with making our own object detector, we read through the dlib blog post: ["Make your own object detector!"](http://blog.dlib.net/2014/02/dlib-186-released-make-your-own-object.html) The blog post discusses the example programs provided with dlib. We tried out their [face detection example program](http://dlib.net/face_detection_ex.cpp.html) which works pretty well. Next we replicated their face detection example using the [FHOG object detector example](http://dlib.net/fhog_object_detector_ex.cpp.html), which uses only 4 images containing a total of 18 faces for training. Even with the small training set, the resulting detector works pretty well.

### Nest Steps

The fact that we can train a decent face detector with only a few training images on a laptop gives us hope. Next time we will try to build a detector for bear faces using the dlib [Train Object Detector](http://dlib.net/train_object_detector.cpp.html) command line tool example.
