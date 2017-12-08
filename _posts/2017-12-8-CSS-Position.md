---
layout: post
title: How to use absolute & relative positioning to put things in weird places
excerpt_separator: <!--more-->
---

So this blog layout took a while for me to design, quite a bit longer than I had anticipated. I looked at CSS and thought "pfft, I can handle this guy", but then CSS turned around and proceeded to kick my butt for hours. And since *Code Meets Girl* is all about explaining the stuff I've struggled with, why not start with the creation of the very page you're reading now? Or to be more specific, one particular element on this page.

See that dancing robot in the top corner? That's an animated gif. The speech bubble is actually a separate image that was positioned adjacent to it. So how did that funny little robot get there? I first tried using:

.site-avatar {
 float: right;
}

...to float the robot to the right side of the title. But that left the robot hovering awkwardly beneath the site navigation, and worse, it pushed the title further to the left so that it was off-center.

This led me to the https://developer.mozilla.org/en-US/docs/Web/CSS/position CSS position property, which would allow me to specify the exact location of the gif. The position property comes in a few different flavors, the most popular ones being **absolute** versus **relative**.

<!--more-->

How do you know whether to use absolute or relative positioning? You can start by asking a couple questions:

Do you want your positioned element to affect the elements surrounding it?

Think back to the earlier example, where I floated the robot to the right of the title. Doing this caused the title to shift to the left, pushing it off-center. In this instance, the title "senses" the presence of the robot and moves away in order to make room for it.



