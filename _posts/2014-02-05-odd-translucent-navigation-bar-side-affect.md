---
id: 7
title: Odd Translucent Navigation Bar Side Affect
date: 2014-02-05T23:59:31+00:00
author: tfranklin
layout: post
permalink: /2014/02/05/odd-translucent-navigation-bar-side-affect/
muut_post_domain:
  - taylorfranklin.me
muut_comments_count:
  - 0
categories:
  - iOS
tags:
  - coregraphics
  - drawing
  - ios7
  - navigationbar
  - titleview
  - translucent
---
Yesterday I was working on my Objective-C iOS app that has a `navigationBar` with `leftBarButton` and `rightBarButton` as well as a custom `TitleView`. I noticed a weird side affect when setting the translucent property on the `navigationBar` like so:
  
You see, the rest of my view is a drawing context made with the CoreGraphics framework. When the translucent property is set to YES, everything works fine, but when it is set to NO, the drawing board goes crazy as you can see in the the picture on the left when it should be like the picture on the right which has the translucent property set to YES.

<img alt="Odd Drawing Effects" style="border: #000000 1px solid;" src="{{ site.url }}/images/2014/02/ios-simulator-screen-shot-feb-5-2014-12-09-21-am.png" width="49%" />
<img alt="Normal Drawing" style="border: #000000 1px solid;" src="{{ site.url }}/images/2014/02/ios-simulator-screen-shot-feb-5-2014-11-47-22-pm.png" width="49%" />

<p style="text-align:left;">
  It appears that the brush strokes are falling off the view and not being drawn continuously. I didn&#8217;t think I was doing anything out of the ordinary with my drawing board, but there seems to be some issues in iOS 7 with translucent property affecting other parts of the view. It is possible something else in my app is interfering, but regardless, this is odd behavior to happen just by changing a boolean value. Comment if you have an idea of why, otherwise, I hope you enjoyed this little adventure.
</p>