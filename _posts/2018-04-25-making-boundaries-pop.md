---
layout:     post
title:      Making city boundaries pop out in maps.
date:       2018-04-18 09:06:29
summary:    This post explains how you can use LeafletJS to clip map tile layers and make boundaries stand out.  
categories: tutorials
---

When designing maps for our projects here at KLL, a very common request that we receive in the early stages of development of any map-based app, is to make the geographical area that is the focus of the project stand out.

In this post, I am going to walk you through a series of steps that will allow you to clip the standard OSM tilelayer based on a geographic boundary.

Before we begin, here is an image that showcases what we are trying to achieve by the end of this tutorial.

![Notice how areas outside the city has a reduced opacity, allowing us to draw the user’s attention to all of the content inside the boundary.]({{ "/assets/img/boundary.png" | absolute_url }})

For the purposes of this tutorial, we will be a GeoJSON file that contains the boundary for Nilkantha municipality, Dhading.
