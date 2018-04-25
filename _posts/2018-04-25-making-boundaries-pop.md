---
layout:     post
title:      Map making in the web: making cities pop!
date:       2018-04-18 09:06:29
summary:    This post explains how you can use LeafletJS to clip map tile layers and make boundaries stand out.  
categories: tutorials
---

When designing maps for our projects here at KLL, a very common request that we receive in the early stages of development of any map-based app, is to make the geographical area that is the focus of the project stand out.

In this post, I am going to walk you through a series of steps that will allow you to clip the standard OSM tilelayer based on a geographic boundary.

Before we begin, here is an image that showcases what we are trying to achieve by the end of this tutorial.

![]({{ "/assets/img/boundary.png" | absolute_url }})
*Notice how areas outside the city has a reduced opacity, allowing us to draw the user’s attention to all of the content inside the boundary.*

For the purposes of this tutorial, we will be a GeoJSON file that contains the boundary for Neelakantha Municipality, Dhading. If you don't understand what that means just yet, there's no need to worry, just follow along and we'll have you ramped up in not time.


### Understanding leaflet.

This section is written for users who have no familiarity with Leaflet. If you already have a basic understanding of what LeafletJS is and what it does feel free to skip this section.


### Basic Principle

Regardless of whether you;re using Leaflet or any other framework (MapboxGL, for example), the basic idea is to add an additional layer in the map, which would be a difference between the GeoJSON and the map’s bounding box, and play with the opacity of these two layers to achieve the desired effect.
