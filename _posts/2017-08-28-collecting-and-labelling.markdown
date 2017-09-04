---
layout: post
title:  "Collecting and Labelling Data"
author: Ed
date:   2017-08-28 16:00:00
excerpt: "Our efforts to collect and label more data."
---

# Collecting More Data

In the post [Bear Face Chips From Videos](/2017/04/21/bearid-video-chips.html), we said our top priority is getting more data. Well, **that is still the case!** We are expecting 2 sizable sets of data, but we're not quite sure when we will get them:

* [Katmai National Park](https://www.nps.gov/katm) will be sending some photos from their bear monitoring program as well as some personal images from Ranger Dave and Ranger Anela. Many thanks to Ranger Anela and Ranger Leslie for their contributions and extra thanks to Ranger Dave for putting it all together in his "spare" time!
* The [Brown Bear Research Network (BBRN)](http://bearresearch.org/) will send us a set of photos and videos of brown bears from British Colombia, Canada. Unfortunately, their first attempt to send us data was thwarted by the postal service (USPS or Canada Post, we're not sure which).

# Focus on Embedding Network

As a reminder, our current approach for bear identification, as described in our blog [FaceNet for Bears](/2017/01/21/facenet-for-bears.html), is based on [FaceNet](https://arxiv.org/abs/1503.03832). This deep learning method requires a lot of labeled data to train a set of neural networks. The steps are:

1. Find the face
2. Reorient each face
3. Encode the face
4. Match the face

Our main concern is **stage 3**, encoding the face. We need to train the encoding network from scratch. To do this, we need a lot of face chips (normalized and cropped to just the face) of a lot of different bears. We also need the bear in each photo or video to be uniquely identified (e. g. Brooks Falls bear # 480). If we get sufficient data, we can train a network that will work not only for the bears we trained it with, but also for new bears. If not, we may need to train a network to work on a specific set of bears. Unfortunately, we don't know how much data we need for either of these cases. We'll just have to keep collecting data and retraining the network to find out.

# Manual Labelling

For finding bear faces, we have been using the [Dog Hipsterizer](http://blog.dlib.net/2016/10/hipsterize-your-dog-with-deep-learning.html) example from the [Dlib Toolkit](http://dlib.net/), which happens to work fairly well for bears. The dog hipsterizer also finds some of the face landmarks (e. g. eyes and nose) which are needed for reorienting the face before we crop it to make a face chip. The landmarks created by the dog hipsterizer network can be off by quite a bit for our bears. To improve the face chips for use in training the encoding network, we are using [imglab](https://github.com/davisking/dlib/tree/master/tools/imglab) to manually adjust the face landmarks for each bear face we find. Later, we will use our manually adjusted face data as the ground truth to train our own bear face detector network to replace the dog hipsterizer.

We are using the manually corrected dataset to run various experiments using different hyperparameters for training the embedding network. We should start seeing some results of various experiments in the coming weeks.
