---
layout: post
status: publish
published: true
title: Tree Crawling Problem
author:
  display_name: abarna
  login: admin
  email: abarna@gmail.com
  url: http://
author_login: admin
author_email: abarna@gmail.com
author_url: http://
wordpress_id: 207
wordpress_url: http://www.andrewbarna.org/blog/?p=207
date: '2009-08-07 21:08:18 -0700'
date_gmt: '2009-08-08 05:08:18 -0700'
categories:
- HPU Blog Mirror
tags: []
comments: []
---
<p>My opportunities to work on coding problems occur rarely in the office I work in. So when I was asked to figure out a menu generation problem, I was more than happy to accept. All of the content I'm working on will eventually be included on the DVD which will come included as supplemental material for a new edition of an oceanographic textbook titled Descriptive Physical Oceanography. What this means is all files included will be unchanging, static, little to no dynamic content. It is also desirable to have any materials included with the book be as self contained as possible due to the seafaring nature of oceanographic work, internet at sea may be unavailable or, when available, very expensive and slow.<br &#47;><br &#47;>To allow the easy construction of static, self contained websites while utilizing templates and generators that use the state of the dynamic content at the time of "compile", we use a <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;RubyGems">ruby gem<&#47;a> called <a href="http:&#47;&#47;webgen.rubyforge.org&#47;">webgen<&#47;a>. This gem allows easy creation of static websites using templates, markup languages, and a rather nifty programing language called <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Ruby_programming_language">ruby<&#47;a>.<br &#47;><br &#47;>Webgen has a rather nice menu generation method which crawls a tree generated from the files and directories in a special folder of the webgen project. When the webgen command is run in the project directory, it crawls this folder looking for changes and updates the tree accordingly. As convenient as this was, it did not function in a way that would suit our needs based on what the very talented graphic designer had produced. The built in behavior was to create a nested <a href="http:&#47;&#47;www.w3schools.com&#47;tags&#47;tag_ul.asp">unordered list<&#47;a>. What we needed it to do was only use the unordered list tag for the first level of the tree. Subsequent branches, if any, needed to be in the html <a href="http:&#47;&#47;www.w3schools.com&#47;tags&#47;tag_div.asp">div tag<&#47;a> and not be nested within the unordered list, as this both makes applying styling difficult, but also appears to be unsupported by the spec. To accomplish these changes, I needed to extend the functionality of webgen. Luckily, there was a framework in place to allow this and, thanks to the object oriented nature of ruby, I could easily inherent the functionally of built in menu generation class and simply override the methods I needed to. Just my luck, only one method need to be overridden. Bellow is the almost finished product.<br &#47;><br />
Code:<br &#47;></p>
<pre style="background-color:#f1f1f1;height:500px;width:500px;overflow:auto;">
<code><br />
module Webgen<br />
  module Tag<br />
    include Webgen::Tag::Base<br />
    class CustomMenu < Webgen::Tag::Menu<br />
      def create_output_nested(context, tree, level = 1)<br />
          ### output variable initialization ###<br />
          out = ""<br />
          out_div = ""<br />
          out = "
<ul>" if level == 1<br />
          out_div = "
<div class='sub_nav#{level}'>" if level > 1</p>
<p>         ### Loop through the tree and all the children to generate the menu ###<br />
          tree.children.each do |child|<br />
            menu = child.children.length > 0 ? create_output_nested(context, child, level + 1) : ''<br />
            style, link = menu_item_details(context.dest_node, child.node, context.content_node.lang, level)<br />
            out << "
<li #{style}>#{link}" if level == 1</p>
<p>            ### Only the first level should be encapsulated in a
<ul> tag ###<br />
            if level > 1 then<br />
              out_div << "
<div class='directory'>" if child.node.is_directory?<br />
              out_div << "
<div class='item#{" current node" if context.node == child.node}'>" if !child.node.is_directory? </p>
<p>              ### Getting the Image path, this should act the same as the relocatable: tag ###<br />
                image_path = ""<br />
                depth = context.node.level - 1<br />
                depth.times do<br />
                  image_path << "..&#47;"<br />
                end<br />
                image_path << "images&#47;"<br />
                image_path << child.node['thumb'] if child.node['thumb']<br />
              ### Done ###</p>
<p>              out_div << "<img src=#{image_path}>" if child.node['thumb']<br />
              out_div <<  link</p>
<p>              out_div << "<br &#47;>#{child.node['blerb']}" if child.node['blerb']<br />
              out_div << "<&#47;div>"<br />
            end</p>
<p>            out_div << menu<br />
            out << "<&#47;li>" if level == 1<br />
          end</p>
<p>          ### Closing the approprate tags to keep things tidy ###<br />
          out_div << "<&#47;div>" if level > 1<br />
          out << "<&#47;ul>"</p>
<p>          ### Add the output of the div enclosed items to the *END* of the output containing the ul ###<br />
          out << out_div<br />
          out<br />
      end<br />
    end<br />
  end<br />
end</p>
<p>Webgen::WebsiteAccess.website.config['contentprocessor.tags.map']['custommenu'] = 'Webgen::Tag::CustomMenu'<br />
<&#47;code><br />
<&#47;pre><br &#47;>You may be noticing that it uses a lot of if statements to check what level of the tree the loop is on. Granted this may not be the best practice and would probably have been better to separate all the level one stuff from the greater than level one stuff by putting them in separate methods. However, if you were able to spot it, you may have noticed that there is <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Recursion_(computer_science)">recursion<&#47;a> occurring in the method. Since it can be tricky to visualize the result of using recursive methods, I opted to just check to see what level of the tree the loop was on, and the construct the appropriate output accordingly. I even managed to throw in a connivence method by resolving the depth of the page in the website, and constructing an appropriate link to the images on the page. Bottom line, all the images work.<br &#47;><br &#47;>In all this took about two days to sort out. Most of the first one spent learning the ins and outs of the <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Application_programming_interface">API<&#47;a> and most of the second day moulding the output to what I wanted.<br &#47;><br &#47;>Finished product due in 3 weeks.<br &#47;>-Andrew</p>
