---
id: 333
title: The Default Memberwise Initializers Headache
date: 2016-07-10T17:48:44+00:00
author: tfranklin
layout: post
permalink: /2016/07/10/the-default-memberwise-initializers-headache/
comments: true
categories:
  - Swift
tags:
  - ios
  - swift
  - framework
  - troubleshoot
---

I ran into a problem recently on a Swift server-side project that uses <a href="https://github.com/IBM-Swift/Kitura" target="_blank">Kitura</a>. The problem though, can happen to anyone using Swift in a project. I was using an external framework that was imported through the Swift Package Manager. In attempting to use it, I tried to use a certain class, lets call it `Bulbasaur`, and I would continually get the following error:

> Bulbasaur initializer is inaccessible due to internal protection level

The code causing this issue looked like this:

```
let myFirstPokemon = Bulbasaur(type:"Grass", maxHP: 20)
```

I checked the source code for this framework and did not see anything obviously wrong since the `Bulbasaur` struct was declared public. It didn't make any sense why I wasn't able to create a `Bulbasaur` instance using the default memberwise initializer. Which means an initializer created by the language behind the scenes for each property in the structure. At this point, the struct looked like this:

```
public struct Bulbasaur {

    public let type: String
    
    public let maxHP: Int
}
```

I tried many debugging techniques, like re-creating the struct right above the method I was working in, which did compile, but would cause other issues in the framework because it was a completly different struct. I edited the access control modifiers in the struct to make different combinations, then I made the struct a class, but none of these attempts were successful.

## The Solution

Alas, I went home for the day and began work the next day with a clear mind. As you might expect, I figured out the issue within 30 minutes, making my problem seem silly, as hindsight will make you think. While I'm sure this is an issue many have run into, I found it suprisingly undocumented until I found this one <a href="http://stackoverflow.com/a/26224873/2280737" target="_blank">StackOverlow post answer</a>. Once I read the following, all became clear:

> As with the default initializer above, if you want a public structure type to be initializable with a memberwise initializer when used in another module, you must provide a public memberwise initializer yourself as part of the type’s definition.

Sure enough, this was taken directly from <a href="https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AccessControl.html" target="_blank">Apple's documentation</a> in the section about default memberwise initializers. **Although my struct was public and my properties were public, the code using the struct was in a different module, causing the default initializer to be internally protected by default.** With this in mind, I made the appropriate addition:

```
public struct Bulbasaur {

    public let type: String
    
    public let maxHP: Int
    
    public init(type: String, maxHP: Int) {
        self.type = type
        self.maxHP = maxHP
    }
}
```

Of course, that resolved all my issues. Simply adding an initializer that seemed unnecessary allowed me to create my own instance of `Bulbasaur` with ease. While this issue was a headache, it is helping me learn the importance of documentation and knowing the intricacies of a language. This can be difficult with all the changes to Swift, including <a href="https://github.com/apple/swift-evolution/blob/master/proposals/0018-flexible-memberwise-initialization.md" target="_blank">proposals</a> about improving default memberwise initializers. Regardless, you know better, I know better, now onto the next issue 😫