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

This style of thinking at the boundaries is often made explicit in applied math, where
we're concerned all the time with finding a solution that satisfies some constraints. 
Finding such a solution is the same thing as finding a system that behaves correctly
at its boundaries, if we imagine that what we can "observe" at the boundaries is
precisely whether or not the system satisfies its given constraints.  In the
case of applied math, we want to do things like find a vector that satisfies
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

Optimization understanding. 

<h3> An Illustration </h3>

Clojure and Java factorial example. 


 
