---
layout: post
title:  "Fastest (?) Rail Serializer "
date:   2018-02-01
categories: rails ror ruby gems json
---
On one of my current projects we have a few objects that are massive. Why is it happened its another question, but accepting the fact that we have those long blocking calls, its been a headache to handle with. Not that critical to spend a lot of time to redesign the architecture (its an old and low budget project), but still making the works isn't better place.
<!--more-->

Long story short, I found link to a new Netflix library in my Twitter flow [https://github.com/Netflix/fast_jsonapi](https://github.com/Netflix/fast_jsonapi). Hm, we all like libraries from big companies, worth to give a try.

The changes to model were barely noticeable:
{% highlight ruby %}
include FastJsonapi::ObjectSerializer
{% endhighlight %}
Result? I deployed the changes to staging environment, and run simple performance tests. Average response time decreased from 2,3 sec to 1,6 and CPU load from 26% down to 22%. Not bad for 10 minutes of work!

Highly recommended.
