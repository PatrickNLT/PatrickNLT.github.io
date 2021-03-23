+++
date = "2017-07-14T08:28:48+01:00"
title = "Options for cross-platform iOS/Android development in 2017"

+++

Cross-platform mobile development is a topic that has been widely discussed since the first years of Android and iOS. The promise is enticing: write once, run everywhere. Don't do the same work twice. Who wouldn't want that? Unfortunately, this is not as easy to achieve as it seems: you need to find the right language, the right tools, the right scope (do you want to share the UI code?) in order to be as productive as possible while taking advantage of the strengths of each platform.

<img class="full-column" alt="Cross-platform" src="/catalog/header.png">

At my new work, we recently had to write a new app from scratch. It was the perfect opportunity to evaluate the options that are available today in that area. Like for many things, the journey was more important than the destination: the final decision was specific to our company needs and constraints, but it made us ask ourselves the right questions and find balanced answers. I thought that sharing some key points with the community may help other developers form their own opinion. In this post, I will list some options that we considered while doing our research.

# All-in-one solutions

The promise of all-in-one frameworks is to let you write an entire app using a single language and paradigm. These tools also allow you to build the UI using either their own layout system or HTML and CSS.

## Xamarin

<img alt="Xamarin" src="/catalog/xamarin.svg" height=150>

[Xamarin](https://www.xamarin.com) is a framework that helps you write Android and iOS apps in C#. Apps run in a virtual machine thanks to the Mono runtime. Also, you can build the UI using `Xamarin.Forms`, so you can have very little platform-specific code. Sadly, there are surprinsingly few mobile developers out there willing to write C# code, maybe because it is historically tied to the Windows platform (and for a long time, Xamarin's IDE has been available only on Windows). It is a nice and mature language, though, with advanced features like asynchronous programming built directly into it.

## Apache Cordova

<img alt="Cordova" src="/catalog/cordova.png" height=150>

[Cordova](https://cordova.apache.org) (and its derivatives [PhoneGap](http://phonegap.com) and [Ionic](https://ionicframework.com)) is an open-source JavaScript framework whose approach is to let you write web apps wrapped up in a shell with access to the native API. It is targeted mainly at web developers, and suffers from the well-known limitations of web-based apps: bad performance and non-native UI.

## Titanium

<img alt="Titanium" src="/catalog/titanium.png" height=150>

[Titanium](https://www.appcelerator.com/mobile-app-development-products/) is another JavaScript framework. This time, the UI can be composed of native elements, which will make your app look better than an web app, while still writing all the code in JavaScript.

## React Native

<img alt="React Native" src="/catalog/react_native.svg" height=150>

[React Native](https://facebook.github.io/react-native/) is the latest addition to the family of JavaScript frameworks. It builts on the success of [React](https://facebook.github.io/react/) on the web and applies the same paradigm based on declarative components to create native apps. It is a well-designed library, and it is already used in production in several major apps such as Facebook, Instagram, or [Artsy](http://artsy.github.io/blog/2016/08/15/React-Native-at-Artsy/). There are currently some drawbacks such as the lack of a good threading model, and you will probably need some people in the team with good Java/Objective-C/Swift knowledge if you're doing advanced things.

## SCADE

<img alt="SCADE" src="/catalog/scade.png" height=100>

[SCADE](http://www.scade.io) is like Xamarin for Swift. As for now, it is still in beta, and requires at least Android 6.0, but it is exciting for iOS developers to be able to write cross-platform apps using their favorite language, so it is definitely a project worth following.

# Languages with bindings of native UI frameworks

If all-in-one frameworks are not your cup of tea, you may be happier with toolchains that expose the iOS and Android APIs to another common language. You will still write the UI code using view controllers on iOS and fragments on Android, so you will need to learn how each platform works, but business logic will be very easy to share. Compared to the business-logic-focused solutions listed below, the big advantage is that the whole code base is written in a single language, thus there is no need to communicate between multiple heterogeneous code bases.

## RubyMotion

<img alt="RubyMotion" src="/catalog/rubymotion.png" height=150>

If you love Ruby, [RubyMotion](http://www.rubymotion.com) may look very tempting to you. It statically compiles Ruby to machine language using LLVM, so no actual Ruby code is bundled into the released app. And the code is called through the Objective-C runtime on iOS and through the JNI (Java Native Interface) on Android.

## Multi-OS Engine

<img alt="Multi-OS Engine" src="/catalog/multios_engine.png" height=150>

[Multi-OS Engine](https://multi-os-engine.org) is Intel's take on cross-platform development (still in preview). It is an interesting way for Android developers to develop for iOS, since it supports both Java and Kotlin. Android apps are written like pure Android apps, and iOS apps are written using Java bindings of UIKit and other Objective-C and C libraries. At runtime, the iOS apps start their own version of the ART (Android Runtime) VM and execute compiled Java/Kotlin code.

# Cross-platform languages

Instead of relying on a big single framework to write your whole app, you may want to share only the business logic of your app and write the other parts (mostly UI) in platform-specific native code. This approach helps take the specificities of each platform into account and provide a native look and feel to the user.

## C/C++

C/C++ is often the first thing that comes to mind when looking for an efficient way to share code between iOS and Android: it is straightforward to integrate C code in an Objective-C code base (Objective-C is a superset of C), and the Objective-C compiler also supports mixing C++ and Objective-C code in the same _Objective-C++_ source file. On the Android side, Java supports calling C/C++ code (known as _native_ code) from Java and Java code from C/C++ through the JNI.

There are some drawbacks, though. First, C and C++ are not very popular among mobile developers which are often used to higher-level and safer languages that make memory management easier. Therefore you may have some difficulties finding good C/C++ developers who are also experts in mobile applications. Second, the JNI introduces a performance hit that you must be aware of, especially if you are considering accessing a lot of fields and methods through this interface. Third, maintaining the source files for the interface between C/C++ and Java can be a little tedious. Fortunately, Dropbox released [Djinni](https://github.com/dropbox/djinni), a tool for generating type declarations and interface bindings from an interface description file. If you are considering C/C++ for your project, Djinni is definitely worth checking out.
 
## J2ObjC

<img alt="J2ObjC" src="/catalog/j2objc.png" height=150>

If you know Java well, you may be interested in [J2ObjC](https://developers.google.com/j2objc/), a Java to Objective-C translator that was developed by Google and is used internally in some of their apps such as Inbox or Google Calendar. It transpiles Java code to Objective-C and provides a compliant Java runtime environment (based on Android libcore) to Objective-C. That way, all your business logic code, including your dependencies (think Retrofit, etc…), will be converted to Objective-C and will run natively on iOS.

One major drawback is that J2ObjC is a rather small project run by only a few people, with still a [few holes](https://github.com/google/j2objc/issues/679) in the implementation, and [tools](https://github.com/j2objc-contrib/j2objc-gradle) in need of new maintainers. So you must think twice before your whole code base relies on it.
 
## Go Mobile

<img alt="Go Mobile" src="/catalog/go.png" height=150>

Go is a language that is very popular among backend developers. They like how pragmatic it is, focusing more on developer productivity than on being the smartest language out there. Plus, it has nice features like built-in support for concurrent programming. And, you guessed it, it can be used on mobile platforms as well.

[Go Mobile](https://github.com/golang/mobile/) is an official but still experimental project that aims at making the interoperability of Go with Java and Objective-C easier. It provides a tool, `gobind`, that automatically generates bindings between those languages. 

Go Mobile has some limitations: at the moment, only a subset of Go types are supported. Also, as Go manages its memory in its own garbage-collected environment, passing pointers to another language must be cautiously done to prevent the destruction of objects that are still used in the other environment. There are [some solutions](https://godoc.org/golang.org/x/mobile/cmd/gobind#hdr-Avoid_reference_cycles) to this, but there are quite cumbersome.

## The case of Swift and Kotlin

<img alt="Swift" src="/catalog/swift.png" height=150>
<img alt="Kotlin" src="/catalog/kotlin.png" height=150>

[Swift](https://swift.org) and [Kotlin](https://kotlinlang.org) have a lot in common. They are both official languages for a mobile platform, respectively iOS and Android. They are both concise, expressive, statically typed languages, they provide type inference, and their syntax is [sometimes very similar](http://nilhcem.com/swift-is-like-kotlin/). Their design also lean towards functional programming by encouraging you to use immutable data and by making functions first-class citizens of the language.

Swift and Kotlin may look like ideal candidates for a cross-platform iOS/Android language. Indeed, Swift was [ported](https://github.com/apple/swift/blob/master/docs/Android.md) to Android, and Kotlin has [Kotlin/Native](https://github.com/JetBrains/kotlin-native), a way to natively (i.e. without the help of the JVM) run Kotlin code. Unfortunately neither of them is ready for production yet:

* Android support for Swift is very rough. The toolchain only runs on Linux, there is no easy way for Swift-to-Java bridging, and the minimum supported API level is 21 (Android 5.0), which excludes more than 25% of Android devices. Also, it looks like there is very little work done to improve those issues.
* Kotlin/Native, on the other hand, is under active development and iOS will be officially supported in the future. However, it is still in preview, and some important bricks are lacking, from variable inspection during debugging to a finalized memory management scheme (it currently uses reference counting with a cycle collection algorithm).

# So, which one should I choose?

As you can see, there are many frameworks and languages that let you write cross-platform code, and most of them are mature and viable options. At the end of the day, it really comes down to two questions:

* Do you think that in your case the benefits of cross-platform development will compensate for the inevitable overhead of introducing a third framework or language into the mix? If you have little business logic to share and mostly have UI code in your app, it is sometimes simpler and safer in the long term to just have two separate projects, one for each platform.
* What will your team be the most efficient at? If you already have iOS and Android experts in your team, you probably don't want to pick an all-in-one solution such as Xamarin that basically requires to learn everything from scratch again. On the other side, if your team has some JavaScript developers in it, React Native may be a very good choice for you.

The decision is yours.