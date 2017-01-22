---
layout: post
title:  "FaceNet for Bears"
author: Ed
date:   2017-01-21 16:00:00
excerpt: "Our plan for a face recognition pipeline for bears inspired by FaceNet."
---
In the previous post, [Deep Learning in the Wild](/2017/01/13/dl-in-the-wild.html), we uncovered a number of projects working on identifying and recognizing animals in the wild. While nothing we have run across so far seems to fit our needs for brown bears, some of the projects seem promising. However, since one of the key points of this project was to gain experience in deep learning, we decided to attempt to develop our own solution, based on more general computer vision and deep learning tools.

In [Bear Necessities](/2017/01/09/bear-necessities.html), we described the methods researchers utilize to identify the brown bears in Katmai. We quickly eliminated some of these methods and characteristics from our consideration. For example, while it is conceivable to analyze video input to identify bear behaviors, we believe the necessary video data required and compute power for analysis puts this method beyond the reach of our project. We also eliminated characteristics that vary significantly from season to season or within a season, such as body size/shape and fur color/patterns. We have decided to focus our efforts on the face and ears. We feel that focusing on these characteristics will bound the complexity of our project while still having a reasonable chance of producing useful results. For example, many watchers of the [Brooks Falls Live Cam](http://explore.org/live-cams/player/brown-bear-salmon-cam-brooks-falls) can identify bear 480 Otis by his somewhat floppy right ear (see below).

![480 Otis](/assets/480otis.jpg){: figure }

### Face Recognition with Deep Learning

Face recognition is one of the most common applications for deep learning these days. One of the top methods for face recognition is [FaceNet](https://arxiv.org/abs/1503.03832), which was developed by a team at Google in 2015. [Adam Geitgey](https://medium.com/@ageitgey) wrote a fantastic article describing how a method like FaceNet works. The article, [Modern Face Recognition with Deep Learning](https://medium.com/@ageitgey/machine-learning-is-fun-part-4-modern-face-recognition-with-deep-learning-c3cffc121d78), breaks the process down to four steps:

1. Find the face
2. Reorient each face
3. Encode the face
4. Match the face

We will attempt to build a similar pipeline to identify our bears.

#### Find the Face

We expect this step to be fairly straightforward. There are already many deep learning and traditional computer vision algorithms which can accurately locate objects (including human faces) in an image. We plan to have a look at a couple CNN based object detectors, such as [Faster R-CNN](https://github.com/ShaoqingRen/faster_rcnn) and [YOLO](http://pjreddie.com/darknet/yolo/). We'll also look at the more traditional face detection method, [Histogram of Oriented Gradients (HOG)](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients), using a library such as [dlib](https://sourceforge.net/projects/dclib/). The hardest part of this step will be annotating a sufficient number of bear images with the face location data used to train the algorithm.

#### Reorient the Face

Once we have found the bear face, reorienting them should be fairly simple. The FaceNet method only requires rotation and scaling. This can be accomplished with [dlib](https://sourceforge.net/projects/dclib/). The trick will be identifying appropriate landmarks on each bear face. There are sophisticated landmark estimators for human faces which generate 68 or more specific points. In fact, the human face reorientation only considers 3 points, the tip of the nose and the outside point of each eye. Estimating a few landmark points for bears will again require annotating a sufficient number of bear images with landmark data for training.

One caveat we should keep in mind: human noses aren't very long compared to bears. For human face, the FaceNet algorithm is still pretty good when the face is turned somewhat up, down or to either side. However, the longer nose of a bear may have a much bigger impact on the recognition algorithms reliability when the pose is even a little off center. We will have to experiment to see.

#### Encode the Face

In this step we want to take the reoriented face and turn it into a set of measurements, such as the distance between the eyes and the ear size. Rather than using a human defined set of measurements, FaceNet makes use of a Deep Convolutional Neural Network (DCNN) to learn a set of 128 measurements. This set of measurements for each face is also known as an **embedding**. The DCNN is trained using a large set image triplets. An image triplet will consist of the following:

1. an image of bear A
2. a different image of bear A
3. an image of bear B

During training, the learning algorithm will tweak the parameters making sure the embeddings for images 1 and 2 are slightly closer while those of 2 and 3 are further apart. Once we have trained the network, we can use it to generate an embedding of the face we are trying to identify.

In practice, training requires millions of triplets to achieve a well performing face encoder. This has already been done for human faces by numerous project, such as [OpenFace](https://cmusatyalab.github.io/openface/). We will need to train our own network for our bears. This step will likely be the most challenging, both in terms of data preparation and compute time. At the start, perhaps we can try a smaller DCNN with fewer measurements. For a small population of bears, this may be sufficient to prove the algorithm's effectiveness for bears.

#### Match the Face

Once we have an embedding for the face, all that remains is to find the bear in our database which is the closest match. This can be achieved with any basic classification algorithm. An [SVM classifier](https://en.wikipedia.org/wiki/Support_vector_machine) was used in the referenced article. We would probably use something similar.

### Let's Get started

To get started, we need to collect a bunch of images of bears. For face detection and orientation, we can use any brown bear images. We can collect these by sifting through Google images searches and the like. At the beginning, we will focus on images where the bear is facing mostly forward. We'll need to annotate a training set with bounding boxes for the faces and whichever landmark points we will use for orientation. For training the face encoder, we will need pairs of known bears. Most likely these will come from web postings and photo galleries related to Brooks River. We have also contacted Katmai National Park to try to get some images. We can add random other bear images to complete the triplets. Our database of known bears will consist of regularly sighted bears listed in the [Bears of Brooks River eBooks](https://www.nps.gov/katm/learn/photosmultimedia/ebooks.htm).

![Brooks Falls](/assets/brooks-falls-banner.jpg){: figure }

To get our feet wet with training, we will likely start with the face detector. We expect to be able to achieve something reasonable in a fairly short order. Once we have something working, improving accuracy should be a matter of more data and training. Finding the face landmarks should be on par with face detection. More data and training will lead to better results. We do need to keep the "nose" problem in mind.

As we collect a larger set of images, we will need to start working on the face encoder. This is the real deep learning portion of the pipeline. We may end up having to invest in some GPU hardware, perhaps building a desktop with a couple of GPU cards. We could also consider some cloud services with GPU instances, but with all the data transfers and experimentation, this may be more expensive for the development phase than building our own machine.

If anyone has thoughts or ideas about the method we are planning to use, hardware/cloud services for training or anything else, please leave them in the comments below.
