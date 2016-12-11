---
published: false
---
My name is Taylor and since 2013 I have been working heads down in Swift iOS development. I did a lot of fun work in that time, made some great UIs, coded some cool features, but I felt it was time to expand my skills. Luckily, Apple open-sourced the Swift programming language around a year ago from today. With that and almost immediate work being done with Swift on the server, I was provided with a unique oppretunity to get out of my comfort zone, but still visit often. I switched gears in March 2016 and began focusing on Swift server-side app development, here is how it went.

![swift-logo]({{site.baseurl}}/images/2016/12/apple-swift-logo.jpg)

### The Transition

The initial transition was slow going at first because I was put on the [Kitura](https://github.com/IBM-Swift/Kitura) team for a short time. If I remember correctly, I made 2 server apps in college that used technologies like Node.js and Express. Unfortunatly, it had been awhile and Javascript always found a way to confuse me 😬 . Nevertheless, I continued to learn about this server-side framework, how routes are made, and the various responses you may want to send back to your client. Simple stuff for the server-side expert, but a great step for me.

### BluePic

My next endeavor into server-side Swift came with my work on [BluePic](https://github.com/IBM-Swift/BluePic), an iOS application that had a recently added Swift server component. Now, this project is what really helped me hone my skills because it was the best of both worlds. It had an iOS component which what I was familiar with, but it also had a basic server setup with more work to be done. Honestly, this is what I would recommend for anyone looking to transition from iOS to Swift server-side dev. That is, start with what you know (iOS) and instead of using some MBaaS system for a database (like what Parse used to be), deploy your own server and connect it to a database.

During this project, my mind really started to connect the dots by writing iOS client code and server code. BluePic is interesting because it has a server component, but that is just a piece of the story because that server connects to many services, such as our database, file storage, and image recognition service. I not only had to think about how my iOS app can make REST calls to a server, I also had to consider how my server will connect to my services. After months of work though, I had great understanding of how all these things work together in a beautiful modular way. If you are curious, the current BluePic architecture can be found [here](https://github.com/IBM-Swift/BluePic/blob/master/Imgs/architecture.png)

### Swift is a Bridge

I occassionally have to look at Javascript code because maybe I'm trying to reproduce a similar functionality in my Swift code, but it takes a good while to really grasp what is going on. So I must say there is a huge benifit to looking at server-side code that is written in Swift. The time it takes to digest someone elses code (or even my own after a few months 😏) is vastly decreased if it is in a familiar language. As I have been stating this whole post, in many ways, Swift has bridged the gap for me in the understanding of how servers work.

Some old school programmers might say this is basic knowledge that every programmer should know. My response to them is, I disagree, because there are so many libraries, frameworks, and abastractions away from the "basics" that it isn't required to know the inner workings of a server. For some, this is fine, but as some point, a programmer may want to know more and that is what I did. We have a great privlidge these days to be able to pick most of what we want to learn. It may very well bite us in the butt, not learning a particular technology, but in large part, I believe you can make a living, feeling accomplished in your work. All that said, if you are remotely interested in server-side Swift, then don't POST-pone, GET a project going, and PUT your mind to good use. Sorry for the RESTful jokes, puns are cool.

### What Came Next

After my work on BluePic, I got to work on porting a Javascript web framework to a Swift framework. This was another great way to transition from iOS/Swift programming to server-side Swift. It allowed me to create a framework, which also exsist in iOS, but confront it with a server in mind. The cool thing is for you, that based on what your framework does, it could easily be used for iOS or server projects with the help of the [Swift Package Manager](https://swift.org/package-manager/).

I now spend a lot of my time creating compelling applications that use server-side Swift. Partly to show off the capabilities of what server-side Swift can do and partly because I enjoy rounding out my skills as a programmer. While I liked being a go-to iOS developer, that is not all I wanted to be and the open sourcing of Swift happened at just the right time for me.

### Give It A Try

If all you know is iOS, it can feel risky branching out with any signifigant amount of your time, but I would argue it's worth it. Yes, I still get my [iOS Dev Weekly](https://iosdevweekly.com/) emails and try to stay up to date, but just a reminder, server-side Swift and iOS development are not mutually exclusive.

To start real simple, just check out the [Kitura-Starter](https://github.com/IBM-Bluemix/Kitura-Starter) project and deploy it on the cloud. I suggest moving on to BluePic as a second more complex example. There are really a lot of great resources for learning server-side Swift, one is the [IBM Swift Engineering Blog](https://developer.ibm.com/swift/blogs/). For the credibility purposes, Apple is officially on board for server-side Swift and has a [dedicated project and work group](https://swift.org/server-apis/) for it.

I hope you take the time to experiment or create something real with Swift on the server. It's a growing eco-system of developers, similar to the iOS community, given that they share a programming language. So you can either enter into this young community or jump on the bandwagon later 😄


