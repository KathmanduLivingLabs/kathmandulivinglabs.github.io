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

For the purposes of this tutorial, we will be a GeoJSON file that contains the boundary for Nilkantha municipality, Dhading.

![Notice how areas outside the city has a reduced opacity, allowing us to draw the user’s attention to all of the content inside the boundary. ]({{ "https://photos-4.dropbox.com/t/2/AAAJuE92c23rn16YoJ9VQtDMxMVodvc3IraX9di4sj0f5A/12/209875859/png/2048x1/5/1524672000/0/10/image.png/_/png%2520https%253A%252F%252Fd2mxuefqeaa7sj.cloudfront.net%252Fs_479BF4A1516B4B8B69A45EE7942917D18732F6625ABC8A67D1FEDD3AC3A21C88_1523432008536_image.png?preserve_transparency=1&size=2048x1&size_mode=5 | absolute_url }})
