---
layout:     post
title:      Map making in the web - making cities pop!
date:       2018-04-18 09:06:29
summary:    This post explains how you can use LeafletJS to clip map tile layers and make boundaries stand out.  
categories: tutorials
---

When designing maps for our projects here at KLL, a very common request that we receive in the early stages of development of any map-based app, is to make the geographical area that is the focus of the project stand out.

In this post, I am going to walk you through a series of steps that will allow you to clip the standard OSM tilelayer based on a geographic boundary.

### So what are we doing again?
Here is an image that showcases what we are trying to achieve by the end of this tutorial.

![]({{ "/assets/img/boundary.png" | absolute_url }})
*Notice how areas outside the city has a reduced opacity, allowing us to draw the user’s attention to all of the content inside the boundary.*

### Before we begin

This tutorial assumes a basic understanding of [LeafletJS]("http://leafletjs.com/") and its API. If you are not familiar with this framework, I urge you to go through its [well curated collection of  tutorials]("http://leafletjs.com/examples.html") and [API reference documentation]("http://leafletjs.com/reference-1.3.0.html").

I have also uploaded all of the resources used for this tutorial in the form of a github gist. You can view the code [here]("#").


### So let's get going.

We first begin by instantiating our map in `index.html`.

{% highlight html %}
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>Making Cities Pop - Final Output</title>
  </head>
  <body>
  </body>
</html>
{% endhighlight %}



For the purposes of this tutorial, we will be a GeoJSON file that contains the boundary for Neelakantha Municipality, Dhading.
