---
layout: post
title:  "Easy cron jobs with Rails"
date:   2017-10-14
categories: rails ror ruby cron gems
---
In our app we use Sidekiq for async operations, like sending email and etc. However, some tasks has to be done regularly and might take a lot of time to accomplish. For those ones we use gem clockwork in very simply way.
<!--more-->
Config file is pretty straightforward, like:
{% highlight ruby %}
Dir[Rails.root.join('app', 'jobs', 'clockworks', '*.rb')].each { |file| require file }
module Clockwork
  handler do |_|
    yield
  end
...
{% endhighlight %}
This let us keep tasks separate from config.

Task looks like this:
{% highlight ruby %}
module Clockwork
  every(1.week, 'delete.archived.pages', :at => '00:00') { archive_page_job }
  def self.archive_page_job
    // do the magic here
  end
end
{% endhighlight %}
I found this way is the best possible to solve cron jobs organising. No need to configure it separately on server/Heroku panel, very easy and loose coupled code to maintain.