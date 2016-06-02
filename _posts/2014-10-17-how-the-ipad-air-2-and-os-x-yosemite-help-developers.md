---
id: 131
title: How the iPad Air 2 and OS X Yosemite Help Developers
date: 2014-10-17T09:06:02+00:00
author: tfranklin
layout: post
permalink: /2014/10/17/how-the-ipad-air-2-and-os-x-yosemite-help-developers/
muut_post_domain:
  - taylorfranklin.me
muut_comments_count:
  - 0
categories:
  - iOS
tags:
  - Apple event
  - iPad air 2
  - its road trip
  - October 16th
  - webGL safari
  - yosemite
---
When watching Apple&#8217;s October 16th live stream today, the biggest thing I noticed was that their live stream was actually working pretty well!

<img src="{{ site.url }}/images/2014/10/app.png" alt="too long">

On a more serious note, there are many things I did like about Apple&#8217;s latest announcement. Some of which included the stunning 5K iMac retina screen, the iPad Air 2, and OS X Yosemite. As an iOS developer, I must ask what does all this mean for developers? Has anything changed, or did Apple just reveal some shiny new toys?

### iPad Air 2

Looking at the technical specifications for the iPad Air 2, we see the screen resolution is _2048 x 1536 on a retina display_. This converts nicely to the 1024 x 768, developers are already familiar with. I think the lack of screen size change comes as a relief to developers after all the changes in screen size over the past couple months.

Now that Metal is out with iOS 8, the best thing that can complement it, is a high performance device. So far, this seems to be the most powerful mobile device Apple has released to date. The iPad Air 2 features the A8X chip, 64-bit architecture, and 3 billion transistors. It&#8217;s crazy to see how consistently the iPad has improved over the years:

<a href="http://www.apple.com/ipad-air-2/performance/" target="_blank">
<img src="{{ site.url }}/images/2014/10/Screen-Shot-2014-10-16-at-8.08.12-PM.png" alt="performance">
</a>

The graphics performance has seemingly grown exponentially, with a nice gap between the latest iPad Air and A7 chip. This is the kind of improvement companies strive for and Apple is doing a pretty good job at it.

Lastly, the the LCD layer being closer to your fingerprints is an amazing addition to this product. The Air 2 has a _fully laminated display_, which may not sound like much, but this will allow the separation between your finger and the screen content to be so small. I&#8217;m not sure what the implications are for design and development, but this is a neat feature that should only enhance existing iPad apps.

Other relevant features:

  * Touch ID
  * Barometer
  * Apple Pay Support

### OS X Yosemite

We have already known about Yosemite for months now, but since it is now here, what do developers need to know?

_Extensions are not just for iOS_. Just like you can find them in iOS 8, developers can include them in OS X Yosemite. According to <a href="https://www.apple.com/osx/developer/" target="_blank">Apple</a>, the supported extensions are for Notification Center, Sharing, and Custom Actions. These three categories cover a lot of ground when you realize a custom action could be anything from photo editing to some sort of word processing.

With Yosemite&#8217;s release, the potential of <a href="https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/Handoff/HandoffFundamentals/HandoffFundamentals.html" target="_blank">Handoff</a> can be fully realized. I really like that Apple opened this up to developers because many times in the past, Apple will wait until the next OS to release an open API for it&#8217;s feature such as UIBlurEffect, touch ID, or App Extensions. We know the obvious use for Handoff being the continuity of tasks between devices, but I cannot wait to see this feature to be used in an even more creative way by developers.

A less exciting yet nice features is that Apple claims _Safari now supports WebGL_ which will allow Safari to natively render 3D scenes. This would be great except Google Chrome has been supporting it for a <a href="http://caniuse.com/#feat=webgl" target="_blank">long time</a>.

<img src="{{ site.url }}/images/2014/10/Screen-Shot-2014-10-16-at-8.43.53-PM.png" alt="metrics">


The green being full support and the yellow meaning partial support. Nevertheless, Safari is and has been a pretty solid browser otherwise.

**What&#8217;s Next?**

Honestly, I think now would be a great time for Apple to slow down with new products and features (as exciting as they are) and focus on stable software. Xcode is pretty buggy, iOS 8 has already had it&#8217;s fair share of issues, and who knows how well Yosemite and Apple Pay will work over the next few weeks. As a developer, I am excited, so much so, I might dabble into OS X development. The iPad Air 2 is not extremely innovative on the surface, but it is definitely a step forward for Apple. If there is one thing you should take away from Apple&#8217;s live stream today, it&#8217;s that autocorrect is not always your friend as we saw with <a href="http://i.imgur.com/impPM42.png" target="_blank">&#8220;it&#8217;s road trip&#8221;</a>
