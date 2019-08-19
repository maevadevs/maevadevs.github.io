---
layout: post
title: How To Configure Apache Proxy To Redirect Route Handles To NodeJS
category: NodeJS
tags: [configuration, nodejs, apache, proxy, proxypass, routing, redirect]
---

When you need to have Apache and NodeJS to work in coordination, this setting allows a specific root route (e.g. `/nodeapp`) on a mainly Apache Server to be redirected and handled by a NodeJS microserver instance instead.

---

Let's assume that the endpoint root route on Apache that we want to be handled by NodeJS is at `https://mydomain.com/nodeapp`, and that everything else under `mydomain.com` should be handled by Apache.

We can use Apache's `ProxyPass` directive to make this setup work

1. In Apache `httpd.conf`, add the following line:

{% highlight sh %}
ProxyPass /nodeapp http://localhost:8080/
{% endhighlight %}

2. Make sure the following lines are **not** commented out for the proxy setting in `httpd.conf`:

{% highlight sh %}
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so
{% endhighlight %}

3. Run the NodeJS server instance on port 8080

{% highlight js %}
const express = require('express')
const PORT = 8080
const app = express()
app.get('/', (req, res) => res.send('Hello from Node within Apache!')
app.listen(PORT, () => `Express is up on port ${PORT}...`)
{% endhighlight %}

4. Access all NodeJS instance logic at the endpoint: `http://mydomain.com/nodeapp`

{% comment %}
=======================
The purpose of this snippet is to list all the tags you have in your site.
=======================
{% endcomment %}
{% for tag in tags %}
	<a href="#{{ tag | slugify }}"> {{ tag }} </a>
{% endfor %}
