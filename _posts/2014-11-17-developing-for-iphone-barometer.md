---
id: 136
title: Developing for the iPhone Barometer
date: 2014-11-17T03:17:12+00:00
author: tfranklin
layout: post
guid: http://taylorfranklin.me/?p=136
permalink: /2014/11/17/developing-for-iphone-barometer/
muut_use_muut_commenting:
  - 1
muut_last_active_tab:
  - 0
categories:
  - iOS
tags:
  - CMAltimeter
  - core motion
  - iphone barometer
  - startRelativeAltitudeUpdatesToQueue
---
We heard that the iPhone 6 and iPhone 6 Plus were shipped with barometers inside of them, but we really haven&#8217;t heard much about them. I will go through a rather quick tutorial on how to access the barometer with the current API available to developers.

### CMAltimeter

The main class developers need to be concerned with for this task, is the `CMAltimeter` class. Note, for fairly obvious reasons, the `CMAltimeter` class will only be effective on a physical device. To begin, start with a basic subclass of `UIViewController` and import the Core Motion library:

<pre class="theme:classic lang:swift decode:true">import CoreMotion</pre>

Next, we need to create a `CMAltimeter` object, but a <span style="color: #ff0000;">common pitfall</span> is to create it in the `viewDidLoad()`. <!--more-->If done that way, the altimeter won&#8217;t be accessible when we need to call a method on it. Nevertheless, go ahead and create your CMAltimeter object just before the viewDidLoad():

<pre class="theme:classic lang:swift decode:true">let altimeter = CMAltimeter()</pre>

I recommend creating a simple UI in Storyboard so you can actually begin tracking the altitude and pressure later on. Something like the following will suffice:

[<img class="aligncenter size-full wp-image-182" src="http://taylorfranklin.me/wp-content/uploads/2014/11/Screen-Shot-2014-11-10-at-7.01.15-PM.png" alt="UIButton action" width="623" height="167" srcset="http://taylorfranklin.me/wp-content/uploads/2014/11/Screen-Shot-2014-11-10-at-7.01.15-PM-300x80.png 300w, http://taylorfranklin.me/wp-content/uploads/2014/11/Screen-Shot-2014-11-10-at-7.01.15-PM.png 623w" sizes="(max-width: 623px) 100vw, 623px" />](http://taylorfranklin.me/wp-content/uploads/2014/11/Screen-Shot-2014-11-10-at-7.01.15-PM.png)As you can see, I just created a button and IBAction so we are ready to begin monitoring with our barometer.

  1. In that start method created, we need to check if relativeAltitude is even available with the following method: <a href="https://developer.apple.com/library/IOs//documentation/CoreMotion/Reference/CMAltimeter_class/index.html#//apple_ref/occ/clm/CMAltimeter/isRelativeAltitudeAvailable" target="_blank"><code>CMAltimeter.isRelativeAltitudeAvailable</code></a>
  2. If that returns true, you can then begin monitoring altitude change with <a href="https://developer.apple.com/library/IOs//documentation/CoreMotion/Reference/CMAltimeter_class/index.html#//apple_ref/occ/instm/CMAltimeter/startRelativeAltitudeUpdatesToQueue:withHandler:" target="_blank"><code>startRelativeAltitudeUpdatesToQueue</code></a>
  3. If there are no errors, you should be able to retrieve data from the <a href="https://developer.apple.com/library/IOs//documentation/CoreMotion/Reference/CMAltitudeData_class/index.html#//apple_ref/occ/instp/CMAltitudeData/relativeAltitude" target="_blank"><code>relativeAltitude</code></a> and <a href="https://developer.apple.com/library/IOs//documentation/CoreMotion/Reference/CMAltitudeData_class/index.html#//apple_ref/occ/instp/CMAltitudeData/pressure" target="_blank"><code>pressure</code></a> properties.

Here is those 3 pieces together.

<pre class="theme:classic nums:false lang:swift decode:true ">// 1
if CMAltimeter.isRelativeAltitudeAvailable() {
    // 2
    altimeter.startRelativeAltitudeUpdatesToQueue(NSOperationQueue.mainQueue(), withHandler: { data, error in
        // 3
        if (error == nil) {
            println("Relative Altitude: \(data.relativeAltitude)")
            println("Pressure: \(data.pressure)")
        }
    })
}</pre>

If you set up your project correctly and run the code above, you should get continuous updates of `CMAltitudeData` as it comes in. The relative altitude you get back is in meters which makes it very easy to tell if it is working. Now, the data you get back from pressure is in <a href="http://www.aqua-calc.com/what-is/pressure/kilopascal" target="_blank">kilopascals</a> which of course, is a measurement of pressure similar to Pascals or PSI (pounds per square inch). To give you some perspective, it is _99.36 kilopascals_ in the room I am in, which converts to _14.41 PSI_. To understand that number, your car most likely has a tire pressure of around _30 to 35 PSI_. While, you won&#8217;t be ready to setup your own meteorologist station, you will be a little smarter about the world directly around you.

Here are some examples of how the previously mentioned data is useful:

  * With the relative altitude, you can track how high a user has ascended or how low they have descended since starting your app. The obvious use would be a Hiking application, but I&#8217;m sure there are more creative uses for that.
  * With the pressure reading of your currently altitude you can gather more weather related data that apps like <a href="https://itunes.apple.com/us/app/weathersignal-barometer-for/id924529896?ls=1" target="_blank">WeatherSignal</a> have done. They had a crowd sourced weather app using the barometer on certain Android devices, but now that iPhone has one, they are included in the data collecting fun.

The data to be gathered through the iPhone&#8217;s barometer seems rather thin, so it would be interesting to see Apple beef it up at some point. Including data like actual elevation above sea level in a simple API would be amazing. Anyway, these are useful and concise classes that are actually pretty easy to use. You can see my entire view controller for this tutorial, excluding the storyboard, in the following <a href="https://gist.github.com/tfrank64/096cdb916f340c740a95" target="_blank">Github Gist</a>.

<!-- AdSense Now! Lite: PreFiltered - NoAds [ WP is not in the loop. ] -->