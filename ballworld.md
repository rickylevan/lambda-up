---
layout: default
title: BallWorld, a Field Report
---

<h2> Recap </h2>

!! Explain at the top the purpose of this field report, how I'm going to introduce
BallWorld and make some surface-level comparisons with a less philosophizing 
than the previous post. I'll save that for post #3. 

!! To explain what makes Clojure work for a larger, stateful simulation, I need
to first go through some background so we have something in common to talk about. 

!! Honor Code Warning: If you are a Rice CS major who has not yet done BallWorld:
On your honor, do not read this post. Check it out after you finish. 

!! Before you write much more, you should reflect on Clojure notes you've already
written, and you should re-examine the BallWorld source in both Clojure and Java.
Doing this, and outlining what you want to say, will make your narrative better.

In the previous post, we conceived of programming as finding a solution to a 
constrained optimization problem. Our optimizing metrics were the rates of
channelling, comprehending and composing. The goal was to transform
our pure abstraction of the mind into something executable and to encrypt the
original abstraction as little as possible. The tactic for achieving this was 
to think in reverse from the desired boundary behavior. 

Here's the code from last time, in Java:

```java
public int factorial(int n) {
	int out = 1;
	for (int j = 1; j <= n; j++) {
		out = out*j;
	}
	return out;
}
```

and in Clojure:

```clojure
(defn factorial [n] (reduce * (range 1 (inc n))))
```

It's easy to see that the Clojure encoding of the factorial abstraction is
superior to the Java encoding, at least by the metrics above. But a skeptic of
the usefulness of functional programming in the real world would argue that
choosing factorial was a bit of a cheat. The factorial function is pure: a clean
black box turning input to output. It's no surprise that Clojure shines there.
The skeptic would argue: 
Sure, Clojure is useful for simple mathematical abstractions. It's a 
nice toy to write one-liners for the first few
<a href="https://projecteuler.net/">Project Euler</a> problems. But once we 
need to design a large system,
we have no choice but to turn to Object-Oriented Programming (OOP). For large systems,
it is well-established that Java will outshine Clojure.


<h2> BallWorld </h2>

It should be no surprise by now that I disagree! In COMP 310 at Rice
last semester, we built a simulation called BallWorld, a pedagogical 
project designed to teach principles of OOP. I wanted to see if I could 
use Clojure to design a more optimal solution (by the CCC metrics) to the
BallWorld problem. Credit goes to 
<a href="http://www.bandgap.cs.rice.edu/personal/adrice_swong/public/default.aspx">
Dr. Wong</a> for designing the original project and 
guiding us through an implementation in Java. 

So what's BallWorld? Here's a screencap of a single frame, from my Clojure rewrite: 

<img style = "width: 450px;" alt="room selfie" src="/lambda-up/assets/ball_world.png"></img>

You can run it for yourself right away if you have 
<a href="http://leiningen.org/">Leiningen</a> installed. Simply clone the repository 
(link <a href="https://github.com/rickylevan/ballworld">here</a>),
navigate to that directory, then enter "lein deps", then "lein run". Since Clojure
runs on the Java Virtual Machine, BallWorld should work on your own
machine without any hassle.

In any case, the basic idea is that the balls bounce off the walls,
and they also bounce off each other if the simulation is in collide mode (which is
toggled on and off by the corresponding button). We can add new balls, clear all the balls,
and also add silly behaviors to the balls such as curving and flashing colors. The 
colliding, curving and color flashing can all be toggled on and off, and the special
behaviors stack. For example, we can have the balls be in collide mode while simultaneously
curving and color flashing. This functionality, in the Clojure version, is a
subset of the functionality that the class implemented 
in Java for COMP 310, but it captures the essential features of the Java version. 


Now, it is true that BallWorld isn't a "large system" in the real sense. It isn't 
air traffic control software or the backend for Amazon. But it does have more
sophisticated boundary behavior than the factorial function.
We can send input stimulus to the system in the form of button clicks and window
resizes. We observe the system through a GUI. The simulation
also evolves over time, and so it is clear that we're not dealing with a pure
black box. Somehow we need to manage state over time. 



