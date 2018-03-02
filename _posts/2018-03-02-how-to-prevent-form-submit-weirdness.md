---
layout: post
title: How to prevent HTML form submit weirdness
excerpt_separator: <!--more-->
---

If you mess around with HTML forms and event handlers long enough, you might notice something strange. Let's say we create the following form:

```
<form>
    <input type="text" name="inputbox" value="Type text here">
    <br/><br/>
    <input type="submit" id="button" value="Submit">
</form>
```
<!--more-->

Let's also say that in our Javascript code, we create a simple event handler:

```
const submitButton = document.querySelector('.button');

submitButton.addEventListener('submit', function () {
    console.log('The form was submitted');
});
```

When you open your wepbage and click the submit button, you notice something strange. The event handler is supposed to log the string "The form was submitted" to the console whenever we click the submit button. But when we submit the form, the console appears to log the text for a split second before the console suddenly clears and the text disappears. What's going on here?

It turns out that whenever we submit a form, the form's default behavior causes the page to refresh. Whenever an event handler is listening to the form submit event, this default behavior essentially prevents these event handlers from functioning as intended. So how do we fix this mess?

### »the one line of Javascript that solves everything

Luckily, in order to get the event handler working, all you need to do is add a single line of code to your Javascript file:

```
const submitButton = document.querySelector('.button');

submitButton.addEventListener('submit', function (event) {
    event.preventDefault();
    console.log('The form was submitted');
});
```

In Javascript, event objects have a built-in method that prevents the event's default behavior from occurring. In this case, the default behavior is refreshing the page upon form submit.

Let's break this code down a little. We passed an argument called 'event' into the function inside of the event handler. This argument contains information about the form submit event and gives us access to the .preventDefault() method.

Inside of the function, all we need to do is call the .preventDefault() method on the event argument. Now, the event handler will work as intended and the function will successfully log the text to the console.

### »additional resources

* [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault) » more info on the event.preventDefault() method
* [javascript.info page](https://javascript.info/default-browser-action) » info on browser default actions
