---
layout: post
title:  "Solve Elasticsearch reindexing downtime problem"
date:   2017-11-09
categories: elasticsearch ruby ror rails
---

Recently we got a problem - reindexing out ES became a huge deal, it could take up to a few hours. Of course, data scheme doesn't change so often but when it did, deploy procedure took too long to be acceptable for business.
<!--more-->
Solution to this is quite simple - Aliases. Instead of pointing model to index itself, we use aliases and after reindexing just update the link. This is how index switching works (code simplified)
{% highlight ruby %}
current_index_name = model.es.index.indices.get_alias(name: model.es_index_name).keys.first
actions = { add: { index: new_index_name, alias: model.es_index_name } }, { remove: {index: current_index_name, alias: model.es_index_name} }

model.es_index_name = new_index_name
model.es.client.indices.update_aliases(body: {actions: actions})
{% endhighlight %}
So you can simply create a task to rebuild index and then activate new one but running code above. Elegant!
