---
layout: default
title: BallWorld, a Field Report
---

<h2> Recap </h2>

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

Well, dear reader, it should be no surprise by now that I disagree! In COMP 310 at Rice
last semester, we built up, over the course of a few weeks, a simulation called BallWorld. 
Here's a screencap of how a single frame looks. 

<img style = "width: 450px;" alt="room selfie" src="/lambda-up/assets/ball_world.png"></img>

You can run BallWorld for yourself right away if you have 
<a href="http://leiningen.org/">Leiningen</a> installed. Simply
clone the <a href="https://github.com/rickylevan/ballworld">repository</a>,
navigate to that directory, then enter "lein deps" then "lein run". Since Clojure
runs on the JVM, it should work on your machine without any hassle. 



