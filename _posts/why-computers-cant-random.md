title: Why Computers Can't Random

I was explaining Javascript's Math.random() function to a friend when he suddenly asked me, "How do computers come up with random numbers?"

I paused. This was a question that I hadn't actually considered. How *do* computers come up with random numbers? After offering a couple lame theories that made no sense, I admitted I was stumped. And it was my friend who thought up the most plausible theory: maybe the computer just memorizes a huge list of numbers?

Which isn't exactly what the computer's doing, but it does get at the core of what's going on: most computer-generated random numbers you'll come across, including the ones you see in the Math.random() function, are in fact *pseudo*-random numbers. Or in other words, they're not random at all.

<!--more-->

## that's right, Math.random() is a lie

Basically, Math.random() and other similar functions are more like random number simulators. They start with a base number and then use [a fancy algorithm](https://en.wikipedia.org/wiki/Linear_congruential_generator) to create a sequence of numbers that appear random.

This sequence isn't *truly* random because it is, essentially, a long-running pattern. Eventually, the sequence of numbers will end and loop back to the beginning. That said, pseudo-random numbers are so good at imitating the real thing that most people would never even notice the pattern. So why does this even matter?

Well, it matters in cases where you really, really don't want the numbers to be predictable in any way. For instance, if your website allows users to gamble on online games using real money, then you'd better make sure that the results of your games are truly random. Otherwise, users might realize the pattern and abuse it.

So what do you do when you're in need of truly random numbers?

## real random numbers come from real life

There are ways for computers to collect random numbers, all of which involve measuring random real-life phenomena. 