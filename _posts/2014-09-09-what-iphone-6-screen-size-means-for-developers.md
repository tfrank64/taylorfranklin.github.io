---
id: 65
title: What iPhone 6 screen size means for developers
date: 2014-09-09T22:34:38+00:00
author: tfranklin
layout: post
guid: http://cleancrispcode.wordpress.com/?p=65
permalink: /2014/09/09/what-iphone-6-screen-size-means-for-developers/
geo_public:
  - 0
mashsb_shares:
  - 100,170,276,329,486,583,635,736,875,0
mashsb_timestamp:
  - 1413147024
categories:
  - iOS
tags:
  - 1136x640
  - 1334x750
  - 1920x1080 iPhone
  - 6 plus
  - aspect ratio
  - cgrect
  - ios 8
  - iPhone
  - iPhone 6
  - iPhone 6 Plus
  - iPhone aspect ratio
  - iphone dimensions
  - iPhone frame size
  - keynote
  - writedraw
  - writedrawgame
---
How is it with the new iPhone 6 that my app, created for iOS 7, still works well in iOS 8 on an iPhone 6 and 6 Plus?!

I modified my code to work with iOS 8, but have not touched it with these new iPhone sizes and resolutions. Some may call it magic, some may just be happy to not have extra work, but there is a reason.

The reason being the same as it was for iPhone 5 and that is the **code frames and sizing don&#8217;t work in actual ****resolution**. For example, the iPhone 6 has a resolution of 1334 x 750, but my code is written to think the frame is 320 x 568 (or 480 height for 4S). This remains the same for the new set of iPhones. So here is the data I found when logging the frame size of my app on these different devices, using the iOS Simulator in iOS 8.

\* All tests were done in the simulator, not on a physical device \*



So there you go, it is as if the resolution has changed, but the devices still have the same ratio as the iPhone 5. <!--more-->

Looking at these frames, setting anything past the 568 y value, might put it off the screen on an iPhone 6, so I tried just that&#8230;

What I found was that _the object was pushed off screen_ kind of as I expected. All this considering that the app, which was targeted towards iOS 7 is being run in a scaled mode. _That is the secret_ on why my app looks as expected, it is not actually changing the frame size for apps that were not made for these bigger screen sizes. For apps built for iOS 8, developers will be using the resolutions mentioned in the following paragraph.

**Important Update: **As I hear comments and work more with the new Xcode, it seems our iOS 7 apps may be running in a scaled/compatibility mode. The screen resolutions should actually be 375 x 667 for the iPhone 6 and 414 x 736 for the iPhone 6 Plus. So that is what a developer will be dealing with if they are using frames. The point remains the same though for those of us using auto layout, I believe there is a way to set up auto layout to work now and in the future for whatever screen sizes Apple may throw at us. This is especially clear with the resizable iPhone option in the iOS Simulator. For more details about the pixel details, check out PaintCode&#8217;s [article](http://www.paintcodeapp.com/news/iphone-6-screens-demystified).

#### To update your iOS 7 app to utilize the new iPhone 6 sizes:

Within Xcode, click on your .xcassets file and add a &#8220;New Launch Image&#8221;[<img class="aligncenter wp-image-80" src="http://taylorfranklin.me/wp-content/uploads/2014/09/screen-shot-2014-09-11-at-6-11-02-pm.png?w=1024" alt="Screen Shot 2014-09-11 at 6.11.02 PM" width="901" height="552" srcset="http://taylorfranklin.me/wp-content/uploads/2014/09/screen-shot-2014-09-11-at-6-11-02-pm-1024x627.png 1024w, http://taylorfranklin.me/wp-content/uploads/2014/09/screen-shot-2014-09-11-at-6-11-02-pm.png 1079w" sizes="(max-width: 901px) 100vw, 901px" />](http://taylorfranklin.me/wp-content/uploads/2014/09/screen-shot-2014-09-11-at-6-11-02-pm.png)

From there just add a 1242 x 2208 image to the Retina HD 5.5 spot and/or a 750 x 1334 image to the Retina HD 4.7 spot and your app should now recognize these new screen sizes as you would expect. Make sure the set of launch images you want to use is named LaunchImage in your .xcassets and not LaunchImage-1 or something like that.

For my app, things still looked pretty good, they just look more spread out since there is more screen space. In some part of the app though, there is a lot of white space for the same reason.

&nbsp;

[<img class="aligncenter size-medium wp-image-67" src="http://taylorfranklin.me/wp-content/uploads/2014/09/screen-shot-2014-09-09-at-11-23-26-pm.png?w=300" alt="Screen Shot 2014-09-09 at 11.23.26 PM" width="300" height="147" srcset="http://taylorfranklin.me/wp-content/uploads/2014/09/screen-shot-2014-09-09-at-11-23-26-pm-300x147.png 300w, http://taylorfranklin.me/wp-content/uploads/2014/09/screen-shot-2014-09-09-at-11-23-26-pm.png 375w" sizes="(max-width: 300px) 100vw, 300px" />](http://taylorfranklin.me/wp-content/uploads/2014/09/screen-shot-2014-09-09-at-11-23-26-pm.png)

### iPhone 6 Aspect Ratio Comparison

Here are the different aspect ratios just so you know.

iPhone 5S: 40:71

iPhone 6: 375:667

iPhone 6 Plus: 9:16

Now these calculations are precise so they seem very different, but it turns out, Apple has hardly changed this ratio at all throughout their newest iPhone models. If you reduce those numbers they are different, ever so slightly.

Using the 2 iPhone 6 aspect ratios on a _320 width_, the height always comes to **569**, which is one pixel off the iPhone 5S frame height of 568. This is not a coincidence and I think it was really smart of Apple to stick with this one aspect ratio for all their new iPhones. New iPhones were announced today and they are supposedly &#8220;Bigger than bigger&#8221; according to Apple, so maybe we will see what means soon. The new iPhones are more than just big, I wrote a [quick tutorial](http://taylorfranklin.me/2014/11/17/developing-for-iphone-barometer/) on the barometer included with the iPhone 6 and 6 Plus. The impact of these new devices, I think will be a positive one for users and developers alike.

<!-- AdSense Now! Lite: PreFiltered - NoAds [ WP is not in the loop. ] -->