---
layout: post
status: publish
published: true
title: The Horizon and the Honolulu Zoo
author:
  display_name: abarna
  login: admin
  email: abarna@gmail.com
  url: http://
author_login: admin
author_email: abarna@gmail.com
author_url: http://
wordpress_id: 657
wordpress_url: http://www.andrewbarna.org/?p=657
date: '2011-04-26 21:25:45 -0700'
date_gmt: '2011-04-27 07:25:45 -0700'
categories:
- HPU Blog Mirror
tags: []
comments: []
---
<p>About a week ago I had stayed up way to late to work on a project that has been on simmer for quite a while now. Basically, I am trying to adjust known sunrise and set equations (and results) to account for the local topography. Where I live in Hawaii is next to the mountains, as such, the sun "sets" bellow the mountains a full hour before it sets over the ocean. To accomplish this, I was going to need to figure out where the earth-sky interface is using whatever GIS data I could get my hands on. I was up till 0300 yet no success. The dataset that I was using was large, consisting of a 1 by 1 degree portion of earth at 1 arc-second resolution. This means that there are approximately 3000 points in each direction (x,y). This means I would need to process about 9 million points. The difficulty arose when trying to find individual points to test. How would I get the correct elevation data? At first I tired putting the data into a kdtree and then performing a nearest neighbor search on it. While this was successful, it was prohibitively slow, taking about 15 seconds to find the closest point in the data to any arbitrary coordinates searched for. Since I test about 800,000 points it would have taken over 100 days to finish. I realized the next morning that I knew what the shape of the data was and that I should be able to quickly calculate where in the array the desired point should be. This method was very successful and the run time for the entire earth-sky interface program was reduced to 15(ish) seconds. The figure below is the results for a point between the residence halls and the academic center.<br &#47;><img src="http:&#47;&#47;www.andrewbarna.org&#47;photos&#47;gallery3&#47;var&#47;resizes&#47;Random%20Stuff&#47;hlc_label.png"><br &#47;><br &#47;><br &#47;>This past friday (Good Friday). I went to the Honolulu Zoo in Waikiki (I think). This was the first time going to the Honolulu zoo and I was eager to see how it compared to the San Diego Zoo. A good time was had and lots of animals were seen (they even have a snake!) While I felt that the elephant enclosure was too small, a new much larger elephant area is being constructed, I hope they finish soon. Like many places in Hawaii, there were peacocks running wild around the place.<br &#47;><img src="http:&#47;&#47;www.andrewbarna.org&#47;photos&#47;gallery3&#47;var&#47;resizes&#47;Random%20Stuff&#47;IMG_0255.JPG"><br &#47;>As for how it compares to the San Diego Zoo (my home town zoo), the Honolulu Zoo was much smaller. I have spent entire days at the San Diego Zoo and I'm pretty sure that I have never managed to see everything there. The Honolulu Zoo in comparison was small enough that the complete circuit around took maybe a little more than 2 hours.<br &#47;><img src="http:&#47;&#47;www.andrewbarna.org&#47;photos&#47;gallery3&#47;var&#47;resizes&#47;Random%20Stuff&#47;IMG_0253.JPG"><br &#47;>The smallness doesn't affect the good time that was had though. Besides, they had a cute fox!<br &#47;><img src="http:&#47;&#47;www.andrewbarna.org&#47;photos&#47;gallery3&#47;var&#47;resizes&#47;Random%20Stuff&#47;IMG_0256.JPG"><br &#47;>Finals are in... two weeks!<br &#47;><br &#47;>-Barna</p>
