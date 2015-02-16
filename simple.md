---
layout: default
title: Simple Systems
---

<h2> Thinking in Reverse </h2>
A system, by its nature, has requirements to which it must adhere at its boundaries. 
For example, we can twist a lamp's knob to turn light on and off.
Similarly, we can turn a faucet's handle to start and stop the flow of water,
we can flip to the next page in a book to start reading new content, and we can use 
email to type text in a box and click a button to send words across the
internet. These examples are simple enough, but they make us reflect on systems
in general and on a principle that, although it is obvious, is worthy of further
exploration. The principle is that the usefulness of a system
is contained in the abstraction that the system provides us, and we can fully understand
that abstraction in terms of the behavior of the system at its boundaries. 
In the lamp example, its boundaries are the knob and the light bulb. Determining whether
or not the lamp is behaving correctly is entirely a matter of whether or not its 
output behavior is a correct function of its input behavior. In other words, it's all 
about how things make sense at the boundaries. This principle is in fact made more worthy
of exploration precisely because it is obvious. It means that we will move forward
on solid footing. 

This style of thinking at the boundaries is often made explicit in my CAAM (Computational
and Applied Math) major, where
we're concerned all the time with finding a solution that satisfies some constraints. 
Finding such a solution is the same thing as finding a system that behaves correctly
at its boundaries, if we imagine that what we can "observe" at the boundaries is
precisely whether or not the system satisfies its given constraints.  In the
case of CAAM, we want to do things like find a vector that satisfies
a system of linear equations or a function that satisfies a differential equation.
Doing this type of thing is referred to as solving an *inverse problem*. An inverse
problem is naturally trickier than its corresponding forward problem. In the forward
case, we assume that we have a solution, and we simply need to check that the solution
satisfies the boundary constraints. For the inverse case, we don't start with the luxury
of a valid solution in hand. Somehow we must find one in the space of 
all possible solutions. 

To illustrate this with the lamp, the forward case would be if I gave you a full
physical description of a specific lamp: its bulb type, its circuitry, whether or not it's
plugged in, etc. Then you use the relevant physics to walk through how system output
responds to system input, which lets you determine whether or not the specific lamp is 
behaving correctly. The inverse case would be if I gave you a description of how a lamp
ought to work. Then you build a lamp that does what it's supposed to do. 

This reasoning about boundary constraints and inverse problems is pretty general and 
abstract. Why is it interesting? It is interesting because I claim that we
can always conceive of constructing a system as solving an inverse problem. By
adopting this frame of mind, we can naturally (and happily!) bias ourselves toward
making our systems simpler. 

<h2> Measuring What's Good </h2>

Let's continue bringing ideas over from CAAM. Often we have a solution that satisfies
the given constraints, but it's less optimal than some other solution. Now we're
dealing with a special flavor of inverse problem called a *constrained optimization* 
problem. Let's also sharpen our object of study and forget about lamps, books and faucets.
Our subject now is software systems. The boundary behavior is now either what a person
inputs and observes at a computer's I/O peripherals or what one software system
reads and writes internally, at the interface between itself and some other, distinct 
software system. The inverse problem is finding a program, in the space of all possible
programs, that behaves correctly at the boundaries. 

In the context of constrained optimization, this gives us the obvious constraint: 
the system must behave correctly at the boundaries. What remains now is to find our metric
for determining what is optimal&mdash;what makes one solution better than another.
On this subject, the right answer depends on one's interests. For example, 
performance-critical applications like high-frequency trading and game servers demand
that there is as little lag as possible between input stimulus and output response. 
Alternatively, one interested in virtuoso feats at the hardware level will prize
dexterity in the use of a computer's resources (such as in the culture of
<a href="http://en.wikipedia.org/wiki/Demo_%28computer_programming%29">demos</a>).

These metrics have their uses, but they are not my interest. The end game in this 
discussion is system simplicity. Simplicity, though, is too vague of a metric in the
context of optimization. Distilling the ideal of simplicity leads to three metrics
which can be
put consisely as the rates of *channelling*, *understanding*, and *extending*.
*Channelling* is a poetic spin on "programming" or "coding". The idea here is that the
coder is a medium who is carrying abstractions from the Platonic realm into the reality. 
There's some abstraction that we want to become real. "Wouldn't it be nice if there were a 
program to ...?" From asking that question, how can we get the best chanelling rate&mdash; 
that is, how can we construct a system adhering to the boundary constraints as quickly as
possible? 

The *understanding* metric asks how quickly one coder can understand code written by 
another coder. (This includes when we need to read our own code six months later.) Is
the code a reasonably natural representation of the core abstraction, which is the
reason we sat down to code in the first place? Or is the code in a sense *encrypted*, 
filled with incidental complexity and concerned excessively with quirks of the underlying
platform?

The *extending* metric has to do with the ease of making an existing system do 
new things, especially unpredictable things that even a thoughtful
programmer would not have planned for upon first designing the system. Do we have
to rewrite everything? And if we do have to do a rewrite, did it feel like a natural
necessity, or was there something lame about our platform that led us to unintentionally
code ourselves into a straightjacket?

Armed with these metrics, we have a means of evaluating software systems from the perspective
of constrained optimization. In particular, we choose for the current analysis to abstract
away performance and instead base our optimization on the rates of channelling, understanding 
and extending. 


<h2> An Illustration </h2>

(Clojure and Java factorial example)


 
