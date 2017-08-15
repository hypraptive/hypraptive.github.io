---
layout: post
title:  "Bear Face Chips From Videos"
author: Ed
date:   2017-04-21 16:00:00
excerpt: "Extending the bear face dataset by extracting face chips from videos."
---
For the past few weeks our main focus has been on building up our image dataset for the brown bears. We have been following up on a few leads, including Katmai National Park, which we think will result in fairly large collections of images and possibly videos. While we're working on getting this content, we extended our `bearchip` software to extract bear face chips from videos.

![Bear Face Chips](/assets/bearid-video-chips.png){: figure }

To achieve this we need to

* open a video file
* decode each frame to an image
* pass the image to our existing `bearchip` face extractor

It turns out this is fairly easy to do using the [OpenCV](http://opencv.org/) VideoCapture class. Once we include the appropriate OpenCV headers and libraries in our project, we can open a video file like this:

```
cv::VideoCapture cap(<VIDEO_FILE>);
```

With the video opened as `cap`, we can extract a frame using `cap.read()`. There is a dlib function, `assign_image`, which converts from the OpenCV image format to the dlib image format. Once we have a dlib image, we can pass it to our face detector and shape predictor (for which we are still using the pre-trained networks from the [dog hipsterizer](https://hypraptive.github.io/2017/02/24/bear-chipsterizer.html) example) and write out the face chips. We loop through the video until the file is no longer open or `cap.read()` fails to read the next frame. We keep track of the frame number so we can map the face chips back to the correct frame in the video. Our loop looks something like this:

```
int frame_num = 0;
while (cap.isOpened())
{
  cv::Mat temp;
  if (!cap.read(temp)) break;
  assign_image(img, cv_image<bgr_pixel>(temp));
  [... do the face extraction stuff and save the chips]
  frame_num++;
}
```
That's all there was to it!

### Next Steps

Our top priority is still **get more data!**

Now that `bearchip` can extract bear face chips from videos, we have started downloading videos of the Brooks Falls bears from the Internet. We need to make sure the bears are accurately identified. We also need to run some experiments to see if the similarity between chips extracted from a given video causes a data bias. If all works out, this should be a good way to grow our dataset more quickly.

We are also improving our testing methodology and metrics, so we can better compare different approaches. We need to make sure we are doing random splits of our dataset to create training, test and cross-validation sets. We also need to calculate metrics for each phase of the pipeline (detection, reorienting, encoding and recognition) as well as the end to end process.

One approach we are considering was method developed by the  [LemurFaceID](https://bmczool.biomedcentral.com/articles/10.1186/s40850-016-0011-9) project, which uses patch-wise Multi-scale [Local Binary Pattern](https://en.wikipedia.org/wiki/Local_binary_patterns) features for the embedding, rather than training a deep CNN to create embeddings. Their project seems to achieve fairly good results for lemur faces with a lot less training data, but it is not clear if the method will work as well on the more uniform brown bear faces. We will have to try it to find out.

Until next time, **SBD**
