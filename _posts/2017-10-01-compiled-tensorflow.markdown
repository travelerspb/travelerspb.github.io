---
layout: post
title:  "Compiled Tensorflow"
date:   2017-10-01
categories: tensorflow machine learning
---
Yesterday changed my backend to tensorflow and noticed a bunch of warning like
"The TensorFlow library wasn't compiled to use SSE.." 

Hm, I don't usually run computation on local machine, I use GPU on Google Cloud, but its always nice to spend less time while doing quick model analysis.
<!--more-->
Whole [compilation process][compilation process] did take about 15 minutes, quite easy. I didn't make any complex performance tests, but here is my VGG16 quick run example:


Before: 

1409/1409 [==================] - 627s   
368/368 [====================] - 171s  

After:

1409/1409 [==================] - 361s   
368/368 [====================] - 91s 

It's works 2x times faster now. For free! :)