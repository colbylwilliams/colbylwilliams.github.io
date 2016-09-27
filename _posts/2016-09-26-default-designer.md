---
layout: post
title:  "Default Desinger"
date:   2016-09-26 18:00:00 -0400
tags: xamarin xamarin-studio
excerpt: I prefer to work with <code>.xibs</code> and <code>.storyboards</code> in Xcode Interface Builder opposed to Xamarin Studio’s built-in designer.  Default Designer is a Xamarin Studio add-in to open these files with Xcode Interface Builder by default.
---

I've been developing native iOS, macOS and Android with Xamarin for years now.  I love C# and Xamarin Studio is an incredible IDE.

However, I prefer to work with `.xibs` and `.storyboards` in Xcode Interface Builder opposed to Xamarin Studio’s built-in designer.

Within Xamarin Studio you can open these files in Xcode easily using the “Open with…” action menu, but I wanted it to use Xcode by default.

Yesterday I wrote a [simple add-in][1] for Xamarin Studio that sets Xcode Interface Builder as the default designer for `.xib` and `.storyboard` files.

You can check out the [source][1] or just follow these steps to install the add-in and use in Xamarin Studio:

1. Download the `.mpack` file of the [latest release][0]
2. Launch Xamarin Studio, open the **Xamarin Studio** menu and select **Add-ins...**
3. In the bottom left of the _Add-in Manager_ dialog, click **Install from file...**
4. Choose the `.mpack` file you downloaded in step 1.
5. When prompted, select **Install**

With the add-in installed, double-clicking `.xib` and `.storyboard` files will open them in Xcode Interface Builder.  Xamarin Studio’s designer can still be used via the “Open with…” action menu.


[0]:https://github.com/colbylwilliams/DefaultDesigner/releases/latest
[1]:https://github.com/colbylwilliams/DefaultDesigner
