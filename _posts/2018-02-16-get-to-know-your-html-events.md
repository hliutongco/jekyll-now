---
layout: post
title: Get to know your HTML events using console.log()
excerpt_separator: <!--more-->
---

Quick tip of the week: when dealing with HTML events, **use console.log() to inspect the event** before doing anything with it. This is probably a habit that should come naturally, but it's one that I sorely neglected for far too long.

Take the case of the following HTML table:

![10 x 10 HTML table grid](https://hliutongco.github.io/images/html-event-grid.png "HTML table javascript event")
<!--more-->

I added a Javascript event listener to this table so that I could keep track of clicks onto the table. The goal was to change the background color of any given table cell when that table cell was clicked. I would do this using a function called colorCell().

```
function colorCell(event) {
    //code for changing the background colpr of the cell
}

table.addEventListener('click', colorCell);
```

But how do you pinpoint the exact cell that was clicked? You could assign an id to each and every table cell, but that's waaaay too tedious and inefficient. It would be much better if you could somehow pinpoint the clicked table cell using the HTML click event.

### »using console.log(event) to find the cell

If you console.log(event), upon clicking the table, you will see a very long and very intimidating object. There is tons of data here, but upon scrolling, you'll eventually see a key called 'path'. If you click and expand 'path', you'll see that the first option is called '0: td'. This is a reference to the clicked cell itself; if you hover over 'td', the DOM will display the table cell you clicked on.

![the developer console and the clicked table cell](https://hliutongco.github.io/images/html-event-console-log.png "developer console HTML event")

If you click and expand '0: td', you'll see that it has access to the style attribute, and beyond that, the backgroundColor property. You can use this to change the background color of the clicked cell. Thus the code for the colorCell() function is as follows.

```
function colorCell(event) {
    //in the below code, we're changing the background color to black
    event.path[0].style.backgroundColor = #000000;
}

table.addEventListener('click', colorCell);
```

Let's break this down:

* event.path[0] refers to the clicked cell (a.k.a. 'td') itself
* .style.backgroundColor is how we access the background color of the cell
* #000000 is the hex code of the new background color

We found all this out by using console.log() on the HTML click event and digging around until we found something that fit.

### »additional resources

* [w3schools HTML events page](https://www.w3schools.com/jsref/dom_obj_event.asp) » a quick list of common HTML events
