---
id: 82
title: Anyone can open source software
date: 2014-09-27T11:02:29+00:00
author: tfranklin
layout: post
permalink: /2014/09/27/anyone-can-open-source-software/
comments: true
geo_public:
  - 0
categories:
  - iOS
  - Open Source
tags:
  - afnetworking
  - cocoapods
  - github
  - ios
  - open source community
  - open source project
  - package manager
  - readme
  - tiltingloader
  - UzysAnimateGifPullToRefresh
---
Even I can open source software, as my title suggests. I recently open sourced a reusable iOS loading view in Swift, called <a href="https://github.com/tfrank64/TiltingLoader" target="_blank">TiltingLoader</a>.

<p style="text-align:center;">
<img src="https://raw.githubusercontent.com/tfrank64/TiltingLoader/master/TiltingLoader/Images.xcassets/tiltingLogo.imageset/tiltingLogo.png" alt="" width="60%" />
</p>

It's nothing crazy, but it works pretty well, looks neat, and it was fun to make. I have it open sourced on <a href="https://github.com/tfrank64" target="_blank">Github</a>, where I keep most of my development projects.

### What every open source project should I have:

  * **A working tool or component**. This one is kind of obvious, but your project can be really simple, assuming you intend to grow it over time or accept contributions from others. You should ask yourself, is this idea novel and/or useful. I think the point is once you have a minimal version of what you actually want, open source your project and let the world help you make it awesome.
  * **Quick and easy way for others to use**. Part of this is how easy it is to download and integrate into your own project. The other part is the actual usage in code, do the method calls make sense (a clean API), is there a general use case or is it very specific, and lastly, is it easier than someone making their own version of what you made. 
    
      * Ideally, using a package manager like <a href="http://cocoapods.org/" target="_blank">CocoaPods</a> for iOS works well and is a fast way to install new components. I didn&#8217;t start TiltingLoader with CocoaPods, but there was always plans to.
      * There are equivalents for other types of projects such as <a href="https://www.npmjs.org/" target="_blank">npm</a> for Node.js projects.
      * Or <a href="https://rubygems.org/" target="_blank">RubyGems</a> for ruby projects.
  * **Create a release on Github or other open source app**. This is useful so there is a clear record of each stable build of your project so if someone needed an older version, they could easily access it. It is also nice to see how far you have come over time like this example from <a href="https://github.com/AFNetworking/AFNetworking/releases" target="_blank">AFNetworking</a>:

  [![afnetworking image]({{ site.url }}/images/2014/09/screen-shot-2014-09-27-at-11-31-35-am.png)]({{ site.url }}/images/2014/09/screen-shot-2014-09-27-at-11-31-35-am.png){:target="_blank"}

  * **Create issues for what is broken as well as what you plan to add**. This is really useful for anyone who forks your project to already know what they can work on to make it better. It shows your project is not perfect, but it has practical steps to improve it, making it very easy for the open source community to grab on to.
  * **Create and awesome and informative README.md**. Creating a good README can make a huge difference on whether someone sticks around to see if what you made is worth learning more about. For functional projects, have lots of clean code samples as well documentation (which can also be in a separate wiki). For more UI focused projects, have a good number of images, adding a GIF or video makes it even better. It was necessary for TiltingLoader because it uses motion control, which is not visible from a still image. A good example is Facebook&#8217;s <a href="https://github.com/facebook/pop" target="_blank">pop</a> for documentation and for UI, here is a good example from <a href="https://github.com/uzysjung/UzysAnimatedGifPullToRefresh" target="_blank">UzysAnimateGifPullToRefresh</a>:

  [![uzys image]({{ site.url }}/images/2014/09/screen-shot-2014-09-27-at-11-42-45-am.png)]({{ site.url }}/images/2014/09/screen-shot-2014-09-27-at-11-42-45-am.png){:target="_blank"}

#### Conclusion

Open source software can be as hard and complicated as you make it and some projects may require it be complicated. You are not alone, if your project is something developers need, I&#8217;m sure they will be happy to help you improve it. So whatever you are skilled in, focus on that, find the need and open source your idea.
