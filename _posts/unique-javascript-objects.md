Fun fact: [Javascript does weird stuff](https://www.destroyallsoftware.com/talks/wat) sometimes. For a quick example, try typing:

`{} === {}`

...into your console. An empty object is equal to an empty object, so clearly the return value will be true. Right?

Well, not exactly. Unless you say otherwise, Javascript will treat every object as a unique individual with its own unique identity. To us, the two empty objects look exactly the same, but the computer interprets them as two completely different objects.

<!--more-->

