---
id: 6
title: Multiple Taps on UICollectionView Cells
date: 2014-01-30T18:48:44+00:00
author: tfranklin
layout: post
permalink: /2014/01/30/multiple-taps-on-uicollectionview-cells/
comments: true
categories:
  - iOS
tags:
  - cell
  - double tap
  - ios
  - mbprogresshud
  - stackmob
  - stackoverflow
  - thread
  - uicollectionview
---
I have been working on an iOS app at work for a few months now and it is coming close to completion.

Problem:

The issue I had today was that multiple taps on a single or many `UICollectionView` Cells would cause the my app to freeze. I narrowed down the issue to be the syncWithServer method I use with the StackMob iOS SDK (Update: StackMob was shutdown in 2014). This method supposedly runs in the background, but I found with many taps in a short amount of time, it got overloaded (comments on why are welcome). The weird thing is that I have a `UITableView` with a very similar implementation and it does not run into this issue. The reason being, `UITableView` decides not to handle any taps over one at a time, without doing some trick. So I chose a similar solution to fix the issue mentioned above.

Solution:

After trying a timer and custom background queue workaround, I simply tried to disable user interaction with the collection view until the completion callback for the syncWithServer method started. This is seemed to work fine, but I chose to go with the better design choice and put the good ol&#8217; MBProgressHUD. The bonus that comes with that is the fact that it disables interaction with the current view while it is up. This worked well in my favor because then I just needed the following two lines of code:

```objective-c
[AppDelegate showGlobalProgressHUDWithTitle:@"Updating..."];
[AppDelegate dismissGlobalHUD];
```

Those helper methods, of course, are from the following StackOverflow <a href="http://stackoverflow.com/questions/12033080/use-of-mbprogresshud-globally-make-it-singleton" target="_blank">post</a>. I&#8217;m sure there are some downsides to the Global Progress HUD since it is not run on a background thread, but it works well. I was able to dismiss the HUD because of an `NSNotifcation` posted from the syncWithServer Completion block. Those two line (in different locations of course) fixed my issue and keeps my app from freezing.

Thanks for reading! I look forward to more posts.
