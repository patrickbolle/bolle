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

<script src="https://gist.github.com/patrickbolle/fede359891ae5e7b19f1bd6df1427c01.js"></script>

\
This is a decent amount of code but the logistics of it are super simple.

Below is the section settings schema. Here I implement two different 'types' of blocks, one is 'block-1' (left banner) and the other is 'block-2' (right banner). They both have identical settings in this, but you can have whichever settings for whichever block you want.

```
{% schema %}
{
  "name": "Double Hero Section Slider",
  "blocks":
  [
    {
      "type": "block-1",
      "name": "3/4 Slider (Left)",
      "settings": [
        {
          "id": "hero_banner",
          "type": "image_picker",
          "label": "3/4 Image"
        },
        {
          "id": "hero_link",
          "type": "url",
          "label": "Hero Link"
        }
      ]
    },
    {
      "type": "block-2",
      "name": "1/4 Slider (Right)",
      "settings": [
        {
          "id": "weekly_banner",
          "type": "image_picker",
          "label": "1/4 Image"
        },
        {
          "id": "weekly_link",
          "type": "url",
          "label": "Weekly Link"
        }
      ]
    }
  ],
  "presets": [
    {
      "category": "Advanced content",
      "name": "Double Block Slider"
    }
  ]
}
{% endschema %}
```

In the actual Liquid / HTML code, all we have to do is run a quick loop through the blocks and then single out each block that corresponds with what we want. 

On the left side of the page I use this following code to grab only blocks that are the type 'block-1' : 
```
{% for block in section.blocks %}
        {% if block.type == 'block-1' %}
          <div class="hero-image-inner" style="background-image: url({{ block.settings.hero_banner | img_url: '2048x2048'}});">
          </div>
        {% endif %}
{% endfor %}
```

And then on the right side of the page, we do the exact same thing, but referencing the 'block-2' types : 
```
{% for block in section.blocks %}
      {% if block.type == 'block-2' %}
        <img src="{{ block.settings.weekly_banner | img_url: '750x' }}">
      {% endif %}
{% endfor %}
```

In the end, it translates to a relatively easy to use format for a client to use double blocks within the theme editor (though I wish I could make it work a bit easier for them). This is what the section now looks like in the drag-n-drop section editor : 

![Double Shopify Section Image](/images/double-block-editor.png)

Hope that helps someone down the road, it took me a while to figure this out but it's a handy code snippet to have around. 

Let me know if you have any questions by clicking the contact page in the top right hand corner.

Thanks!
Patrick
