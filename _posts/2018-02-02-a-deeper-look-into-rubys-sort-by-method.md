---
layout: post
title: A deeper look into Ruby's .sort_by method
excerpt_separator: <!--more-->
---

I was recently given a coding challenge that involved overriding Ruby's default sorting behavior. It asked to sort an array of strings using the esperanto alphabet:

```
ESPERANTO_ALPHABET = "abcĉdefgĝhĥijĵklmnoprsŝtuŭvz"
```

Ruby's default sorting behavior places any accented characters at the end of the array. So for example:

```
array = ["abc","ĉde","fgĝ"]
array.sort -> ["abc","fgĝ","ĉde"]
```

I struggled with this for way, way longer than I should have, and it was all because I didn't *really* understand how Ruby's .sort and .sort_by methods actually worked.

<!--more-->

### ».sort or .sort_by?

So in terms of regular usage, the main difference between these two methods is:

* .sort accepts two arguments, which represent a pair of items in your array; in this case, the sort is determined based on how those two arguments compare to one another
* .sort_by accepts one argument, which represents each individual item in your array, and a block dictating how each item in your array should be sorted

Let's break this down a little. The default sort method in Ruby can be expressed as the following:

```
array = ["abc","def","ghi"]
array.sort { |a, b| a <=> b }
```

The spaceship operator (<=>) basically dictates that the order should remain unchanged if the two items are equal, but that item 'a' should be placed before 'b' when item 'a' is larger. Likewise, item 'b' should be placed after 'a' whenever 'b' is smaller.

If you wanted to sort in reverse order, you would simply need to write:

```
array = ["abc","def","ghi"]
array.sort { |a, b| b <=> a } -> ["ghi","def","abc"]
```

In comparison, the .sort_by method is a little more abstract, since the sort is not determined based on how the items of the array compare to one another. To mimic the default sort behavior, you would simply need to write:

```
array = ["abc","def","ghi"]
array.sort_by { |item| item }
```

### »so how do we sort using the esperanto alphabet?

Firstly, the .sort method is probably not the best option to solve this conundrum, since we want to change the sort behavior using a completely different alphabet. This is different from simply comparing the array items to one another, since Ruby does not naturally recognize that the letter "ĉ" should come before the letter "f".

But how do we solve this using .sort_by? What code should we put into the block? How do we get .sort_by to recognize that "ĉ" should come before "f"? Let's write the very beginnings of this code.

```
ESPERANTO_ALPHABET = "abcĉdefgĝhĥijĵklmnoprsŝtuŭvz"
array = ["abc","ĉde","fgĝ"]

array.sort_by { |item| /* code */ }
```

One of my initial thoughts was to use the index numbers of the letters in the ESPERANTO_ALPHABET variable. In this case, you would need to break each string in the array down to its individual letters. You would then compare each letter to the contents of the ESPERANTO_ALPHABET string, and receive an index number in return.

(As a side note, I thought this meant that .sort_by would alphabetize and rearrange the letters of each item in the array, which was a completely wrong assumption, and one that led me on a wild goose chase for a long, long time. Learn from my mistakes, friends!)

If we were to use [Ruby's split method](https://apidock.com/ruby/String/split) to break down the letters of the array items and [Ruby's .map method](https://apidock.com/ruby/Enumerable/map) to map each letter to the ESPERANTO_ALPHABET, our code would look something like this:

```
array.sort_by { |item| item.split("").map{ |letter| ESPERANTO_ALPHABET.index(letter) } }
```

To reiterate, the above code is:

1. splitting each string in the array
2. finding each letter within the ESPERANTO_ALPHABET string
3. looking up the index number of each letter

To provide a better visual for what this code is doing, let's write out the index numbers of each array item:

```
ESPERANTO_ALPHABET = "abcĉdefgĝhĥijĵklmnoprsŝtuŭvz"
array = ["abc","ĉde","fgĝ"]

array.sort_by { |item| item.split("").map{ |letter| ESPERANTO_ALPHABET.index(letter) } }

// This is now the criteria that .sort_by is using to sort the array:
// [012, 345, 678]
-> ["abc","ĉde","fgĝ"]
```

Using the index numbers as a sort criteria allows .sort_by to finally recognize that "ĉ" should come before "f". And with that, we are finally done!

### »additional resources

* [stack overflow question](https://stackoverflow.com/questions/7249775/what-is-going-on-in-rubys-sort-method) » goes more in-depth into the .sort method
* [api dock documentation](https://apidock.com/ruby/Enumerable/sort_by) » more info on .sort_by
