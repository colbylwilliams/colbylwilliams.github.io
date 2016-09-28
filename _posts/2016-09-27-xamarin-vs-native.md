---
layout:  post
title:   "Xamarin vs. Native"
tags:    xamarin ios android
excerpt: I spend a lot of my time talking to people about mobile development.  Many of these conversations are about Xamarin, and how it compares to "native", so I figured I’d take the time to break down Xamarin.  I’ll also spend a little time on alternative approaches to mobile development — just to add some context.
---


I spend a lot of my time talking to people about mobile development.  Many of these conversations are about Xamarin, and how it compares to "native", so I figured I’d take the time to break down Xamarin.  I’ll also spend a little time on alternative approaches to mobile development — just to add some context.  Here’s the short version:

_**Mobile applications written in C# using Xamarin are native — just as native as iOS apps written in Swift or Objective-C, and Android apps written in Java.**_

If you’re intrigued (or disagree), read on.  If you did read on, and you still disagree, email me.  We’ll get to the bottom of this ;)


## Approaches to Writing Mobile Apps

Okay, let’s break it down.  When you, your company, your wife - whatever, decide to build a mobile app, you’ve got a few options.  And like most things in life, each choice, or approach, is going to have pros and cons.

Since we’re comparing Xamarin to "native", let’s start out with the approach that undoubtedly yields a 100% native app.  I tend to call this approach Indigenous Native, or simply writing the native app with the “indigenous” language and toolset.  An example of this approach would be writing an iOS app in Swift using Xcode.

### Indigenous Native

This approach is going to yield a fully native app that performs and responds the way the user expects it to.  Perfect.

However, the approach is also going to yield a unique codebase for each platform the app will support.  If the app is written for iOS and Android, the iOS version must be written in Swift or Objective-C using Xcode, then the Android version must be written from scratch in Java using Android Studio or Eclipse, leaving you with two separate codebases, and likely two separate teams writing and maintaining them.

Kind of sounds terrible.  But a truly native application is so important to a mobile app’s success — both consumer apps and business apps — that people and companies commonly write and maintain two completely separate codebases for the same app on iOS and Android.

That’s why the "short version" simply states that Xamarin is native.  That's the most important part.

### Xamarin

Xamarin is the only other approach to building mobile apps that yields a fully native app and does so without limiting the developer to a subset of the native SDKs.  To understand how that's possible, let’s break down what Xamarin is and a little bit of how it works.

Xamarin is essentially made up of two parts — the first of which is a collection of one-to-one bindings for the entire iOS, Mac, and Android SDKs.  What does that mean?

#### One-to-One Bindings

Well Xamarin didn’t reverse-engineer all the frameworks and libraries you’d use to write native iOS and Android apps.  Instead, they simply _exposed_ those APIs to C#.  When you call an iOS or Android API in your Xamarin app in C#, you’re calling the exact same API of the exact same framework or library you would call using the “indigenous” languages.

So with just this “first part” of Xamarin, you now have access to everything you would if you were writing your app in Objective-C, Swift, or Java.  _**Anything that can be done in an iOS application using Objective-C or Swift, and anything that can be done in an Android app using Java, can be done in C# using Xamarin.**_  There is no exception.

These one-to-one bindings cover 100% of the public APIs Apple and Google have exposed to developers to write iOS and Android apps respectively.

To put this in context, you could literally take an iOS app written in Swift, or a Android app written in Java, and rewrite it line-for-line — using all of the same objects, methods, properties, etc. — in C# with Xamarin and end up with the same app with the same UI, the same performance, the same… well, you get it.

Those of you that’ve been paying attention may have just realized that Xamarin doesn’t sound all that cross-platform at all.  If you’re just calling the same APIs in a different language, you’re not going to share any code…?

You’re right.  The way I see it, Xamarin is not really a “cross-platform solution”, but there is a cross-platform "component" to Xamarin — and that’s the second part — Mono.

#### Mono

Mono is an implementation of the .NET base class libraries that’ll run natively inside of your Xamarin app.

There’s plenty of information out there on Mono — if you want to find out more, I’d encourage you to Google it — but in the context of Xamarin, Mono means you can write portable .NET code in C# (or F#) and share it across your native iOS, Mac, Android, Windows apps.

Anything you can do using the .NET base class libraries — or with any third-party portable .NET library — you write once and share that code and functionality across a iOS, Mac, Android, and Windows.  A couple of common examples of this are the service layer and data access layers of your application.

The title of this post is Xamarin vs. Native, so I'm not going to spend as much time on the remaining approaches.

I’m going to lump everything else into two remaining buckets: Hybrid and Web.  There are several solutions out there that create a pretty big spectrum, but I’ll be talking about these two categories at such a high level, it won’t really matter.

### Hybrid

First let’s talk Hybrid.  Usually these solutions are truly “write-once-run-everywhere” and frequently written in a familiar language like JavaScript.

The two biggest benefits to using a hybrid solution are 1) the time it takes to produce a functional app and 2) the ability to use existing skills (JavaScript).

Additionally, some Hybrid solutions can compile to a native or near-native app.  And depending where on the spectrum the solution sits, this is going to mean much better performance than a webpage disguised as an app (see below).

But I want to clarify what I mean when I say “compile to a native or near-native app” because the word "native" gets thrown around a lot.

"Native binary" does not necessarily mean a "native app" in the same sense as the two previous approaches.  If a Hybrid tool exposes 60% of the iOS and Android SDK through its own “write-once-run-everywhere” APIs, it may compile the resulting app to native binary, but the app is still going to look and feel like it was developed using 60% of the SDK.

To put this in context, let’s look at the very specific example: the best way to do animations inside of an iOS application is to use the animation framework that Apple created and distributed to developers to do animations in iOS apps.  Using anything else is either going to yield subpar animations, perform poorly, or simply be an abstraction that is actually using the same animation framework behind the scenes.

Without access to 100% of the APIs in 100% of the frameworks shipped with the iOS SDK, you are going to be limited.  Now, that example was specific to iOS, but the concept is equally true for Android.

Every Hybrid solution is going to have some level of this "least common denominator" type limitation. The only two approaches that expose 100% of the SDKs are Indigenous Native and Xamarin.

### Web

In the context of the blog post, Web refers to everything from responsive or mobile websites, to apps made of wrapped websites.

And on this approach, I’ll very be brief.  There is absolutely a place for responsive or mobile web, but let’s not call it a mobile app.  Why?  Well, let’s be honest, just because the app can open up the camera, it’s still just a webpage.

## The End

Hopefully this short write-up puts Xamarin in perspective for those interested.

I'm obviously a fan of Xamarin, and that's really because I love native iOS and Android development, and I really like C#.


