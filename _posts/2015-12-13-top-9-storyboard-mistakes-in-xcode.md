---
id: 285
title: Top 9 Storyboard Mistakes in Xcode
date: 2015-12-13T07:46:32+00:00
author: tfranklin
layout: post
guid: http://taylorfranklin.me/?p=285
permalink: /2015/12/13/top-9-storyboard-mistakes-in-xcode/
muut_last_active_tab:
  - 0
muut_use_muut_commenting:
  - 1
categories:
  - Uncategorized
tags:
  - autolayout
  - constraints
  - storyboard
  - top 9
  - xcode 7
---
I know there are many who live and die by programmatic iOS development, but for those who use storyboard or are willing to try, here are some tips on what I&#8217;ve learned. What I&#8217;ve seen in watching people try to learn storyboard and auto-layout, is that there are many nuances that seem obvious to me, having used storyboards for awhile now.

#### #1 &#8211; Update Your Label

We&#8217;ll get more advanced, but this is a very basic mistake where you try to change the text for a `UILabel` in the attributes inspector, but fail to press enter so the label does not get updated. So make sure you actually updated your label by pressing the enter key. The picture below is an example of changing the title text, but not confirming the change.

[<img class="aligncenter size-full wp-image-286" src="http://taylorfranklin.me/wp-content/uploads/2015/11/Screen-Shot-2015-11-22-at-5.19.15-PM.png" alt="Label not updated" width="643" height="185" srcset="http://taylorfranklin.me/wp-content/uploads/2015/11/Screen-Shot-2015-11-22-at-5.19.15-PM-300x86.png 300w, http://taylorfranklin.me/wp-content/uploads/2015/11/Screen-Shot-2015-11-22-at-5.19.15-PM.png 643w" sizes="(max-width: 643px) 100vw, 643px" />](http://taylorfranklin.me/wp-content/uploads/2015/11/Screen-Shot-2015-11-22-at-5.19.15-PM.png)

#### #2 &#8211; Unchecking &#8220;Constrain to margins&#8221;

You&#8217;ve probably seen this little checkbox before, but never really knew what it was doing.

[<img class="aligncenter size-full wp-image-290" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-06-at-10.17.38-PM.png" alt="constrain to margin" width="291" height="422" srcset="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-06-at-10.17.38-PM-207x300.png 207w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-06-at-10.17.38-PM.png 291w" sizes="(max-width: 291px) 100vw, 291px" />](http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-06-at-10.17.38-PM.png)

So you continue on, because why not constrain to margins, it&#8217;s already pre-selected. So yes, there are some benefits to using the margins in storyboard, like having a common element that multiple views are aligned by, as mentioned in this <a href="http://stackoverflow.com/questions/25807545/what-is-constrain-to-margin-in-storyboard-in-xcode-6" target="_blank">Stack Overflow post</a>. Although, aligning to a common element is possible with some other `UIView` or UI anything, but they will be less constant in position than the margin. In my experience though, 96% of the time, I uncheck that constrain to margins checkbox. Most of



the time, I want my views to stretch to the edges of the screen on whatever device they are on. The main point here is that that checkbox can be useful, but most of the time developers leave it checked, unaware that it will cause odd looking UI because they never intended to constrain to margins.

#### #3 &#8211; Forgetting to set your Delegate and Datasource

Ever wonder why your TableView, CollectionView, or any other view, adopting this familiar delegate/datasource protocol, was not being loaded with data. You then come to find that <span class="s1"><code>numberOfRowsInSection</code> and </span><span class="s1"><code>cellForRowAtIndexPath</code> is not being called. This leads to the discovery that you forgot to set your delegate and datasource in storyboard, like so:</span>

[<img class="aligncenter size-full wp-image-292" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.30.53-PM.png" alt="delegate & datasource" width="790" height="424" srcset="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.30.53-PM-300x161.png 300w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.30.53-PM.png 790w" sizes="(max-width: 790px) 100vw, 790px" />](http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.30.53-PM.png)

This used to get me every time and I still forget to do it sometimes, but now, I realize almost immediately what I did wrong.

Bonus: On the topic of forgetting things, save yourself the trouble and don&#8217;t forget to set the TableView/CollectionView Cell Identifier so that you can properly instantiate that cell in code.

#### #4 &#8211; Not Properly Removing Storyboard Object References

When you remove a referencing outlet from storyboard, oddly enough, you can still build & run the app, but if you run any code that used that reference, the app will crash. When you do it the opposite way and delete the IBOutlet reference in code, the reference in storyboard will give you a very tiny warning:

[<img class="aligncenter size-full wp-image-293" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.41.06-PM.png" alt="outlet warning" width="261" height="63" />](http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.41.06-PM.png)

Here, resultsTableView doesn&#8217;t have a valid code reference, which will of course, cause issues later. We simply need to remember to remove both references if choosing to remove one.

#### #5 &#8211; Using One Storyboard for Large Projects

Apple has made this as easy as possible now, with Xcode 7 and <a href="https://developer.apple.com/library/ios/recipes/xcode_help-IB_storyboard/Chapters/AddSBReference.html" target="_blank">Storyboard References</a>. The problem for many in the past is that you start to get over 10 or 20 View Controllers and your one storyboard becomes hard to manage. Meaning, you can&#8217;t easily find what you are looking for and the file itself takes longer to load. In addition, the likelihood of a merge conflict increases when you have many people working on one storyboard. That said, even if you are just working alone, it really helps with organization. Honestly, it seems natural, because we as programmers have very particular ways of organizing our code so why wouldn&#8217;t we at least have some way of organizing our UI.

Oh, just so I&#8217;m consistent, here is a screenshot of what Storyboard References look like:

[<img class="aligncenter size-full wp-image-295" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.52.23-PM.png" alt="Storyboard Ref" width="523" height="294" srcset="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.52.23-PM-300x169.png 300w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.52.23-PM.png 523w" sizes="(max-width: 523px) 100vw, 523px" />](http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-12.52.23-PM.png)

#### #6 &#8211; Custom Fonts on Attributed String Reset at Runtime

This mistake is a little more rare and may not come up very much, but it was perplexing for me at first. The issue happened when I had a `UILabel`, I set the attributed text and custom font that was imported into the project (I believe it was Lato).

<a href="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-5.42.12-PM.png" rel="attachment wp-att-298"><img class="aligncenter size-full wp-image-298" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-5.42.12-PM.png" alt="attributed string" width="650" height="175" srcset="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-5.42.12-PM-300x81.png 300w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-5.42.12-PM.png 650w" sizes="(max-width: 650px) 100vw, 650px" /></a>

Everything seemed to work fine until runtime when my attributed string reset to the default system font. I had no idea why and still don&#8217;t _really_ know, but in this case, custom fonts don&#8217;t work directly on storyboard. So 2 solutions is to just reset your font on that string in code, or use an `IBDesignable` class, as the <a href="http://stackoverflow.com/questions/25925914/attributed-string-with-custom-fonts-in-storyboard-does-not-load-correctly" target="_blank">this Stack Overflow post</a> suggests.

#### #7 &#8211; Debugging AutoLayout Constraints Without Using Identifiers

I know many of you have come across the following issue:

> Unable to simultaneously satisfy constraints, will attempt to recover by breaking constraint

And then you are given a list of constraints, that could be causing issues, in a not very human readable form. In order to make this debugging process easier, I suggest you at least give all possible issue causing constraints, an identifier:

<a href="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-5.49.49-PM.png" rel="attachment wp-att-300"><img class="aligncenter size-full wp-image-300" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-5.49.49-PM.png" alt="constraint ID" width="668" height="250" srcset="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-5.49.49-PM-300x112.png 300w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-5.49.49-PM.png 668w" sizes="(max-width: 668px) 100vw, 668px" /></a>

Identifiers on auto layout constraints is relatively new, but has been around awhile. It has certainly helped me figure out my auto layout issues and I hope this little tip helps you. For more info on using identifiers, check out this <a href="http://useyourloaf.com/blog/using-identifiers-to-debug-autolayout.html" target="_blank">post</a> on Use Your Loaf.

#### #8 &#8211; Not Testing on Multiple Screen Sizes

It&#8217;s easy to get your 4.7 inch iPhone 6 screen going in storyboard and never look back. The issue is you design your constraints for one screen and assume it should work well for all screens. The truth is, thats not always true since there is a large difference between a 4S and a 6 Plus. The key here is to, of course run on all different simulators (including iPad if you support that), but you can also test certain layouts quickly in storyboard. In Assistant Editor mode, you can select preview to get a rendering of the current screen you are working on in whatever size you want to view it in. The dropdown looks like this:

<a href="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.51-PM.png" rel="attachment wp-att-303"><img class="aligncenter size-full wp-image-303" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.51-PM.png" alt="dropdown" width="698" height="242" srcset="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.51-PM-300x104.png 300w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.51-PM.png 698w" sizes="(max-width: 698px) 100vw, 698px" /></a>

Using my <a href="https://itunes.apple.com/us/app/nyms-synonym-finder/id986235823?mt=8" target="_blank">Nyms</a> project, as in all the screenshots here, I can show the full result:<figure id="attachment_302" style="width: 1440px" class="wp-caption aligncenter">

<a href="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.42-PM.png" rel="attachment wp-att-302"><img class="wp-image-302 size-full" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.42-PM.png" alt="Screen Shot 2015-12-12 at 6.05.42 PM" width="1440" height="900" srcset="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.42-PM-300x188.png 300w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.42-PM-768x480.png 768w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.42-PM-1024x640.png 1024w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.42-PM-1200x750.png 1200w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.05.42-PM.png 1440w" sizes="(max-width: 1440px) 100vw, 1440px" /></a><figcaption class="wp-caption-text">I have a 4 inch iPhone on the left and a 5.5 inch iPhone on the right.</figcaption></figure> 

This example is not super compelling, but you see the effect. In addition, any changes you make on the left will immediately be reflected on the right. One more thing I&#8217;ll mention for supporting multiple screen sizes is <a href="https://developer.apple.com/library/ios/recipes/xcode_help-IB_adaptive_sizes/chapters/AboutAdaptiveSizeDesign.html" target="_blank">Size Classes</a>, which will truly allow you to develop for all iOS screens in one storyboard.

#### #9 &#8211; Not Taking Advantage of `UIStackView`

<a href="https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIStackView_Class_Reference/" target="_blank"><code>UIStackView</code></a> is new with iOS 9 and it fixes a lot of layout problems developers have had in the past. That problem is, how do you space multiple views perfectly across a screen? In the past, there was no good solution, causing developers to do odd workarounds. For example, you have 3 views that should be evenly horizontally spaced, so you put them all on a new parent view and have one hug the left, one hug the right, and one centered in the middle. This works great, but gets more complicated the more views you have to deal with. So please, use a vertical or horizontal stack view to space out your views. Here is a simple example:

<a href="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.22.06-PM.png" rel="attachment wp-att-304"><img class="aligncenter size-full wp-image-304" src="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.22.06-PM.png" alt="stack view" width="656" height="156" srcset="http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.22.06-PM-300x71.png 300w, http://taylorfranklin.me/wp-content/uploads/2015/12/Screen-Shot-2015-12-12-at-6.22.06-PM.png 656w" sizes="(max-width: 656px) 100vw, 656px" /></a>

&nbsp;

#### Last Thought

It&#8217;s easy to make comparisons of Xcode with other mobile IDEs, but I must say storyboards have gotten better over the years. Some improvements I&#8217;ve seen are, in the way you add constraints to support many screen sizes and also the amount of customization allowed on each UIKit component. Thanks for reading and please let me know any mistakes you&#8217;ve made in storyboard and the fixes to combat them.

<!-- AdSense Now! Lite: PreFiltered - NoAds [ WP is not in the loop. ] -->