---
layout: post
title:  "OnComplete callbacks in Deepleaning frameworks"
date:   2017-10-14
categories: tensorflow machine learning
---

I was thinking the other day, it would be very nice to have callback in various time-consuming functions. Especially its helpful for indie or hobby researchers, who have to spend they own money on cloud VM with GPU.
<!--more-->
Something like

{% highlight ruby %}
send_me_sms = lambda : service.send_sms()
model.fit(data, labels, on_complete=send_me_sms)
{% endhighlight %}

would be great to have.
