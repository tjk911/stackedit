---


---

<p>Shortcodes are simple ways to get additional interactive elements into our stories.</p>
<p>The benefit of using shortcodes is that our users are empowered to think with interactivity in mind, and it is relatively easy to integrate into the NewsGate-to-Django workflow.</p>
<p>Additionally, incorrect shortcodes do not create template issues, they simply do not appear.</p>
<p><strong>Caveat: Some of these shortcodes have not been tested or used recently, and may require additional tweaks/fixes</strong></p>
<h1 id="available-shortcodes">Available shortcodes</h1>
<p>Most of these shortcodes require some preparation beforehand in order to be used properly in NewsGate.</p>
<ol>
<li>Teasers</li>
<li>Video</li>
<li>Audio</li>
<li>Document</li>
<li>Photo</li>
<li>Photoset</li>
<li>Phototile</li>
<li>360 Photo</li>
<li>Vertical Photo</li>
<li>Longform photo</li>
<li>Then and Now</li>
<li>Mug</li>
<li>Timeline</li>
<li>Embed</li>
<li>Graphic</li>
<li>Graphic set</li>
<li>Pie chart</li>
<li>Bar chart</li>
<li>Line chart</li>
<li>Special sections</li>
<li>Genericlink</li>
</ol>
<h2 id="how-to-use-them-in-newsgate">How to use them in NewsGate</h2>
<p>In the following sections we’ll cover the specific shortcodes and how to use them, but generally speaking for NewsGate use, you will need to write the shortcode, highlight it, and select <code>mm_shortcode</code></p>
<p>For example, if I were embedding a photo in the story, I would do this:<br>
<code>[photo id=4257834]</code>, highlight/select it, and choose <code>mm_shortcode</code>. It should change the color of it to a shaded light blue.</p>
<p>It is possible to just use shortcodes in Django, but it’s not recommended as it will break the connection between NewsGate and Django (or disable easy updates).</p>
<h2 id="teasers">Teasers</h2>
<p>Teasers will embed a small box in the story with a photo, headline and teaser text to a different story.</p>
<p>It’s useful when we’re running related stories, or a series of stories, and we wish to drive attention to additional stories.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Teaser stories must already be in Django with an available Story ID</li>
</ol>
<p>Example of usage, if wishing to tease to two stories:</p>
<ul>
<li><code>[teasers ids=844380,844309]</code></li>
</ul>
<h2 id="video">Video</h2>
<p>Similar to the Youtube shortcode, except this lets us embed any video that is in our Django CMS. This includes externally linked videos such as Vimeo, Youtube or even Facebook.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django video ID</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[video id=3456888]</code></li>
</ul>
<h2 id="audio">Audio</h2>
<p>Much like the Video shortcode, except this is for us to embed audio files that are in our Django CMS.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django audio ID</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[audio id=2363]</code></li>
</ul>
<h2 id="document">Document</h2>
<p>This lets us embed documents in our Django CMS.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django document ID</li>
<li>Document requires a description</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[document id=10126]</code></li>
</ul>
<h2 id="photo">Photo</h2>
<p>When you want to embed a single photo in a story.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django photo ID</li>
<li>Photo requires a caption</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[photo id=471520]</code></li>
</ul>
<h2 id="photoset">Photoset</h2>
<p>Photoset, aka galleries, can be embedded in a story when we have multiple galleries running.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django photoset ID</li>
<li>Gallery requires title/headline</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[photoset id=6816]</code></li>
</ul>
<h2 id="phototile">Phototile</h2>
<p>You can create a phototile made of three horizontal photos. The first item will be large, with the following two other smaller.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django photo IDs</li>
<li>Photos require captions</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[phototile ids=123,456,789]</code></li>
<li><a href="http://www.spokesman.com/stories/2017/sep/03/wet-spring-and-summers-heat-deliver-mixed-wheat-ha/">http://www.spokesman.com/stories/2017/sep/03/wet-spring-and-summers-heat-deliver-mixed-wheat-ha/</a></li>
</ul>
<h2 id="then-and-nowbefore-and-after">Then and Now/Before and After</h2>
<p>This lets you create a then-and-now slider with two photos.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django photo ID for the “before” and “after” photo</li>
<li>Photos should have captions</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[thennow before=479478 after=482687]</code></li>
</ul>
<h2 id="mugs">Mugs</h2>
<p>This embeds a mug shot.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django photo ID</li>
<li>Float direction (left or right)</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[mug id=481936 float=right]</code></li>
</ul>
<h2 id="vertical-photo">Vertical photo</h2>
<p>This embeds a vertical photo.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django photo ID</li>
<li>Photo caption</li>
<li>Float direction (left or right)</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[vertical_photo id=481935 float=right]</code></li>
</ul>
<h2 id="longform-photo">Longform photo</h2>
<p>This embeds a photo with additional styling. It enlarges the photo across the entire screen width.</p>
<p><strong>DO NOT</strong> use on normal stories, use this only with longform stories.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Django photo ID</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[longform_photo id=475912]</code></li>
<li><a href="http://www.spokesman.com/stories/2018/jul/28/amazon-brings-its-order-fulfillment-machine-spokan/">Amazon brings its order fulfillment machine to Spokane</a></li>
</ul>
<h2 id="timelines">Timelines</h2>
<p>This embeds a timeline into the story</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Timeline ID</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[timeline id=33]</code></li>
<li><a href="http://www.spokesman.com/stories/2017/aug/20/25-years-after-ruby-ridge-our-divisions-have-grown/">25 years after Ruby Ridge, our divisions have grown</a></li>
</ul>
<h2 id="embeds">Embeds</h2>
<p>This embeds an embed. Embeds are typically used for iframes, but do be careful - you can put <strong>anything</strong> in these. This means you could break the story page if you’re not careful.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Embed ID</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[embed id=33]</code></li>
<li><a href="http://www.spokesman.com/stories/2018/sep/10/trump-promises-a-real-book-on-his-white-house/">Trump promises a ‘real book’ on his White House</a></li>
</ul>
<h2 id="graphics">Graphics</h2>
<p>This embeds a graphic item. If they’re <strong>not</strong> in svg format, they will slide into the page with animation. The “swoosh” effect as Megan Rowe calls it.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Graphic ID</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[graphic id=33]</code></li>
<li><a href="http://www.spokesman.com/stories/2018/sep/02/with-an-eye-to-its-bottom-line-wsu-turns-to-privat/">WSU anticipates revenue boost from partnership with international student recruiter</a></li>
</ul>
<h2 id="photos">360 photos</h2>
<p>This embeds a teaser to a 360 photo.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>360 Photo ID</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[photo360 id=17]</code></li>
<li><a href="http://www.spokesman.com/stories/2017/mar/05/spokanes-urban-explorers-look-for-the-humanity-in-/">Spokane’s urban explorers look for the humanity in abandoned places, but there are risks</a></li>
</ul>
<h2 id="pie-chart">Pie chart</h2>
<p>We can make interactive pie charts! It’s a little clunky, but it works as a good alternative to photos being used as graphics sometimes.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Title (optional)</li>
<li>Source (optional)</li>
<li>Datasets
<ul>
<li>each data point should end with and underscore followed by incrementing number (example below)</li>
<li>each data point should start with a descriptive name, followed by the number value</li>
</ul>
</li>
<li>Currency (optional)
<ul>
<li>If we’re displaying currency, add <code>currency="yes"</code></li>
</ul>
</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[piechart title="Percent of area cities using charts" source="http://www.dandatasourceatalongurl.com" data_1="Spokane,48.6" data_2="Coeur d'Alene,16.4" data_3="Moses Lake,54" data_4="Pullman,32"]</code></li>
</ul>
<p><em>The totals can be more than 100, it’ll automatically calculate how big of a slice each data point should be</em></p>
<h2 id="bar-chart">Bar chart</h2>
<p>Interactive bar charts.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Title (optional)</li>
<li>Source (optional)</li>
<li>X-axis labels (optional)</li>
<li>Y-axis title (optional)</li>
<li>Y-axis minimum value</li>
<li>Y-axis maximum value</li>
<li>Datasets
<ul>
<li>each data point should end with and underscore followed by incrementing number (example below)</li>
<li>each data point should start with a descriptive name, followed by the number value</li>
</ul>
</li>
<li>Currency (optional)
<ul>
<li>If we’re displaying currency, add <code>currency="yes"</code></li>
</ul>
</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[barchart title="Number of Charts" source="http://www.spokanecountycharts.org" y_title="Number" y_max=70 y_min=0 x_labels="Jan.,Feb.,March,April,May,June,July" data_1="Spokane,1,1,2,3,5,8,13" data_2="Coeur dAlene,1,2,4,8,16,32,64" data_3="Post Falls,0,2,3,2,5,7,19"]</code></li>
</ul>
<h2 id="line-chart">Line chart</h2>
<p>Interactive line charts.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Title (optional)</li>
<li>Source (optional)</li>
<li>X-axis labels (optional)</li>
<li>Y-axis title (optional)</li>
<li>Y-axis minimum value</li>
<li>Y-axis maximum value</li>
<li>Datasets
<ul>
<li>each data point should end with and underscore followed by incrementing number (example below)</li>
<li>each data point should start with a descriptive name, followed by the number value</li>
</ul>
</li>
<li>Currency (optional)
<ul>
<li>If we’re displaying currency, add <code>currency="yes"</code></li>
</ul>
</li>
</ol>
<p>Example of usage:</p>
<ul>
<li><code>[linechart title="Number of Charts" source="www.spokanechartsource.com" y_title="Number" y_min=0 y_max=20 data_1="Spokane,None,None,2,4,6,8,7,5,9,10,13" x_labels="January,February,March,April,May,June,July,August,September,October,November"]</code></li>
</ul>
<h2 id="special-section">Special section</h2>
<p>This will embed a teaser to a special section.</p>
<p>It’s useful when we want to link stories together through a special section and tease to each other.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Title</li>
<li>Description</li>
<li>Teaser photo</li>
</ol>
<p>Example of usage, if wishing to tease to two stories:</p>
<ul>
<li><code>[specialsection id=99201]</code></li>
</ul>
<h2 id="generic-links">Generic links</h2>
<p>This will embed a teaser to a genericlink.</p>
<p>It’s similar to the special section teaser.</p>
<p><strong>Requirement(s)</strong></p>
<ol>
<li>Headline</li>
<li>URL</li>
<li>Content</li>
<li>Photo in one of the fields (image, external or photo)</li>
</ol>
<p>Example of usage, if wishing to tease to two stories:</p>
<ul>
<li><code>[genericlink id=99201]</code></li>
</ul>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

