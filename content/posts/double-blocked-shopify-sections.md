---
title: Double-Blocked Sections in Shopify
featured: true
thumbnail: /images/uploads/screenshot_2018-08-01-haago-hand-warmers.png
date: '2018-06-05T10:13:27-04:00'
---
A while back I was building out a slider component on a client's Shopify store. In general, sliders/carousels are dead simple once you get the gist of it, but the challenge with this specific slider was that the client wanted two different 'sides' of the carousel, and wanted to be able to edit each. 

Basically, both the 3/4 image (left) and the 1/4 image (right) are independent sliders, but edited from within the same Shopify section.

Here is an image of what it looks like, to give you a better idea of the section :

![Double Shopify Section Image](/images/double-block.png)

Upon some research I found that this is... not really supported by Shopify sections. Sections are meant to be code blocks that don't really mesh with one another, so this double section concept was a little bit out of the original section scope. 

Determined to sort this out I stitched together a few different Shopify forum threads and came up with the following solution (excluding the slider code itself, of course. I believe I used Slick Carousel for this site specifically) :

<script src="http://gist-it.appspot.com/https://github.com/patrickbolle/shopify-snippets/blob/master/double-block-section.liquid"></script>
