---
layout: post
title:  "The Many Faces of Brooks Falls"
author: Ed
date:   2017-08-14 16:00:00
excerpt: "An overview of the bear data we have so far."
---

In the last post, [Bear Face Chips From Videos](/2017/04/21/bearid-video-chips.html), we said our top priority is getting more data. Well, **that is still the case!** We are expecting 2 sizable sets of data, but we're not quite sure when we will get them:

* [Katmai National Park](https://www.nps.gov/katm) will be sending some photos from their bear monitoring program as well as some personal images from Ranger Dave and Ranger Anela. Many thanks to Ranger Anela and Ranger Leslie for their contributions and extra thanks to Ranger Dave for putting it all together in his "spare" time!
* The [Brown Bear Research Network (BBRN)](http://bearresearch.org/) will send us a set of photos and videos of brown bears from British Colombia, Canada. Unfortunately, their first attempt to send us data was thwarted by the postal service (USPS or Canada Post, we're not sure which).

# Brown Bear Research Network (BBRN)

We have started a collaboration with the [Brown Bear Research Network (BBRN)](http://bearresearch.org/). The BBRN are a network of scientists and commercial bear-viewing operators, committed to the conservation of brown bears in British Columbia. They are interested in developing an automatic method of identifying bears to use with their camera traps to survey and monitor brown bears worldwide. After a few discussions, we agreed we should join forces. In addition to their own research images, they have put out a call to researchers, bear tourists and citizen scientists to contribute photos and videos to the project:

<img src="/assets/many-faces/BBRN-call-for-photos.jpg" width="500">

# Where We Are Now

As a reminder, our current approach for bear identification, as described in our blog [FaceNet for Bears](/2017/01/21/facenet-for-bears.html), is based on [FaceNet](https://arxiv.org/abs/1503.03832). This deep learning method requires a lot of labeled data to train a set of neural networks. The steps are:

1. Find the face
2. Reorient each face
3. Encode the face
4. Match the face

Our main concern is **stage 3**, encoding the face. We need to train the encoding network from scratch. To do this, we need a lot of face chips (normalized and cropped to just the face) of a lot of different bears. We also need the bear in each photo or video to be uniquely identified (e. g. Brooks Falls bear # 480). If we get sufficient data, we can train a network that will work not only for the bears we trained it with, but also for new bears. If not, we may need to train a network to work on a specific set of bears. Unfortunately, we don't know how much data we need for either of these cases. We'll just have to keep collecting data and retrain the network to find out.

For finding bear faces, we have been using the [Dog Hipsterizer](http://blog.dlib.net/2016/10/hipsterize-your-dog-with-deep-learning.html) example from the [Dlib Toolkit](http://dlib.net/), which happens to work fairly well for bears. The Dog Hipsterizer also finds some of the face landmarks (e. g. eyes and nose) which are needed for reorienting the face before we crop it to make a face chip. The landmarks created by the Dog Hipsterizer network can be off by quite a bit for our bears. To improve the face chips for use in training the encoding network, we are using [imglab](https://github.com/davisking/dlib/tree/master/tools/imglab) to manually adjust the face landmarks for each bear face we find. Later, we will use our manually adjusted face data as the ground truth to train our own bear face detector network to replace the dog hipsterizer.

We are using the manually corrected dataset to run various experiments using different hyperparameters for training the embedding network. We should start seeing some results of various experiments in the coming weeks.

# Brooks Falls Dataset

So far we have put together a data set of approximately 1100 bear face chips, all from Brooks Falls bears. The face chips were extracted from photos from the following sources:

* [Mike Fitz's Flickr album](https://www.flickr.com/photos/ikefitz/albums) (thanks Mike!)
* [Carla Farris' Flickr Album](https://www.flickr.com/photos/129908461@N03/albums/with/72157672138992512)
* [Ranger Jeanne's Flickr Album](https://www.flickr.com/photos/jeanner/albums)
* Photos sent by larinor (thank you!)

Below is a table of the Brooks Falls bear chip data. We have face chips for 43 different bears. The table has a row for each bear. The columns are:

* **ID**: the bear's identification number
* **Nickname**: the bear's nickname (if it has one)
* **Count**: the number of face chips we have for the bear
* **Example Face Images**: a few example face chips for the bear

ID | Nickname | Count | Example Face Images
---- | :----: | :----: | ----
032 | Chunk| 16 | ![](/assets/many-faces/bf_032/001.jpg) ![](/assets/many-faces/bf_032/002.jpg) ![](/assets/many-faces/bf_032/003.jpg)
051 | Diver Jr. | 1 | ![](/assets/many-faces/bf_051/001.jpg)
068 | | 7 | ![](/assets/many-faces/bf_068/001.jpg) ![](/assets/many-faces/bf_068/002.jpg) ![](/assets/many-faces/bf_068/003.jpg)
083 | Wayne Brother | 21 | ![](/assets/many-faces/bf_083/001.jpg) ![](/assets/many-faces/bf_083/002.jpg) ![](/assets/many-faces/bf_083/003.jpg)
089 | Backpack | 28 | ![](/assets/many-faces/bf_089/001.jpg) ![](/assets/many-faces/bf_089/002.jpg) ![](/assets/many-faces/bf_089/003.jpg)
094 | | 11 | ![](/assets/many-faces/bf_094/001.jpg) ![](/assets/many-faces/bf_094/002.jpg) ![](/assets/many-faces/bf_094/003.jpg)
128 | Grazer | 61 | ![](/assets/many-faces/bf_128/001.jpg) ![](/assets/many-faces/bf_128/002.jpg) ![](/assets/many-faces/bf_128/003.jpg)
132 | | 29 | ![](/assets/many-faces/bf_132/001.jpg) ![](/assets/many-faces/bf_132/002.jpg) ![](/assets/many-faces/bf_132/003.jpg)
151 | Walker | 67 | ![](/assets/many-faces/bf_151/001.jpg) ![](/assets/many-faces/bf_151/002.jpg) ![](/assets/many-faces/bf_151/003.jpg)
171 | | 3 | ![](/assets/many-faces/bf_171/001.jpg) ![](/assets/many-faces/bf_171/002.jpg) ![](/assets/many-faces/bf_171/003.jpg)
201 | | 1 | ![](/assets/many-faces/bf_201/001.jpg)
218 | Ugly | 3 | ![](/assets/many-faces/bf_218/001.jpg) ![](/assets/many-faces/bf_218/002.jpg) ![](/assets/many-faces/bf_218/003.jpg)
261 | | 13 | ![](/assets/many-faces/bf_261/001.jpg) ![](/assets/many-faces/bf_261/002.jpg) ![](/assets/many-faces/bf_261/003.jpg)
273 | | 43 | ![](/assets/many-faces/bf_273/001.jpg) ![](/assets/many-faces/bf_273/002.jpg) ![](/assets/many-faces/bf_273/003.jpg)
274 | Overflow | 4 | ![](/assets/many-faces/bf_274/001.jpg) ![](/assets/many-faces/bf_274/002.jpg) ![](/assets/many-faces/bf_274/003.jpg)
284 | | 16 | ![](/assets/many-faces/bf_284/001.jpg) ![](/assets/many-faces/bf_284/002.jpg) ![](/assets/many-faces/bf_284/003.jpg)
289 | | 51 | ![](/assets/many-faces/bf_289/001.jpg) ![](/assets/many-faces/bf_289/002.jpg) ![](/assets/many-faces/bf_289/003.jpg)
402 | | 8 | ![](/assets/many-faces/bf_402/001.jpg) ![](/assets/many-faces/bf_402/002.jpg) ![](/assets/many-faces/bf_402/003.jpg)
409 | Beadnose | 73 | ![](/assets/many-faces/bf_409/001.jpg) ![](/assets/many-faces/bf_409/002.jpg) ![](/assets/many-faces/bf_409/003.jpg)
410 | Four-Ton | 77 | ![](/assets/many-faces/bf_410/001.jpg) ![](/assets/many-faces/bf_410/002.jpg) ![](/assets/many-faces/bf_410/003.jpg)
415 | | 1 | ![](/assets/many-faces/bf_415/001.jpg)
435 | Holly | 4 | ![](/assets/many-faces/bf_435/001.jpg) ![](/assets/many-faces/bf_435/002.jpg) ![](/assets/many-faces/bf_435/003.jpg)
469 | | 3 | ![](/assets/many-faces/bf_469/001.jpg) ![](/assets/many-faces/bf_469/002.jpg) ![](/assets/many-faces/bf_469/003.jpg)
480 | Otis | 131 | ![](/assets/many-faces/bf_480/001.jpg) ![](/assets/many-faces/bf_480/002.jpg) ![](/assets/many-faces/bf_480/003.jpg)
482 | Brett | 23 | ![](/assets/many-faces/bf_482/001.jpg) ![](/assets/many-faces/bf_482/002.jpg) ![](/assets/many-faces/bf_482/003.jpg)
489 | Ted | 2 | ![](/assets/many-faces/bf_489/001.jpg) ![](/assets/many-faces/bf_489/002.jpg)
500 | Indy | 5 | ![](/assets/many-faces/bf_500/001.jpg) ![](/assets/many-faces/bf_500/002.jpg) ![](/assets/many-faces/bf_500/003.jpg)
503 | Cubadult | 54 | ![](/assets/many-faces/bf_503/001.jpg) ![](/assets/many-faces/bf_503/002.jpg) ![](/assets/many-faces/bf_503/003.jpg)
505 | | 21 | ![](/assets/many-faces/bf_505/001.jpg) ![](/assets/many-faces/bf_505/002.jpg) ![](/assets/many-faces/bf_505/003.jpg)
634 | Popeye | 16 | ![](/assets/many-faces/bf_634/001.jpg) ![](/assets/many-faces/bf_634/002.jpg) ![](/assets/many-faces/bf_634/003.jpg)
700 | Marge | 4 | ![](/assets/many-faces/bf_700/001.jpg) ![](/assets/many-faces/bf_700/002.jpg) ![](/assets/many-faces/bf_700/003.jpg)
708 | Amelia | 2 | ![](/assets/many-faces/bf_708/001.jpg) ![](/assets/many-faces/bf_708/002.jpg)
719 | Princess | 19 | ![](/assets/many-faces/bf_719/001.jpg) ![](/assets/many-faces/bf_719/002.jpg) ![](/assets/many-faces/bf_719/003.jpg)
744 | Dent | 2 | ![](/assets/many-faces/bf_744/001.jpg) ![](/assets/many-faces/bf_744/002.jpg)
747 | | 20 | ![](/assets/many-faces/bf_747/001.jpg) ![](/assets/many-faces/bf_747/002.jpg) ![](/assets/many-faces/bf_747/003.jpg)
755 | Scare D Bear | 13 | ![](/assets/many-faces/bf_755/001.jpg) ![](/assets/many-faces/bf_755/002.jpg) ![](/assets/many-faces/bf_755/003.jpg)
775 | Lefty | 178 | ![](/assets/many-faces/bf_775/001.jpg) ![](/assets/many-faces/bf_775/002.jpg) ![](/assets/many-faces/bf_775/003.jpg)
813 | Nostril Bear | 3 | ![](/assets/many-faces/bf_813/001.jpg) ![](/assets/many-faces/bf_813/002.jpg) ![](/assets/many-faces/bf_813/003.jpg)
814 | Lurch | 11 | ![](/assets/many-faces/bf_814/001.jpg) ![](/assets/many-faces/bf_814/002.jpg) ![](/assets/many-faces/bf_814/003.jpg)
818 | | 1 | ![](/assets/many-faces/bf_818/001.jpg)
854 | Divot | 3 | ![](/assets/many-faces/bf_854/001.jpg) ![](/assets/many-faces/bf_854/002.jpg) ![](/assets/many-faces/bf_854/003.jpg)
856 | | 36 | ![](/assets/many-faces/bf_856/001.jpg) ![](/assets/many-faces/bf_856/002.jpg) ![](/assets/many-faces/bf_856/003.jpg)
868 | Wayne Brother | 7 | ![](/assets/many-faces/bf_868/001.jpg) ![](/assets/many-faces/bf_868/002.jpg) ![](/assets/many-faces/bf_868/003.jpg)

# What We Need

As you can see, there are quite a few bears for which we only have a couple images. We really need more images of these bears to use them for training. We think we need at least 20 good face chips per bear, preferably from different seasons and different times of the season. We're hoping the set we get from Katmai will fill out our set, but we can always you more!

We are also not sure if we can use the images where the bear is looking far to the left or right or down. We're planning a few experiments to see how the various poses effect our results. If we have to filter out some of these more extreme poses, our dataset will get even smaller.

If you have decent quality photos or videos of the Brooks Falls bears, or of any other brown bears, please contact us at bearid [at] hypraptive [dot] com or the BBRN at photos [at] bearresearch [dot] org.

We are not using any captures from the [explore.org bearcams](http://explore.org/live-cams/player/brown-bear-salmon-cam-brooks-falls) at this time, as we don't think the quality is sufficient. Hopefully, once we have the application working reasonably well, we can adapt it to work with the bearcams as well!
