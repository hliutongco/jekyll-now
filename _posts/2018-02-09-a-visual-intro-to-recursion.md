---
layout: post
title: A visual introduction to recursion (and Scala!)
excerpt_separator: <!--more-->
---

In really simplistic terms, recursion is when a function refers to itself. And it can get pretty confusing. Take the case of these crosses:

![image of crosses](images/crosses-recursion.png "crosses made with recursion")

The cross starts as one circle. In each new iteration, four new circles are added: one on top, one on the bottom, and one to the right and left. So one circle becomes five, five becomes nine, and so on. Since each new cross builds off its previous version, we could use recursion to build these crosses.

### »creating a function in Scala

Let's define a function called #cross:

```
def cross(count: Int): Image = {
    //code
}
```

<!--more-->

The (count: Int) parameter is an **int**eger argument that we will pass to #cross.  Image indicates that the result of the function will be an image. The next step is to declare a circle variable:

```
def cross(count: Int): Image = {
    val cross_circle = Image.circle(10)
}
```

Let's break this down: you use val to declare variables in Scala. Image.circle(10) creates an image of a circle with a diameter of 10.

After declaring the cross_circle variable, we will then use the [match expression](https://docs.scala-lang.org/tour/pattern-matching.html), which will run different blocks of code depending on the value of the count parameter.

```
def cross(count: Int): Image = {
    val cross_circle = Image.circle(10)
    
    count match {
    case 0 => cross_circle
    case n => //code using recursion
    }
}
```

In the above code, we have defined two different scenarios:
* when count is equal to 0
* when count is equal to any other number

The code in case 0 will create a single circle. This forms the base of the cross. We can then use recursion to build any other iteration of the cross.

### »now for some recursion wizardry

For each cross we make, we essentially want to do two things:

* Take the previous iteration of the cross
* Add four circles to its outer edges

For the first step, we can access the previous iteration of the cross using the following code:

```
def cross(count: Int): Image = {
    val cross_circle = Image.circle(10)

    count match {
    case 0 => cross_circle
    case n => cross(n-1)
    }
}
```
cross(n-1) will pass the argument n-1, which is a reference to the previous iteration of the cross. For example. if count = 1 then cross(n-1) is equal to cross(1-1), which is equal to cross(0). This will then match case 0 and create an image of a single cross_circle.

At this point, our #cross function is almost done. Whew! But there's still one big hurdle remaining: in case n of the match expression, we still need to add four circles to the outer edges of the cross. After all, in its current state, our #cross function is currently producing only one circle no matter what number we pass to it. So how do we accomplish this?

Firstly, let's use the keywords "beside" and "above" to describe when an element should be beside or above another element. Secondly, we can use the cross_circle variable to add the four circles that we need. Thus our final code looks like:


```
def cross(count: Int): Image = {
    val cross_circle = Image.circle(10)

    count match {
    case 0 => cross_circle
    case n => cross_circle above (cross_circle beside cross(n-1) beside cross_circle) above cross_circle
    }
}
```

Again, cross(n-1) represents the previous iteration of the cross. We then add one circle to the top, one to the bottom, and one to each side. For example, if we were to pass our #cross function an argument of 1, it would essentially work like this:

```
def cross(1): Image = {
val cross_circle = Image.circle(10)

count match {
case 0 => cross_circle
case 1 => cross_circle above (cross_circle beside cross_circle beside cross_circle) above cross_circle
}
```

![image of crosses made with recursion](images/crosses-recursion-short.png "recursion examples")

And that's recursion in a nutshell!

### »additional resources

* [javascript recursion](https://www.thecodingdelight.com/understanding-recursion-javascript/) » a guide to recursion in javascript
* [scala recursion examples](https://alvinalexander.com/scala/scala-recursion-examples-recursive-programming) » a more in-depth explanation for recursion in scala
