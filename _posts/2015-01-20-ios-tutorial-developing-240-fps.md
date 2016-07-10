---
id: 218
title: 'iOS Tutorial: Developing with 240 FPS'
date: 2015-01-20T11:45:32+00:00
author: tfranklin
layout: post
permalink: /2015/01/20/ios-tutorial-developing-240-fps/
comments: true
categories:
  - iOS
  - iOS Tutorials
tags:
  - 240 fps
  - avcapturesession
  - iPhone 6
  - iPhone 6 Plus
  - slomo
  - tutorial
---
I think every person with an iPhone 6 or 6 Plus has enjoyed the slo-mo feature that comes with their device. Why, you say? Because you can make videos of basketball tricks, that you can somehow still do after all these years, like this <a href="https://flic.kr/p/qQHu1i" target="_blank">one of me</a>, or maybe capture a majestic pour of <a href="https://flic.kr/p/pU6CBp" target="_blank">beer</a>!

A lot can happen in 240 frames per second, so I&#8217;m going to show you a quick iOS tutorial using `AVCaptureSession` on how you can take advantage of this awesome capability in your next app. I haven&#8217;t used `AVCaptureSession` very much, so this was a great learning opportunity. I must say, it is simpler than you might expect. While using `UIImagePickerController` as your camera is pretty stinkin easy, using the `AVFoundation` class is not that bad.

### Let Us Begin

We&#8217;ll start by assuming you have a basic UIViewController set up. There are 3 main objects you will need:

<pre class="theme:classic lang:swift decode:true" title="The variables">let captureSession = AVCaptureSession()
var videoPreviewLayer: AVCaptureVideoPreviewLayer?
var captureDevice: AVCaptureDevice?</pre>

Now in your `viewDidLoad`, you need to make sure your `AVCaptureDevice` is ready and able:

<pre class="theme:classic lang:swift decode:true" title="capture device set up">captureSession.sessionPreset = AVCaptureSessionPresetHigh
        
let devices = AVCaptureDevice.devices()
        
// 1
for device in devices {
    // 2
    if (device.hasMediaType(AVMediaTypeVideo)) {
        // 3
        if(device.position == AVCaptureDevicePosition.Back) {
            // 4
            captureDevice = device as? AVCaptureDevice
            // 5
            if captureDevice != nil {
                startSession()
            }
        }
    }
}</pre>

  1. First thing here is just iterating through the available devices.
  2. Ensure the device you are using can even capture video.
  3. Make sure you are using the back facing camera (the front-facing camera doesn&#8217;t support 240 FPS).
  4. Assign the device that matches the previous criteria for later use.
  5. Lastly, call a method to actually start the video session.

### Start Your Session

For this next part, you will run through a few steps to initialize your session, device, and previewLayer.

<pre class="theme:classic lang:swift decode:true" title="session start">func startSession() {

    // 1    
    var error: NSError?
    captureSession.addInput(AVCaptureDeviceInput(device: captureDevice, error: &error))
        
    if error != nil {
        println("Error: \(error?.localizedDescription)")
    }

    // 2    
    configureDevice()
    
    // 3    
    videoPreviewLayer = AVCaptureVideoPreviewLayer(session: captureSession)
    self.view.layer.addSublayer(videoPreviewLayer)
    videoPreviewLayer?.frame = self.view.layer.frame
    captureSession.startRunning()
}</pre>

Round 2, here&#8217;s what&#8217;s happening:

  1. `addInput` is where you actually associate your capture device with your capture session. If everything was set up correctly, there should be no errors to print out.
  2. This is where you will configure the various options on the capture device. _Scroll down for more on that_.
  3. Then set up the the `AVCaptureVideoPreviewLayer` so your UI will show what the camera is reading in.

### Getting Just the Right Frame Rate

When researching what camera capabilities developers had access to with the new camera hardware on the iPhone 6 and 6 Plus, I found the following <a href="https://developer.apple.com/library/ios/technotes/tn2409/_index.html" target="_blank">technical documentation</a>. It contains details on many of the new features Apple has allowed developers to access, such as optical image stabilization and focus pixels. That ties in to the last piece of this tutorial:

<pre class="theme:classic lang:swift decode:true " title="device config">func configureDevice() {
    if let device = captureDevice {

        // 1
        for vFormat in captureDevice!.formats {

            // 2
            var ranges = vFormat.videoSupportedFrameRateRanges as [AVFrameRateRange]
            var frameRates = ranges[0]

            // 3
            if frameRates.maxFrameRate == 240 {

                // 4    
                device.lockForConfiguration(nil)
                device.activeFormat = vFormat as AVCaptureDeviceFormat
                device.activeVideoMinFrameDuration = frameRates.minFrameDuration
                device.activeVideoMaxFrameDuration = frameRates.maxFrameDuration
                device.unlockForConfiguration()
                    
            }
        }
    }
        
}</pre>

  1.  First thing here, you want to loop through the available formats on the chosen device, with `.formats` representing an array of `AVCaptureDeviceFormat` objects.
  2. Here, you extract the `AVFrameRateRange` object from each format.
  3. Loop through formats until you find one that supports 240 fps.
  4. Lock configuration, set the current format along with the frame rates you want with `maxFrameDuration` being the most important part.

**Pitfalls**

You need to be aware of a few things that could cause you some frustration if not taken care of.

  * Changing format values like `activeFormat` and neglecting to call `lockForConfiguration` will cause your app to terminate.
  * Changing properties like `activeVideoMinFrameDuration` before setting your `activeFormat` will also terminate your app. Additionally, forgetting to set the `activeFormat` at all&#8230;will terminate your app.
  * Lastly, be aware if 240 FPS is not available on your device, it will fallback to the default frame rate for your device, but I must say, it will not terminate your app &#128515;

### Slo-mo Activated!

Now, you can implement slo-mo video capture, outside of the default Camera app. In addition to that, this is a great introduction to `AVFoundation` and video capture in iOS development. I didn&#8217;t cover saving the video in this iOS tutorial, but I may in the future (hint: check out `AVCaptureOutput`). Even if this is your first time to my blog, let <a href="https://twitter.com/tfrank64" target="_blank">me</a> know what you liked and what you found most helpful. Have a good one!
