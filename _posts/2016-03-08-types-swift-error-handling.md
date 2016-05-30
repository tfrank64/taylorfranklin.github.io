---
id: 321
title: Types of Swift Error Handling
date: 2016-03-08T19:00:28+00:00
author: tfranklin
layout: post
guid: http://taylorfranklin.me/?p=321
permalink: /2016/03/08/types-swift-error-handling/
muut_last_active_tab:
  - commenting-tab
muut_post_settings:
  - 'a:1:{s:19:"commenting_settings";a:3:{s:11:"enabled-tab";s:1:"1";s:4:"type";s:4:"flat";s:15:"disable_uploads";s:1:"0";}}'
muut_post_domain:
  - taylorfranklin.me
muut_comments_count:
  - 0
categories:
  - iOS
  - Swift
tags:
  - do catch
  - error handling
  - ios
  - swift
---
I recently did an informal presentation on error handling in Swift to inform others on the variety of options we have with Swift. I used an Xcode playground to present this topic and it ended up surprising all of us with how many interesting features playgrounds have. That playground can be downloaded [here]({{ site.url }}/images/2016/03/ErrorHandles.playground.zip) or you can just read this post for info (be sure to check out the playground fun at the bottom).

There are 4 main types of error handling <a href="https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/ErrorHandling.html" target="_blank">Apple mentions</a> with Swift.

### 1. Propagate the error from a function to the code that calls the function

<pre class="lang:swift decode:true ">enum WindStrength: ErrorType {
    case Gust
    case Gale
    case Hurricane
}

class WeatherManager {
    
    // in MPH
    var currentWindSpeed = 34
    
    func isWeatherSafe() throws -&gt; Bool {
        
        if currentWindSpeed &gt;= 25 && currentWindSpeed &lt;= 38 {
            throw WindStrength.Gust
        } else if currentWindSpeed &gt;= 39 && currentWindSpeed &lt;= 72 {
            throw WindStrength.Gale
        } else if currentWindSpeed &gt;= 73 {
            throw WindStrength.Hurricane
        }
        
        // good for cleanup, such as closing a file that was opened
        defer {
            print("do clean up task")
        }
        
        return true
        
    }
    
}
</pre>

<p class="p1">
  I would use this when I have a method I will call a lot and a method that could have multiple things go wrong for which the method caller will need to know about. No user or dev likes the description-less error, such as &#8220;An error occurred&#8221;.
</p>

### 2. Handle the error using a do-catch statement



<pre class="lang:swift decode:true ">var weatherManager = WeatherManager()
var isSafe: Bool? {
    didSet {
        print("Must be safe")
    }
}

do {
    isSafe = try weatherManager.isWeatherSafe()
} catch WindStrength.Gust {
    print("You should go somewhere safe")
} catch WindStrength.Gale {
    print("Strong winds, to say the least")
} catch WindStrength.Hurricane {
    print("Hurricane winds, best of luck")
} catch {
    print(error)
}</pre>

Very similar to try-catch statements in other languages, it is more focused on how you handle an error result rather than translating something else into an error case. For example, method #1 in this list is more for the person writing a framework, however simple, and method #2 here, is for the person consuming that framework.

### 3. Handle the error as an optional value

<pre class="lang:swift decode:true ">// If any error, value is nil
if let _ = try? weatherManager.isWeatherSafe() {
    print("Weather is fine, wind is calm")
} else {
    print("error")
}

// Bonus: ?? operator takes the value that is not nil, if possible
var myValue = try? weatherManager.isWeatherSafe()
let safeWeather = myValue ?? false</pre>

This is essentially doing the optional unwrap you all should be familiar with by now. The difference with this one is that the `try?` keyword is used because we don&#8217;t care what type of error we get back, just that we get an error. In addition, there is a `try!` which should very rarely be used, in fact, you _shouldn&#8217;t_ ever have to use it, nevertheless, here is an example:

<pre class="lang:swift decode:true">let photo = try! loadImage("./Resources/John Appleseed.jpg")</pre>

### 4. Assert that an error will not occur

<pre class="lang:swift decode:true ">func transformString(string: String?) -&gt; String {
    assert(string != nil, "Invalid parameter")
    return string! + "_transformed"
}

transformString("hi")</pre>

This is probably the least common type of &#8220;error handling&#8221; because it simply crashes your app if the error occurs. You should check out this more thorough <a href="http://blog.krzyzanowskim.com/2015/03/09/swift-asserts-the-missing-manual/" target="_blank">blog article</a> on asserts by Marcin Krzyżanowski.

### 

### Keep in Mind

Exceptions do not exist in Swift, but they do exist in Objective-C. It is really easy to get these two things mixed up in your head, but they have a very key difference. Exceptions are more for **informing the developer**, because they will crash your app when thrown and not handled. While errors, are more for **informing the user** of an issue while keeping your app running.

For reference, here is an example of error handling in Objective-C

<pre class="lang:objc decode:true ">NSError *anyError;
BOOL success = [receivedData writeToURL:someLocalFileURL
                                options:0
                                  error:&anyError];

if (!success) {
    NSLog(@"Write failed with error: %@", anyError);
    // present error to user
}</pre>

Pretty different from Swift, considering error pointers are passed to methods by reference to be updated by the method being called.

One more feature, is that you can cast do-catch error objects to an `NSError` object when by default, they are of type `ErrorType`

<pre class="lang:swift decode:true">// Catch clauses

let fileManager = NSFileManager.defaultManager()
let fromURL = NSURL(fileURLWithPath: "/path/to/old")
let toURL = NSURL(fileURLWithPath: "/path/to/new")
do {
    try fileManager.moveItemAtURL(fromURL, toURL: toURL)
} catch let error as NSError {
    print("Error: \(error.localizedDescription)")
}</pre>

<p class="p1">
  <span class="s1">For additional reading and an exhaustive explanation of why Swift error handling is the way it is, go to <a href="https://github.com/apple/swift/blob/master/docs/ErrorHandlingRationale.rst" target="_blank"><span class="s2">Swift Error Handling Rationale</span></a></span>
</p>

### Wrap Up

For many iOS tasks, I can get by with just optional unwrapping, but sometimes you need a little something more that explains errors more effectively, such as a do-catch statement. This is especially true when you are writing a framework with a lot of network calls. I hope this post was a good overview and that Swift error handling is not something you need to shy away from, but rather a great tool for developers and your user experience.

<!-- AdSense Now! Lite: PreFiltered - NoAds [ WP is not in the loop. ] -->