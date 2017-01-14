---
layout: post
title:  "Deep Learning in the Wild"
author: Ed
date:   2017-01-13 14:00:00
excerpt: "A brief overview of existing deep learning and computer vision projects aimed at identifying animals in the wild."
---
Before we jumped in to this brown bear identification project, we needed to figure out what already been done. It turns out there are a number of animal identification projects and research papers out there. So far we have not found anything immediately suitable for brown bears.

### Wildbook

One project we ran across, which on the surface seemed very promising, was the [University of Manitoba Polar Bear Whiskerprint Project](http://www.polarbearlibrary.org/). This aim of this project is to identify individual polar bears (Ursus maritimus) from user submitted photos and videos. As far as we can tell, the project uses a pattern recognition algorithm on the polar bear's whisker spots or facial scars. The following is an example from their page, ["Photographing a polar bear"](http://www.polarbearlibrary.org/photographing.jsp):

![Polar Bear Whisker Spots](/assets/dl-in-the-wild/whisker-spots.jpg)

We have seen academic papers on just this topic, such as Carlos Anderson's 2007 paper, ["Individual Identification of Polar Bears by Whisker Spot Patterns"](http://etd.fcla.edu/CF/CFE0001671/Anderson_Carlos_J_200705_MS.pdf). While brown bears also have these facial features, we don't believe they are sufficiently visible due to low contrast with their darker fur.

We did some further investigation on [Wildbook](http://www.wildbook.org/), which is "an open source software framework to support collaborative mark-recapture, molecular ecology, and social ecology studies, especially where citizen science data needs to be incorporated and managed." It is developed by [Wild Me](http://www.wildme.org/), a non-profit organization. A number of projects are using Wildbook for species such as seals, sharks, cheetahs and whales. Like the polar bears, all of these projects seem to be performing identification based on patterns in the fur, skin, tail, etc.

![IBEIS](/assets/dl-in-the-wild/ibeis-logo.png){:align="left" style="margin-right:20px; margin-bottom:0px;"} The computer vision layer of Wildbook is the [Image-Based Ecological Information System](http://www.ibeis.org/) (IBEIS). According to the IBEIS [Science/Technology page](http://ibeis.org/wordpress/science/), the current release of Wildbook is Version 6. Image analysis for Version 6 is based on [HotSpotter](https://github.com/Erotemic/hotspotter), which is itself based on [stripespotter](https://code.google.com/archive/p/stripespotter/). As previously suspected, these projects focus on matching patterns, like stripes and spots (see the [HotSpotter paper](http://homepages.rpi.edu/~crallj/crall-hotspotter-wacv-2013.pdf)). However, Wildbook Version 7 will start to identify facial characteristics and environmental context. It is supposed to beta in June 2017.

Wildbook Version 7 sounds promising for our brown bear project, so we will definitely keep an eye on their [GitHub repo](https://github.com/WildbookOrg).

### Lion Identification Network of Collaborators

![LINC](/assets/dl-in-the-wild/linc-faces.png)

[Lion Identification Network of Collaborators](http://www.linclion.org/) (LINC) is another interesting project we have come across. LINC is "an open source shared database and facial recognition system that allows researchers and conservationists the ability to monitor lions across broad landscapes." The fact that they are using facial recognition software for lion identification sounds very interesting. They are using a [HAAR classifier](https://en.wikipedia.org/wiki/Haar-like_features) to detect lion faces then a neural network running in [Caffe](http://caffe.berkeleyvision.org/) for facial recognition. This is similar to the method we have been considering for brown bears. The project is open source as well ([LINC on GitHub](https://github.com/linc-lion)).

It's not clear if the method LINC is developing can work directly for brown bears as well. Presumably we would have to retrain both the face detection classifier and the facial recognition network. It is also likely that for brown bears, we may need to include more of the head since there may not be sufficient data in a close face crop. We anticipate that the ears will be a key marker for the brown bears. We have reached out to the development team, [IEF R&D](http://iefrd.com/), to see how we can get involved.

### Other Projects

![SAISBECO Screen Shot](/assets/dl-in-the-wild/SAISBECO.png)

Some other projects we are looking into include:

* [Semi-Automated Audiovisual Species and Individual Identification System for Behavioral Ecological Research and Conservation](https://www.idmt.fraunhofer.de/en/institute/projects_products/projects/expired_publicly_financed_research_projects/saisbeco.html) (SAISBECO) - A Fraunhofer Institute project to identify great ape individuals from audio and video data (screenshot shown above).
* [**WILD**LABS.NET](https://www.wildlabs.net/) - A community for sharing information, ideas, tools and resources to discover and implement technology-enabled solutions to some of the biggest conservation challenges facing our planet.
* [deepsense.io's Right Whale Recognition](https://deepsense.io/deep-learning-right-whale-recognition-kaggle/) - The winner of a NOAA Fisheries sponsored [Kaggle contest](https://www.kaggle.com/c/noaa-right-whale-recognition).
* [WildTrack](http://wildtrack.org/) - Non-invasive wildlife monitoring through Footprint Identification Technology.
* [Biometric Recognition for Pet Animal](http://file.scirp.org/pdf/JSEA_2014052809540892.pdf) - Academic paper on the use of facial recognition for recognizing dogs.
* [Tracking Animals in Wildlife Videos Using Face Detection](https://pdfs.semanticscholar.org/90bc/f0af3d7e9fbc99c76e2b66f4d40dfb1fc42d.pdf) and [Analysing Animal Behaviour in Wildlife Videos Using Face Detection and Tracking](http://epubs.surrey.ac.uk/531566/1/revised_burgcalic_02.pdf) - A pair of papers from the University of Bristol on the use of face detection for tracking and analyzing wildlife.

I'm sure there will be more projects in this space soon. I mean, you know it's getting popular when [NVIDIA blogs about it](https://blogs.nvidia.com/blog/2016/11/04/saving-endangered-species/).
