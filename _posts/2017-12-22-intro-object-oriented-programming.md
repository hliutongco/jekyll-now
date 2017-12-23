---
layout: post
title: Super simple intro to object oriented programming
excerpt_separator: <!--more-->
---

So let's say that you've decided to flex your programming abilities by making a series of simple games. Let's also say that you decided to make these games using Ruby, because why not?

You start by creating a couple methods for your games:

```
def tictactoe
  #Insert code for tic tac toe game
end

def hangman
  #Insert code for hangman game
end

def guess_the_number
  #Insert code for guess the number game
end
```

As you begin to write your code, you realize that your #tictactoe, #hangman, and #guess_the_number methods are becoming very unwieldy very quick. Not only do you need to build several separate methods within each method, but you also realize that your three games share a lot of similar code. If only there were a good way to organize these methods, and to standardize the bits of code that are used across all three games.

This is precisely where **classes** come in handy. Classes allow for a more elegant way of structuring our code, in large part due to some built-in functionality specific to classes. For instance, classes can inherit code from other classes.

<!--more-->

### »sharing (code) is caring

Since all three of your games share certain bits of code, we can create a separate class that houses those bits of code. We can then have our games inherit code from that newly-created class. In Ruby, it might look something like this:

```
class Games
  #Insert code that all games share
end

class TicTacToe < Games
  #Insert code specific to tic tac toe
end

class Hangman < Games
  #Insert code specific to hangman
end

class GuessTheNumber < Games
  #Insert code specific to guess the number
end
```

A couple things to note:
* You've probably noticed that after each game class, I've put "< Games". This is the syntax to inherit code from another class. So in the above code, the tic tac toe, hangman, and guess the number games are all inheriting code from the Games class.
* You might have also noticed that the class names are all capitalized. Using capital letters is standard for classes in Ruby.

### »classes as object creators

One other major, major difference between classes versus regular methods is that classes have the power to **create objects**. In the context of the game classes in the above examples, it is sort of like creating a new instance of each game every time we run the code. If we were to call on a method in the TicTacToe class, for example, we would first create a new instance of a tic tac toe game:

```
class TicTacToe < Games
  
  def play_tictactoe
    #Insert code for playing tic tac toe
  end
  
  #Insert other code specific to tic tac toe
end

#Here we are creating a new tic tac toe game object
ttt_game = TicTacToe.new

#Here we are using the new object to call upon the method that will start the game
ttt_game.play_tictactoe
```

Additional clarification: "TicTacToe.new" is the Ruby syntax for creating a new object using a class. In the example, I assigned "TicTacToe.new" to the variable "ttt_game". I then used that variable to call upon a method within the TicTacToe class.

Note that calling the "play_tictactoe" method directly on the TicTacToe class will result in an error. This is because a class is an **object creator** rather than an object itself. You need to create an object (in this case, a tic tac toe game) first in order to call a method upon that object.

### »additional resources
* [bastards book of ruby](http://ruby.bastardsbook.com/chapters/oops/) » a more thorough explanation
* [launch school lesson](https://launchschool.com/books/oo_ruby/read/inheritance) » this goes super in-depth into the topic of class inheritance
