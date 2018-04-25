---
layout:     post
title:      Making cities pop!
date:       2018-04-18 09:06:29
summary:    A small tutorial that explains how you can clip map tile layers based on an external GeoJSON boundary in Leaflet.
categories: tutorials
---

*A small tutorial that explains how you can clip map tile layers based on an external GeoJSON boundary in Leaflet.*

When designing maps for our projects here at KLL, a very common request that we receive in the early stages of development of any map-based app, is to make the geographical area that is the focus of the project stand out.

In this post, I am going to walk you through a series of steps that will allow you to clip the standard OSM tilelayer based on a geographic boundary.


### So what are we doing again?

Here is an image that showcases what we are trying to achieve by the end of this tutorial.

![]({{ "/assets/img/scr_4.png" | absolute_url }})
*Notice how areas outside the city has a reduced opacity, allowing us to draw the user’s attention to all of the content inside the boundary.*


### Before we begin

This tutorial assumes a basic understanding of <a href="http://leafletjs.com/">LeafletJS</a> and its API. If you are not familiar with this framework, I urge you to go through its <a href="http://leafletjs.com/examples.html">well curated collection of  tutorials</a> and <a href="http://leafletjs.com/reference-1.3.0.html">API reference documentation</a>.

I have also uploaded all of the resources used for this tutorial in the form of a github gist. You can view the code <a href="http://bl.ocks.org/arkoblog/1a0b65bd62686bab0d8a7ccca26be998">in this github gist.</a>


### Step 1: Wiring up a basic map

Let's start by quickly wiring up a basic leaflet map for our use. For this, we will be following the same procedure as outlined in Leaflet's official <a href="http://leafletjs.com/examples/quick-start/">quick start guide</a>, with the following differences:

  - The bounding box and the zoom level will be set to around that of Neelakantha municipality.
  - The tilelayer that we will be using will be different to the one provided in the guide.

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
      <div id="my-map" style="height:400px;"></div>
      <script>

          var mymap = L.map('my-map').setView([27.89512, 85.1], 11);
      </script>
  </body>

</html>
{% endhighlight %}

Before we proceed, here's a screenshot of what the output currently looks like:

![]({{ "/assets/img/scr_1.png" | absolute_url }})
As you may have noticed, not much has happened so far.


### Step 2: Adding the base tile layer

Inside the script tag, we now create a new tile layer and add it to the map as follows.

{% highlight html %}
...

<script>
  var mymap = L.map('my-map').setView([27.89512, 85.1], 11);

  var osmURL = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
  var baseTileLayer = L.tileLayer(osmURL, { opacity: 0.2 });
  baseTileLayer.addTo(mymap);
</script>

...
{% endhighlight %}

Notice how I've set the opacity of `baseTileLayer` to `0.2`. Here's what the output looks like now:
![]({{ "/assets/img/scr_2.png" | absolute_url }})


### Step 3: Loading the external GeoJSON boundary.

The next step involves making the GeoJSON boundary file available for use within our `index.html`. For this we will have to make use of the `$.ajax()` method available in jQuery. To do so, we first load jQuery as an external dependency onto the head section of our document, like so:

{% highlight html %}
...
<head>
  ...
  <script src="https://code.jquery.com/jquery-2.2.4.js"></script>
  ...
</head>
...
{% endhighlight %}

After this, we can now access the GeoJSON as follows:

{% highlight html %}
...

<script>
  var mymap = L.map('my-map').setView([27.89512, 85.1], 11);
  var osmURL = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
  var baseTileLayer = L.tileLayer(osmURL, { opacity: 0.4 });
  baseTileLayer.addTo(mymap);


  $.ajax({mimeType: 'application/json', url: 'boundary.geojson'} ).done(function(data) {
    console.log(data)
  });
</script>

...
{% endhighlight %}


### Step 4: Making it pop!

The final step involves adding one more tilelayer onto the original map. However, in this case, the tile layer will only be visible inside the boundary. This is achieved my making use of an external leaflet plugin called 'BoundaryCanvas', which allows us to draw tiled raster layers with an arbitrary boundary (in our case, `boundary.geojson`). You can learn more about its capabilities <a href="https://github.com/aparshin/leaflet-boundary-canvas">here</a>.

We begin by loading the boundary canvas script within the head section of `index.html`.

{% highlight html %}
...
<head>
  ...
      <script src="https://unpkg.com/leaflet-boundary-canvas@1.0.0/src/BoundaryCanvas.js"></script>
  ...
</head>
...
{% endhighlight %}

Finally, we add the additional tile layer inside the `$.ajax()` call as follows:

{% highlight html %}
...

<script>

  var mymap = L.map('my-map').setView([27.89512, 85.1], 11);
  var osmURL = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
  var baseTileLayer = L.tileLayer(osmURL, { opacity: 0.2 });
  baseTileLayer.addTo(mymap);

  $.ajax({mimeType: 'application/json', url: 'boundary.geojson'} ).done(function(data) {
    var test = L.TileLayer.boundaryCanvas('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        boundary: data,
    }).addTo(mymap);
  });

</script>

...
{% endhighlight %}

If all goes well, here's what you will see:
![]({{ "/assets/img/scr_3.png" | absolute_url }})

To make the municipality stand out a little more, let's modify the leaflet container's background color. To do this, let's add a style tag inside the `<head>` section of `index.html`

{% highlight html %}
...
<head>
  ...
  <style>
     .leaflet-container {
       background: #000;
     }
  </style>
  ...
</head>
...
{% endhighlight %}

In the end, this is what we should have:
![]({{ "/assets/img/scr_4.png" | absolute_url }})

Cheers,
Arogya
