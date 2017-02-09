---
layout: post
title:  "Hipster Bears"
author: Ed
date:   2017-02-08 16:00:00
excerpt: "Having fun with dlib's dog hipsterizer example and realizing it just may be just what we need."
---
In the last post, [Bear Face Detector](/2017/02/03/bear-face-detector.html), we described how we used the [Dlib Toolkit](http://dlib.net/) to train a [Histogram of Oriented Gradients (HOG)](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients) based detector for bear faces. Having succeeded in training a working bear face detector, we laid out three possible next steps:

1. Improve the dlib HOG detector thought better training.
2. Look into the dlib CNN detector.
3. Move on to the next stage: reorientation.

We decided to take a look at the dlib CNN detector.

### Deep Learning with dlib

We started out by reading the dlib blog post: [Easily Create High Quality Object Detectors with Deep Learning](http://blog.dlib.net/2016/10/easily-create-high-quality-object.html). The detector we trained last time relied on the HOG feature extractor followed by a single linear filter. It works pretty well, but can not handle a lot of pose variability. To deal with this, we would have to train a different detector for each pose (e. g. bear looking at camera versus bear in profile). This limitation is not a show stopper for us, since we are focusing our efforts on bears looking toward the camera anyway.

The new detector described in the dlib blog utilizes a CNN based feature extractor. As we discussed in a earlier blog, CNNs are great at image detection and classification problems. In fact, all of the ImageNet Challenge winners in recent years utilize CNNs. The dlib blog post provides some performance numbers for the [Face Detection Data Set and Benchmark (FDDB)](http://vis-www.cs.umass.edu/fddb/) which look quite good. The main concern with this approach is the training time that may be required. The CNN detector example code talks about *hours* while the HOG detector trained in minutes, and that for the small example dataset provided (4 images). We still don't have the compute power or annotated data for high quality training.

### Hipsterizer

The dlib blog goes on to talk about some other tests of the CNN detector. One of the tests is the [Dog Hipsterizer](http://blog.dlib.net/2016/10/hipsterize-your-dog-with-deep-learning.html). This is a fairly silly example which takes images of dogs and adds thick eyeglasses and a curly mustache to each dog face. It was trained on more than 9000 dog heads, so it works fairly well. On a whim, I gave it a try with one of our bear images, and it worked!

![Hipster Bears](/assets/hipster-bears/hipster-bears.png){: figure }

The HOG detector we trained last time did not detect any bear faces on this image. Rather than improve the HOG detector or start training a CNN bear face detector, perhaps we can simply use the pretrained model from the Dog Hipsterizer for now.

### Face Landmarks

The Dog Hipsterizer has three steps:

1. It uses [dlib's deep learning tools](http://blog.dlib.net/2016/06/a-clean-c11-deep-learning-api.html) to detect dogs looking at the camera.
2. It uses the [dlib shape predictor](http://blog.dlib.net/2014/08/real-time-face-pose-estimation.html) to identify the positions of the eyes, nose, and top of the head.
3. It draws glasses and a mustache.

Step 1 is the same as our **stage 1 (Find the Face)**. For our **stage 2 (Reorient Each Face)** we need the eye and nose landmarks created in the hipsterizers' step 2:

![Bear Face Landmarks](/assets/hipster-bears/landmark-bears.png){: figure }

Instead of drawing glasses and a mustache on each bear, we can modify it for our **stage 2**. Namely, we extract the face and use the landmarks for reorienting the face. Once we have the reoriented face, we pass it to **stage 3 (Encode the Face)**.

![Reorienting Bear Face](/assets/hipster-bears/reorienting-bears.png){: figure }

This could possibly get us through **stage 1** and **stage 2** without doing any training of our own.

### Next Steps

The pre-trained network from the Dog Hipsterizer example seems to work pretty well for bears. It already works better than the simple HOG based detector we trained last time, so for now we're going to run with it. To complete **stage 2** we need to modify the code to add in the face reorientation (rotation and scaling). Eventually, we may need to retrain the network with bear examples, but we'll cross that bridge if/when we come to it.

Training the CNN detector takes quite a bit longer than training the HOG detector (hopefully we won't need to train it for a while). Even the detection takes longer with the CNN detector. Also, the face encoder in **stage 3** is probably going to be the hardest to train in terms of compute. Now might be a good time to invest in some hardware. With that in mind, we put together a build list of a basic PC with a decent GPU. You can see the [Hypraptive ML #1 Part List on PCPartPicker](https://pcpartpicker.com/user/bluevalhalla/saved/#view=X9RnQ7). We hope to get all the parts within the next few days.

In the coming days look for posts about our progress with face reorientation as well as a deeper dive into our hardware build.
