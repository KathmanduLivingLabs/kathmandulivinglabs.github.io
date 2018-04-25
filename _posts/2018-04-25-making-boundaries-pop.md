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

Let's start by quickly wiring up a basic leaflet map for our use. For this, we will be following the same procedure as outlined in Leaflet's official [quick start guide]("http://leafletjs.com/examples/quick-start/"), with the following differences:

  - The bounding box and the zoom level will be set to around that of Neelakantha municipality.
  - The tilelayer that we will be using will be different to the one provided in the guide.

#### Step 1: Wiring up a basic map
{% highlight html %}
<!DOCTYPE html>
<html lang="en" dir="ltr">

<head>
    <meta charset="utf-8">
    <!-- Loading leaflet JS styles and JS -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.1/dist/leaflet.css" integrity="sha512-Rksm5RenBEKSKFjgI3a41vrjkw4EVPlJ3+OiI65vTjIdo9brlAacEuKOiQ5OFh7cOI1bkDwLqdLw3Zg0cRJAAQ==" crossorigin="" />
    <script src="https://unpkg.com/leaflet@1.3.1/dist/leaflet.js" integrity="sha512-/Nsx9X4HebavoBvEBuyp3I7od5tA0UzAxs+j83KgC8PU0kgB4XiK4Lfe4y4cgBtaRJQEIFCW+oC506aPT2L1zw==" crossorigin=""></script>
    <!-- End loading Leaflet JS -->
    <title>Making Cities Pop - Final Output</title>
</head>

<body>
    <!-- Create a div where the map will reside -->
    <div id="my-map" style="height:180px;"></div>
    <script>

        var mymap = L.map('my-map').setView([27.89512, 85.1], 11);
    </script>
</body>

</html>
{% endhighlight %}

At this point, I'd like to point out that since most of the code we will be working on will be inside the `<script>` tags inside the `<body>`, I'll only be sharing snippets from that section, and ignore the rest of the HTML.

Before we move on, here's a screenshot of what the output currently looks like:
![]({{ "/assets/img/scr_1.png" | absolute_url }})

As you may have noticed, not much has happened so far.

#### Step 2: Add the base tile layer

Inside the script tag, we now create a new tile layer and add it to the map as follows.

{% highlight html %}
...

<script>
    var mymap = L.map('my-map').setView([27.89512, 85.1], 11);

    var osmURL = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
    var baseTileLayer = L.tileLayer(osmURL, { opacity: 0.4 });
    baseTileLayer.addTo(mymap);
</script>

...
{% endhighlight %}

Notice how I've set the opacity of `baseTileLayer` to 40%. Here's what the output looks like now:
![]({{ "/assets/img/scr_2.png" | absolute_url }})

#### Step 3: Loading the external GeoJSON boundary.

The next step involves making the GeoJSON boundary file available for use within our `index.html`. For this we will have to make use of an external library called leaflet ajax. To do so, we simply load the script onto the head section of our document, like so:

{% highlight html %}
...
<head>
  ...
  <script src="/leaflet-ajax.min.js"></script>
  ...
</head>
...
{% endhighlight %}
