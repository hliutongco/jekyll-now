---
layout: post
title: Why every Javascript object is a special snowflake
excerpt_separator: <!--more-->
---

Fun fact: [Javascript does weird stuff](https://www.destroyallsoftware.com/talks/wat) sometimes. For a quick example, try typing:

`{} === {}`

...into your console. An empty object is equal to an empty object, so clearly the return value will be true. Right?

Well, not exactly. Unless you say otherwise, Javascript will treat every object as a unique individual with its own unique identity. To us, the two empty objects look exactly the same, but the computer interprets them as two completely different entities.

<!--more-->
![olsen twins as javascript objects](/images/olsen_objects.png)

Every time Javascript encounters a new object, it assigns a space for that object in its memory. Think of it this way: when Javascript meets the first object, Mary-Kate, it gives her a house on 54th street. It then meets Ashley and offers her a house on 55th street.

When it comes time to compare Mary-Kate and Ashley, Javascript looks at their addresses and thinks, "Mary-Kate lives on a completely different street from Ashley. They can't be the same person!" And so it returns as false.

### »now for some math

Just to make things more complicated, go ahead and type the following expression into your console:

`{} + {} === {} + {}`

Based on the above explanation, you probably expect this expression to also return a false value.

Well, not exactly. When you throw arithmetic into the equation, Javascript converts each empty object into a string, and then it simply adds those strings together:

`{} + {} -> '[object Object][object Object]'`

It then compares the two strings, which are identical, and so the expression returns as true.

### »additional resources

* [Watch and Code video](https://watchandcode.com/courses/60264/lectures/938895) » a video lecture from the Practical Javascript course

* [Stack Overflow question](https://stackoverflow.com/questions/41124252/why-is-true) » explanation of what happens when you throw arrays into the mix
