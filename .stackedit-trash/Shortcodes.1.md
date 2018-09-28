
Shortcodes are simple ways to get additional interactive elements into our stories.

The benefit of using shortcodes is that our users are empowered to think with interactivity in mind, and it is relatively easy to integrate into the NewsGate-to-Django workflow.

Additionally, incorrect shortcodes do not create template issues, they simply do not appear.

**Caveat: Some of these shortcodes have not been tested or used recently, and may require additional tweaks/fixes**

# Available shortcodes

Most of these shortcodes require some preparation beforehand in order to be used properly in NewsGate.

 1. Teasers
 2. Video
 3. Audio
 4. Document
 5. Photo
 6. Photoset
 7. Phototile
 8. 360 Photo  
 9. Vertical Photo
 10. Longform photo 
 11. Then and Now
 12. Mug
 13. Timeline
 14. Embed
 15. Graphic
 16. Graphic set
 17. Pie chart
 18. Bar chart
 19. Line chart
 20. Special sections
 21. Genericlink

## How to use them in NewsGate

In the following sections we'll cover the specific shortcodes and how to use them, but generally speaking for NewsGate use, you will need to write the shortcode, highlight it, and select `mm_shortcode`

For example, if I were embedding a photo in the story, I would do this:
`[photo id=4257834]`, highlight/select it, and choose `mm_shortcode`. It should change the color of it to a shaded light blue.

It is possible to just use shortcodes in Django, but it's not recommended as it will break the connection between NewsGate and Django (or disable easy updates).

## Teasers

Teasers will embed a small box in the story with a photo, headline and teaser text to a different story.

It's useful when we're running related stories, or a series of stories, and we wish to drive attention to additional stories.

**Requirement(s)**
1. Teaser stories must already be in Django with an available Story ID

Example of usage, if wishing to tease to two stories:
 - ``[teasers ids=844380,844309]``

## Video

Similar to the Youtube shortcode, except this lets us embed any video that is in our Django CMS. This includes externally linked videos such as Vimeo, Youtube or even Facebook.

**Requirement(s)**
1. Django video ID

Example of usage:
 - ``[video id=3456888]``

## Audio

Much like the Video shortcode, except this is for us to embed audio files that are in our Django CMS.

**Requirement(s)**
1. Django audio ID

Example of usage:
 - ``[audio id=2363]``

## Document

This lets us embed documents in our Django CMS. 

**Requirement(s)**
1. Django document ID
2. Document requires a description

Example of usage:
 - ``[document id=10126]``

## Photo

When you want to embed a single photo in a story.

**Requirement(s)**
1. Django photo ID
2. Photo requires a caption

Example of usage:
 - ``[photo id=471520]``

## Photoset

Photoset, aka galleries, can be embedded in a story when we have multiple galleries running.

**Requirement(s)**
1. Django photoset ID
2. Gallery requires title/headline

Example of usage:
 - ``[photoset id=6816]``

## Phototile

You can create a phototile made of three horizontal photos. The first item will be large, with the following two other smaller.

**Requirement(s)**
1. Django photo IDs
2. Photos require captions

Example of usage:
 - ``[phototile ids=123,456,789]``
 - http://www.spokesman.com/stories/2017/sep/03/wet-spring-and-summers-heat-deliver-mixed-wheat-ha/
  
 
## Then and Now/Before and After

This lets you create a then-and-now slider with two photos.

**Requirement(s)**
1. Django photo ID for the "before" and "after" photo
2. Photos should have captions

Example of usage:
 - ``[thennow before=479478 after=482687]``


## Mugs

This embeds a mug shot.

**Requirement(s)**
1. Django photo ID
2. Float direction (left or right)

Example of usage:
 - ``[mug id=481936 float=right]``

## Vertical photo

This embeds a vertical photo.

**Requirement(s)**
1. Django photo ID
2. Photo caption
3. Float direction (left or right)

Example of usage:
 - ``[vertical_photo id=481935 float=right]``

## Longform photo

This embeds a photo with additional styling. It enlarges the photo across the entire screen width.

**DO NOT** use on normal stories, use this only with longform stories.

**Requirement(s)**
1. Django photo ID

Example of usage:
 - ``[longform_photo id=475912]``
 - [Amazon brings its order fulfillment machine to Spokane](http://www.spokesman.com/stories/2018/jul/28/amazon-brings-its-order-fulfillment-machine-spokan/)

## Timelines

This embeds a timeline into the story

**Requirement(s)**
1. Timeline ID

Example of usage:
- ``[timeline id=33]``
- [25 years after Ruby Ridge, our divisions have grown](http://www.spokesman.com/stories/2017/aug/20/25-years-after-ruby-ridge-our-divisions-have-grown/)

## Embeds

This embeds an embed. Embeds are typically used for iframes, but do be careful - you can put **anything** in these. This means you could break the story page if you're not careful.

**Requirement(s)**
1. Embed ID

Example of usage:
- ``[embed id=33]``
- [Trump promises a ‘real book’ on his White House](http://www.spokesman.com/stories/2018/sep/10/trump-promises-a-real-book-on-his-white-house/)

## Graphics

This embeds a graphic item. If they're **not** in svg format, they will slide into the page with animation. The "swoosh" effect as Megan Rowe calls it.

**Requirement(s)**
1. Graphic ID

Example of usage:
- ``[graphic id=33]``
- [WSU anticipates revenue boost from partnership with international student recruiter](http://www.spokesman.com/stories/2018/sep/02/with-an-eye-to-its-bottom-line-wsu-turns-to-privat/)

## 360 photos

This embeds a teaser to a 360 photo.

**Requirement(s)**
1. 360 Photo ID

Example of usage:
- ``[photo360 id=17]``
- [Spokane’s urban explorers look for the humanity in abandoned places, but there are risks](http://www.spokesman.com/stories/2017/mar/05/spokanes-urban-explorers-look-for-the-humanity-in-/)

## Pie chart

We can make interactive pie charts! It's a little clunky, but it works as a good alternative to photos being used as graphics sometimes.

**Requirement(s)**
1. Title (optional)
2. Source (optional)
3. Datasets
	- each data point should end with and underscore followed by incrementing number (example below)
	-  each data point should start with a descriptive name, followed by the number value
4. Currency (optional)
	- If we're displaying currency, add `currency="yes"`  

Example of usage:
- ``[piechart title="Percent of area cities using charts" source="http://www.dandatasourceatalongurl.com" data_1="Spokane,48.6" data_2="Coeur d'Alene,16.4" data_3="Moses Lake,54" data_4="Pullman,32"]``

*The totals can be more than 100, it'll automatically calculate how big of a slice each data point should be*

## Bar chart

Interactive bar charts.

**Requirement(s)**
1. Title (optional)
2. Source (optional)
3. X-axis labels (optional)
4. Y-axis title (optional)
5. Y-axis minimum value
6. Y-axis maximum value
7. Datasets
	- each data point should end with and underscore followed by incrementing number (example below)
	-  each data point should start with a descriptive name, followed by the number value
8. Currency (optional)
	- If we're displaying currency, add `currency="yes"`  

Example of usage:
- ``[barchart title="Number of Charts" source="http://www.spokanecountycharts.org" y_title="Number" y_max=70 y_min=0 x_labels="Jan.,Feb.,March,April,May,June,July" data_1="Spokane,1,1,2,3,5,8,13" data_2="Coeur dAlene,1,2,4,8,16,32,64" data_3="Post Falls,0,2,3,2,5,7,19"]``


## Line chart

Interactive line charts.

**Requirement(s)**
1. Title (optional)
2. Source (optional)
3. X-axis labels (optional)
4. Y-axis title (optional)
5. Y-axis minimum value
6. Y-axis maximum value
7. Datasets
	- each data point should end with and underscore followed by incrementing number (example below)
	-  each data point should start with a descriptive name, followed by the number value
8. Currency (optional)
	- If we're displaying currency, add `currency="yes"`  

Example of usage:
- ``[linechart title="Number of Charts" source="www.spokanechartsource.com" y_title="Number" y_min=0 y_max=20 data_1="Spokane,None,None,2,4,6,8,7,5,9,10,13" x_labels="January,February,March,April,May,June,July,August,September,October,November"]``

## Special section

This will embed a teaser to a special section.

It's useful when we want to link stories together through a special section and tease to each other.

**Requirement(s)**

1. Title
2. Description
3. Teaser photo 

Example of usage, if wishing to tease to two stories:
 - ``[specialsection id=99201]``

## Generic links

This will embed a teaser to a genericlink.

It's similar to the special section teaser.

**Requirement(s)**

1. Headline
2. URL
3. Content
4. Photo in one of the fields (image, external or photo)

Example of usage, if wishing to tease to two stories:
 - ``[genericlink id=99201]``

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NzExMTgxNjBdfQ==
-->