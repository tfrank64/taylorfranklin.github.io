---
id: 97
title: 'Open Source Fusion: CRPixellatedView &#038; MGSpotyViewController'
date: 2014-10-11T10:19:20+00:00
author: tfranklin
layout: post
guid: http://cleancrispcode.wordpress.com/?p=97
permalink: /2014/10/11/open-source-fusion-crpixellatedview-mgspotyviewcontroller/
geo_public:
  - 0
mashsb_shares:
  - 100,170,276,329,486,583,635,736,875,0,0
mashsb_timestamp:
  - 1413147640
muut_post_domain:
  - taylorfranklin.me
muut_comments_count:
  - 0
categories:
  - iOS
  - Open Source
tags:
  - CRPixellatedView
  - gist
  - github
  - github fusions
  - ios
  - ios8
  - MGSpotyViewController
  - open source fusion
  - open source project
---
Sometimes I like to experiment with ideas I have, but these ideas are not quite big enough for an open source project, much less a full app. Therefore, I hope to have a series of posts called, **Open Source Fusion**, where I combine at least 2 open source projects to create something cool, interesting, or weird.

For this Open Source Fusion, I choose to substitute the blurring in <a href="https://github.com/matteogobbi/MGSpotyViewController" target="_blank">MGSpotyViewController</a> with a more pixelated approach, using <a href="https://github.com/chroman/CRPixellatedView" target="_blank">CRPixellatedView</a>. I will explain more of how I did this, but without further adieu, here is what I made:

<img src="{{ site.url }}/images/2014/10/pixelpull.gif" alt="cat gif">

### How It Came About

I enjoy discovering new and trending repositories on Github. So when I come across some repos I like, I star them so that I might use them in my own creations someday. For this, I liked what these two repos did separately, but I thought they might be even better together, like the classic example of peanut butter and chocolate or better yet, bacon and everything else. Regardless, I came across MGSpotyViewController and I liked the effect of the image expanding as the tableview was scrolled down, in addition the blurring effect fading in and out.

<img class="aligncenter" src="https://camo.githubusercontent.com/20ccae14b0cfbee5bcd3867df4e2c5c51909d989/687474703a2f2f7777772e6d617474656f676f6262692e69742f66696c65732d686f7374696e672f4d4753706f747956696577566964656f2d736d616c6c65722e676966" alt="MGSpotyViewController" width="300" height="535" />

There is similar story for how I came across CRPixellatedView and I just loved the effect.

<img class="aligncenter" src="https://camo.githubusercontent.com/fa00bd7b49d4b0fc0d5b2ff6cdbdb2a293521221/687474703a2f2f6368726f6d616e2e6d652f77702d636f6e74656e742f75706c6f6164732f323031342f30362f4352506978656c6c61746564566965772e676966" alt="CRPixellatedView" width="318" height="318" />

I had noticed a lot of iOS apps were doing the expanding image with their table view headers and I wondered how I could take it one step further. Therefore, I made my own little project and began fusing these two amazing projects.

### The Details

In my implementation, I used the same design pattern as MGSpotyViewController, using a transparent header over a `UIImageView` that is actually on `self.view`. It is important for the image to be on self.view because if it was on the tableview header it would get scrolled down somewhat, but we want the y value to stay in place. I then modify the frame in a `scrollViewDidScroll` delegate method to increase and decrease the size of the image depending on how the tableview is scrolled.

Adding CRPixellatedView was actually pretty simple, I just dropped in the .h and .m into my project and started using them. I made the previously mentioned `UIImageView` a CRPixellatedView which is a subclass of `UIImageView`, so it worked great. I then set the animationDuration and pixelScale for when I pixelate the view later.

**Roadblock**: unfortunately, I do not think there is a way to instantly pixelate a view with the API for CRPixellatedView. Therefore, when scrolling, you will notice the image only pixelates one time whenever you scroll down past a certain point and not in many small increments. The animation starts to get buggy and laggy when you set the `animationDuration` too small (e.g. 0.1) or try to animate the view too often. It would be nice if the update was instant and I did not have to set an `animationDuration`, but I worked within these constraints.

In the `scrollViewDidScroll` method, I kept a boolean value, `pulled`, so that once I pixelated the view, I would not reverse that pixelation until the tableview was greater than or equal to the starting offset. Once that was implemented, everything started working pretty smoothly.

### The Code

I didn&#8217;t insert any code snippets because I felt it made the most sense to see my PixelViewController in it&#8217;s entirety.

So check my Github gist here: <a href="https://gist.github.com/tfrank64/e0d78df2c85268e1da85" target="_blank"><img class="alignnone" src="https://assets-cdn.github.com/images/modules/open_graph/github-mark.png" alt="" width="118" height="62" /></a>

Thanks for reading, I look forward to more of these Open Source Fusions!
