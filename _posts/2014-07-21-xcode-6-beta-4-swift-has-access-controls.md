---
id: 55
title: 'Xcode 6 Beta 4: Swift has access controls'
date: 2014-07-21T21:39:03+00:00
author: tfranklin
layout: post
guid: http://cleancrispcode.wordpress.com/?p=55
permalink: /2014/07/21/xcode-6-beta-4-swift-has-access-controls/
geo_public:
  - 0
muut_post_domain:
  - taylorfranklin.me
muut_comments_count:
  - 0
categories:
  - iOS
tags:
  - .by()
  - //fixme
  - //mark
  - //todo
  - ios8
  - ios8 beta
  - objective-c swift
  - private
  - public
  - stride()
  - swift access controls
  - xcode 6
  - xcode 6 beta 4
---
#### Only **2 weeks** after the previous beta release, we get the next iteration of Xcode and iOS. Here are some key features:

  1. ACCESS CONTROLS! I believe developers would have been outraged if Swift did not include this soon. While still in Beta, Swift does implement the important programming paradigm of access controls although it is done in a slightly different way, as to be expected. The basic description from Apples release notes is as follows: 
      1. • `private` entities can only be accessed from within the source file where they are defined.
  
        • `internal` entities can be accessed anywhere within the target where they are defined.
  
        • `public` entities can be accessed from anywhere within the target and from any other context that imports the current target’s module.

  2. Another nice one is the keywords `@final`, `@lazy`, `@optional`, and `@required` are drifting away from any Objective-C roots they had by making the @ sign not required.

  3. Another nice, almost superficial improvement is Xcode now recognizes comment annotations for the following: `//MARK:`, `//TODO:`, and `//FIXME:`. It will also include them in the jump bar so you can &#8220;jump&#8221; right to that point in code. This is nice to have since `#pragma marks` seem to have disappeared in Swift. Some at Apple believe using extensions would make more sense rather than throwing pragma marks everywhere, but I guess that is up to you <img src="http://taylorfranklin.me/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />
  4. From what I can tell, the left pane in Xcode has been improved, there is not overlapping icons, which is great. Also, Xcode projects seems to have gotten a more Yosemite UI update. A+ for small UI changes.
  5. Lastly, I never used `.by()` functions, but their replacement of `stride()` functions looks straightforward and readable, kind of like those verbose Objective-C method signatures. Take a look at the examples in the Apple Release notes:

<p style="padding-left: 60px;">
  stride(from: x, to: y, by: z)      // was: (x..<y).by(z)
</p>

<p style="padding-left: 60px;">
  stride(from: x, through: y, by: z) // was: (x&#8230;y).by(z)
</p>

&nbsp;

### What I want to see

  * An improved debugger console, most of the time I cannot see the values of elements where I have set a breakpoint. I then revert back to beginner programming days of putting print statements everywhere&#8230; I am going to have to play with Beta 4 a little more to see if there are any improvements on this.

It is so cool to be developing in a new programming language as it is being created! All the big and important programming languages we know about have been out of Beta forever, but Swift is just getting started.

<!-- AdSense Now! Lite: PreFiltered - NoAds [ WP is not in the loop. ] -->