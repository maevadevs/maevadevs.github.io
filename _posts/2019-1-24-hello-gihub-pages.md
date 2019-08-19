---
layout: post
title: Hello Github Pages, Jekyll, and world!
category: Blog
tags: [jekyll, jekyll-now]
---

As the post title suggests, this is my first post for my Github pages. My intent with this page is to keep it as a very simple side blog for my programming activities.

---

So for this *"Hello World"* post, I will simply explain what I did to get this blog started in a matter of 5 minutes. The setup steps for Github pages using Jekyll were pretty straightforward and well documented in my opinion.

1. Log into your Github account and fork the [Jekyll-Now original repo](https://github.com/barryclark/jekyll-now), then rename it as `yourgithubusername.github.io`

1. Next, Update your site name, avatar and other options using the `_config.yml` file in the root of your repository. The configuration file is commented out so very easy steps.

![_config.yml]({{ site.baseurl }}/images/jekyll-yml-config.png)

3. Then edit the first post to see how the changes are affected. You can also create new posts by simply creating a new `.md` file in the post. Just make sure to include the *front-matter block* at the top of each new blog post and make sure the post's filename is in this format: `year-month-day-title.md`

That's it!
