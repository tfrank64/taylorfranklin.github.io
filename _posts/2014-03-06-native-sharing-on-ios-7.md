---
id: 21
title: Native Sharing on iOS 7
date: 2014-03-06T19:01:57+00:00
author: tfranklin
layout: post
permalink: /2014/03/06/native-sharing-on-ios-7/
muut_post_domain:
  - taylorfranklin.me
muut_comments_count:
  - 0
categories:
  - iOS
tags:
  - dialog
  - facebook
  - facebook sdk
  - fbdialogs
  - ios
  - ios7
  - native
  - nativly
  - share
  - slcomposeviewcontroller
  - slservicetypefacebook
  - twitter
  - uiactionsheet
---
In researching the topic of using the native sharing dialogs in iOS 7, I found it surprisingly difficult. I got tons of information on the Facebook and Twitter development sites, but it was overkill for my needs. I realized that after adding the Facebook SDK to my iOS project&#8230; I also got info from a user perspective on the feature itself and lastly I read Stackoverflow answers on kinda doing it with `FBDialogs` in the Facebook SDK. Anyway, here is a little code snippet of how you can use the native sharing dialogs for Facebook, Twitter, LinkedIn (OS X only), and even Weibo.

First I will show you what you can do if presenting sharing options in a `UIActionSheet` such as what I did in my app so people could share my app. The next thing here is using the `SLComposeViewController`. For some reason it took me awhile to come across it, but it is the key to making the share dialogs happen. Therefore, make sure the Social framework is added to your project and then `#import <Social/Social.h>` into the relevant files so that you use social features such as `SLServiceTypeFacebook`. For reference, here is all the relevant code hosted in a <a href="https://gist.github.com/tfrank64/9403006" target="_blank">Github gist</a>.

The code snippet in that gist, shows the way I chose to implement the `SLComposeViewContrller`. Of course, you still need to create a `UIActionSheet` and declare it&#8217;s delegate, but this is most of what you need and it is fairly simple.

So that is about it, I hope you enjoyed the simplicity of this rather than including some external framework.
