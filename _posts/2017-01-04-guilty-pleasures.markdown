---
layout: post
title:  "Guilty Pleasures"
author: Ed
date:   2017-01-04 14:00:00
excerpt: "Turning a guilty pleasure into a deep learning project."
---
My partner and I have a shared guilty pleasure: we love watching wildlife on webcams. We often have a live cam from [Explore](http://explore.org/) streaming on our screens or [Chromecast](https://www.google.com/intl/en_us/chromecast/) to the TV. One of our favorite cams is [Brooks Falls Live Cam](http://explore.org/live-cams/player/brown-bear-salmon-cam-brooks-falls) from [Katmai National Park](https://www.nps.gov/katm), Alaska. In spring and summer, Brooks Falls sees one of the highest concentrations of brown bears in the world. During the [heart of the season](https://www.nps.gov/katm/learn/photosmultimedia/brown-bear-frequently-asked-questions.htm#11), you can sit and watch dozens of bears fishing at the falls:

![Brooks Falls](/assets/brooks-falls.jpg){: figure }

If passively watching is not enough, you can join the discussion on the Explore page and join in the various ranger talks. You will quickly learn that each of the bears have been assigned a number by the rangers, and some of them have nicknames. Pretty soon you will start to recognize some of the individual bears, especially the fan favorites, like 480 Otis:

![480 Otis](/assets/480otis.jpg){: figure }

But I don't know all the bears and I certainly can't tell them all apart. It would be cool if I can find out which bears I'm watching on the cam, or who I just captured in a [snaphot](http://blog.explore.org/snapshots/). The Explore community is very helpful. Often someone in the community has identified which bears are on camera and posted in the comments. But even the experts have difficulty telling the bears apart. Could machine learning do any better?

Hang on a minute. I know that CNNs can distinguish, for example, between a brown bear and a polar bear. That's already part of the ImageNet data set. But can we train a machine to tell, say, [480 Otis](https://www.flickr.com/photos/katmainps/galleries/72157634850500991/) from [435 Holly](https://www.flickr.com/photos/katmainps/galleries/72157634823125686/)?

We found our project. We would attempt to develop an application which could identify the individual bears we see on the Brooks Falls live cam. To begin, we had to start answering the following questions:

* Who are the bears of Brooks Falls?
* How do **we** tell one bear from another?
* Has this already been done?
* What tools already exist that we can make use of?

We will begin to explore these and other questions in the coming blogs.
