---
layout: post
title: How to use absolute & relative positioning to put things in weird places
excerpt_separator: <!--more-->
---

So this blog layout took a while for me to design, quite a bit longer than I had anticipated. I looked at CSS and thought "pfft, I can handle this guy", but then CSS chugged a protein shake and proceeded to kick my butt for hours. And since *Code Meets Girl* is all about explaining the stuff I've struggled with, why not start with the creation of the very page you're reading now? Or to be more specific, one particular element on this page.

### »say hi to BMO, the blog mascot

See that dancing robot in the top corner? That's an animated gif. The speech bubble is actually a separate image that was positioned adjacent to it. So how did that funny little robot get there? I first tried using:

```
.site-avatar {
    float: right;
  }
```

...to float the robot to the right side of the title. But that left the robot hovering awkwardly beneath the site navigation, and worse, it pushed the title further to the left so that it was off-center.

This led me to the [CSS position property](https://developer.mozilla.org/en-US/docs/Web/CSS/position), which would allow me to specify the exact location of the gif. The position property comes in a few different flavors, the most popular ones being **absolute** versus **relative**.

<!--more-->
### »the difference between absolute vs relative positioning

How do you know whether to use absolute or relative? You can start by asking a couple questions:

* Do you want your positioned element to affect the elements surrounding it?

Think back to the earlier example, where I floated the robot to the right of the title. Doing this caused the title to shift to the left, pushing it off-center. In this instance, the title "senses" the presence of the robot and moves away in order to make room for it.

* Do you want for a certain amount of space to be reserved specifically for your positioned element?

Similar to the previous point, you want to consider whether you need to create blank space for your positioned element and whether you want the surrounding elements to make room for it.

In regards to my dancing robot, the answer to both questions is **no**. I don't want to push the title off-center; I want the title to treat the robot as if it's not really there. Likewise, I don't need to create extra space for the robot because there's already plenty of blank space in the header.

### »using position: absolute

This is the code I ended up using:

    .site-avatar {
        position: absolute;
        top: 115px; right: 10px;
        width: 60px;
        height: 60px;
      }

Elements with absolute positioning are kind of like ghosts. They're technically there and *we* can see them, but the other elements act like it doesn't exist.

By default, the robot ended up in the top right corner of the page, overlapping the navigation links. In order to get the robot to its own little spot, I essentially added 115px of padding above it and 10px of padding to the right.

Since the speech bubble is a separate image, I also had to use absolute positioning in order to put it right beside the robot:

    .avatar-speech {
        position: absolute;
        top: 75px; right: 60px;
        width: 50px;
        height: 50px;
      }

### »using position: relative

Let's shift our attention away from the robot and instead focus on the "{ }" braces before and after the site title. By default, the braces were placed a little lower than the title text. I wanted to bump the braces up so that they were perfectly aligned with the text.

In this case, I didn't really want to use absolute positioning. After all, I only wanted to move the braces a few pixels up from their original position. This is the code I ended up using:

    .site-name:before {
        content: "{";
        position: relative;
        top: -10px;
      }
 
    .site-name:after {
        content: "}";
        position: relative;
        top: -10px;
      }
  
Because I'm using relative positioning, the braces are not placed in the top right corner of the page. Instead, the braces maintained their original position by default. In order to bump the braces up, I only had to remove 10px of padding from the top of each brace.

### »additional resources

This post contains a super basic and non-technical explanation of the position property. Check out the below links if you want to learn more:

* [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/position) » this one has a helpful demo

* [CSS-tricks page](https://css-tricks.com/almanac/properties/p/position/) » this one has gifs

* [A List Apart article](https://alistapart.com/article/css-positioning-101) » this one is super thorough
