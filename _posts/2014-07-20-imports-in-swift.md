---
id: 45
title: Imports in Swift
date: 2014-07-20T16:41:14+00:00
author: tfranklin
layout: post
guid: http://cleancrispcode.wordpress.com/?p=45
permalink: /2014/07/20/imports-in-swift/
geo_public:
  - 0
muut_post_domain:
  - taylorfranklin.me
muut_use_muut_commenting:
  - 1
muut_last_active_tab:
  - commenting-tab
muut_post_settings:
  - 'a:1:{s:19:"commenting_settings";a:3:{s:11:"enabled-tab";s:1:"1";s:4:"type";s:4:"flat";s:15:"disable_uploads";s:1:"0";}}'
categories:
  - iOS
tags:
  - autocomplete
  - bridging header
  - imports in swift
  - ios7
  - ios8
  - programming
  - swift
  - swift programming
  - xcode 6
---
### One of greatest features of convenience that Apple released in the Swift programming language was deleting the necessity to import user created files.

The days of imports looking like this:

<pre class="theme:classic lang:objc decode:true ">#import &lt;UIKit/UIKit.h&gt;
#import "GameBoardViewController.h"
#import "AppDelegate.h"
#import "BGCurrentUserController.h"
#import "BoardThemeModel.h"
#import &lt;FacebookSDK/FacebookSDK.h&gt;
#import "FBGame.h"
#import "GameManager.h"
#import "GameListViewController.h"
#import "GridCollectionViewLayout.h"
#import "NSString+XQueryComponents.h"
#import &lt;Parse/Parse.h&gt;
#import "PhraseCell.h"
#import "PushNotificationUtility.h"
#import "UIAlertViewHelper.h"
#import "UIDeviceMacros.h"
#import "StaticVariables.h"
#import "FBPhrase.h"
#import "GameBoardController.h"</pre>

&#8230;are over for native iOS developers.

Instead, this is what it might look like in Swift:
  
`import UIKit`

In addition, you don&#8217;t have to import System frameworks (i.e. CoreData, UIKit) manually from your build phases menu. Although, this feature has been around since Xcode 5 at least, but it is still really nice! For example, more than half of the following includes are not necessary:<figure id="attachment_50" style="width: 1173px" class="wp-caption aligncenter">

[<img class="wp-image-50 size-full" src="http://taylorfranklin.me/wp-content/uploads/2014/07/screen-shot-2014-07-20-at-5-29-55-pm.png" alt="Build Phases" width="1173" height="434" srcset="http://taylorfranklin.me/wp-content/uploads/2014/07/screen-shot-2014-07-20-at-5-29-55-pm-1024x378.png 1024w, http://taylorfranklin.me/wp-content/uploads/2014/07/screen-shot-2014-07-20-at-5-29-55-pm.png 1173w" sizes="(max-width: 1173px) 100vw, 1173px" />](http://taylorfranklin.me/wp-content/uploads/2014/07/screen-shot-2014-07-20-at-5-29-55-pm.png)<figcaption class="wp-caption-text">Don&#8217;t do this! (anymore)</figcaption></figure> 

&nbsp;

Another nice thing I enjoy about Xcode 6 and Swift is that the vast majority of Objective-C libraries and frameworks work just as well in Swift as they do in Objective-C. The time saver in all of that is the autocomplete **converts Obj-C function declarations into a clean Swift format**, even if they used blocks or something out of the ordinary.

&nbsp;

Bridging headers seem kinda weird, but really they are not complicated at all. Also, with the autocomplete features mentioned above, you won&#8217;t even notice there are Objective-C classes in your project. Check out the docs on [Using Swift and Obj-C in the same project](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html#//apple_ref/doc/uid/TP40014216-CH10-XID_76).

&nbsp;

Anyway, I could go on about the pros of these here new innovations, but check em out for yourself or wait until the Fall when they should all be released with iOS 8. Thanks for the read!

(Screenshots coming soon once these products are out of Beta in compliance with the [Developer Agreement](https://developer.apple.com/programs/terms/ios/standard/ios_program_standard_agreement_20140602.pdf))

<!-- AdSense Now! Lite: PreFiltered - NoAds [ WP is not in the loop. ] -->