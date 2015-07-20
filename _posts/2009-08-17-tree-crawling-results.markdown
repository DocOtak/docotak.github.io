---
layout: post
status: publish
published: true
title: Tree Crawling Results
author:
  display_name: abarna
  login: admin
  email: abarna@gmail.com
  url: http://
author_login: admin
author_email: abarna@gmail.com
author_url: http://
wordpress_id: 252
wordpress_url: http://www.andrewbarna.org/blog/?p=252
date: '2009-08-17 00:21:43 -0700'
date_gmt: '2009-08-17 08:21:43 -0700'
categories:
- HPU Blog Mirror
tags: []
comments: []
---
<p>Last weeks post might have been a bit puzzling to most people so I figured I could show what it actually does. Just the end product (in its current state). When that code is <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Interpreted_language">interpreted<&#47;a> (ruby is not a compiled language), it outputs HTML stable for display in any (modern) web browser. The particular bit of code, produces a navigation menu to make finding the videos easy. I can't link to the live page yet as it is not complete, but I can show a screen shot of what it looks like.<br &#47;><a href="http:&#47;&#47;andrewbarna.org&#47;photos&#47;gallery3&#47;var&#47;albums&#47;dailyphoto&#47;ghdc_sci_at_sea.png"><img src="http:&#47;&#47;andrewbarna.org&#47;photos&#47;gallery3&#47;var&#47;albums&#47;dailyphoto&#47;ghdc_sci_at_sea.jpg"&#47;><&#47;a><br &#47;><br &#47;>The to make the embedding of the video itself convenient I wrote a custom tag class that is then interpreted to make an embedded video. All I need to put in the page file is the following line: <code>{video: "Rosette&#47;Rosette_Recovery_Day_Rough.m4v"}<&#47;code> where the "Rosette&#47;Rosette_Recovery_Day_Rough.m4v" is simply the path to the desired video inside the video folder. The custom video tag class then figures out how deep the resulting page is in the tree and constructs the video embed path accordingly so it always is the correct path. So far everyone (especially myself) is happy with the results. The graphic designer is currently working on what we are calling an "exploding ship," if you is familiar with the book series <a href="http:&#47;&#47;www.subsim.com&#47;books&#47;cross_sections.htm">Incredible Cross-Sections<&#47;a> it will be something like that. So the exploding ship will be included to give a location of where the video was shot on the ship.<br &#47;><br &#47;>Finished product due in 2 weeks...<br &#47;>-Andrew<br &#47;><b>Due to a disaster, the screenshot will probably be lost forever<&#47;b></p>
