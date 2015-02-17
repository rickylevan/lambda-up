---
layout: default
title: Simple Systems
---

<h2> Thinking in Reverse </h2>
A system is all about the behavior at its boundaries. 
We can twist a lamp's knob to turn light on and off.
Similarly, we can turn a faucet's handle to start and stop the flow of water,
we can flip to the next page in a book to start reading new content, and we can use 
email to type text in a box to send words across the
internet. These examples are simple enough, but they make us reflect on systems
in general and on a principle that, although it is obvious, is worthy of further
exploration. The principle is that the usefulness of a system
is contained in the abstraction that the system provides us, and we can fully understand
that abstraction in terms of how the system acts at its boundaries. Its behavior at its 
boundaries captures the essence of the system as a tool, and why we find the system to be useful.
In the lamp example, its boundaries are the knob and the light bulb. Determining whether
or not the lamp is behaving correctly is entirely a matter of whether or not its 
output behavior is a correct function of its input behavior. 

<a href="http://xkcd.com/722/">
<img style = "width: 600px;" alt="room selfie" src="/lambda-up/assets/computer_problems.png"></img>
</a>

This style of thinking at the boundaries is often made explicit in my CAAM (Computational
and Applied Math) major, where
we're usually concerned with finding a solution that satisfies some constraints. 
Finding such a solution is the same as finding a system that behaves correctly
at its boundaries, if we imagine that what is "observable" at the boundaries is
precisely whether or not the system satisfies its given constraints.  In the
case of CAAM, we want to do things like find a vector that satisfies
a system of linear equations or find a function that satisfies a differential equation.
This sort of thing is referred to as an *inverse problem*. An inverse
problem is naturally trickier than its corresponding forward problem. In the forward
case, we assume that we have a solution, and we simply need to check that the solution
satisfies the boundary constraints. In the inverse case, we don't start with the luxury
of a valid solution in hand. Somehow we must find one in the space of 
all possible solutions. 

To illustrate this with the lamp, the forward case would be if I gave you a full
physical description of a specific lamp: its bulb type, its circuitry, whether or not it's
plugged in, etc. Then you use the relevant physics to walk through how system output
responds to system input, which lets you determine whether or not the specific lamp is 
behaving correctly. The inverse case would be if I gave you a description of how a lamp
ought to work. Then you build a lamp that does what it's supposed to do. 

This reasoning about boundary constraints and inverse problems is pretty general and 
abstract. What makes it interesting? It is interesting because I claim that we
can always conceive of constructing a system as solving an inverse problem. By
adopting this frame of mind, we can naturally (and happily!) bias ourselves toward
making our systems simpler. 

<h2> Measuring What's Good </h2>

Let's continue bringing ideas over from CAAM. Often we have a solution that satisfies
the given constraints, but it's less optimal than some other solution. Now we're
dealing with a special flavor of inverse problem called a *constrained optimization 
problem*. Let's also sharpen our object of study and forget about lamps, books and faucets.
Our subject now is software systems. The boundary behavior is now either what a person
inputs and observes at a computer's I/O peripherals or what one software system
reads and writes internally, at the interface between itself and some other, distinct 
software system. The inverse problem is finding a program, in the space of all possible
programs, that behaves correctly at the boundaries. 

In the context of constrained optimization, the obvious constraint is that
the system must behave correctly at the boundaries. What remains now is to find our metric
for determining what is optimal&mdash;why one solution better than another.
On this subject, the right answer depends on one's interests. For example, 
performance-critical applications like high-frequency trading and game servers demand
that there is as little lag as possible between the input stimulus and the output response. 
Alternatively, one interested in virtuoso feats at the hardware level will prize
dexterity in the use of a computer's resources (such as in the culture of
<a href="http://en.wikipedia.org/wiki/Demo_%28computer_programming%29">Demos</a>).

These metrics have their uses, but they are not my interest. The end game of this 
discussion is system simplicity. The tangled mess of a system is idealized by the
<a href="http://en.wikipedia.org/wiki/Rube_Goldberg_machine">Rube Goldberg machine</a>.
I imagine its opposite, the delightfully clean and elegant system, as a grid of prisms
and mirrors: each of its components are clear, composable and manifestly necessary. To move
from the former to the latter is an example of moving *lambda-up*.

<img style = "width: 400px;" alt="room selfie" src="/lambda-up/assets/rubegoldberg.jpg"></img>
<img style = "width: 400px;" alt="room selfie" src="/lambda-up/assets/prism.jpeg"></img>


Simplicity, however, is too vague of a metric in the
context of optimization. Distilling the ideal of simplicity leads to three metrics
that can be
put consisely as the rates of *channelling*, *comprehending*, and *composing*.
*Channelling* is a poetic spin on "programming" or "coding". The idea here is that the
coder is a medium who is carrying ideas from the pure abstractions of the mind into reality. 
There's some abstraction that we want to become real. "Wouldn't it be nice if there were a 
program to ...?" From asking that question, how can we get the best chanelling rate&mdash;that is,
how can we construct a system adhering to the boundary constraints as quickly as
possible? 

The *comprehending* metric asks how quickly one coder can understand code written by 
another coder (or when we need to read our own code six months later). Is
the code a reasonably natural representation of the core abstraction, which is the
reason we sat down to code in the first place? Or is the code in a sense excessively *encrypted*, 
filled with incidental complexity and overly concerned with quirks of the underlying
platform?

The *composing* metric has to do with the ease of joining our code with some other code elsewhere.
There's often trouble associated with this sort of thing. But does the trouble feel natural or does it feel
crazy? Is it surprisingly easy to compose our programs, as though we were stacking together legos? 
Or do we have to write a tremendous amount of glue that is totally unrelated to the heart of the problem?


Armed with these metrics, we have a means of evaluating software systems from the perspective
of constrained optimization. In particular, our current analysis abstracts
away performance and instead bases its optimization on the rates of channelling, comprehending 
and composing. 


<h2> An Illustration, Java vs. Clojure </h2>

Let's consider a concrete problem to illustrate the above ideas. Our desired system has the 
boundary behavior of computing the factorial function. The system is a simple black box. 
Its only boundary constraint is that the system must emit,
after some finite time, the application of \\(f\\) to the input stimulus \\(n\\), where
\\(f\\) is defined by \\(f\(n\)=n!\\). We now play the role of
the medium. We want to quickly channel this abstraction into reality, and we want the
resulting code artifact to be both clear and easily extendable. 

What follows is a pair of code segments in Java and Clojure that are solutions to the 
above boundary constraint. To keep things simple, I assume that \\(n\\) is small enough so that \\(n!\\)
will not overflow our internal representation of an integer. (This is an example
of a recurring problem: 
<a href="http://www.joelonsoftware.com/articles/LeakyAbstractions.html">
Leaky abstractions</a> are inevitable. Battling them is a war
against entropy that always demands new mental energy. More on this in the future.)

Let's first talk Java:

```java
public int factorial(int n) {
	int out = 1;
	for (int j = 1; j <= n; j++) {
		out = out*j;
	}
	return out;
}
```

The code here is brief enough that we can channel, comprehend and compose it
quite easily. Nevertheless I'll zoom in on the details. Even in this simple example, there
is plenty to talk about, and the points here will generalize to larger systems. 

One thing to notice about the code is that it is
explicitly time-dependent. It has a flavor: "Do this thing, then keep doing this
other thing until some condition fails, then return the value stored over here." 
Another thing to notice is that the variables
("n", "out" and "j" in the code) lack the semantics of names.
Instead, they are thin wrappers around explicit reference to memory
locations inside of the machine. They're not names, but places, ready for mutation at
a moment's notice. 

The Java code is of course aware of the boundary constraints. It does in fact compute the factorial
function (assuming that we feed it a non-negative integer \\(n\\) small enough to avoid overflow). 
But I can't help but feel that the core abstraction, \\(f\(n\)=n!\\), has been *encrypted*
more than necessary. With time and with attention to detail, we can always *decrypt* the meaning of the code. 
Say the Java method were poorly named, as "number-transformer" instead of "factorial". We
could still walk through the sequence of commands to discover that we are indeed computing the factorial
function. However, this decryption process wastes mental energy, and forces the coder to push the task at hand
out of his mind and instead focus on less relevant details. Of course, keeping track of
some detail is always necessary. The term "coder", for one who writes software, is especially apt, because
the coder is one who writes *code*, in the sense of a special language that is harder 
to understand than the plaintext. We have to do this because the plaintext, in this analogy,
is a pure abstraction of the mind, and that of course can't actually run. 
Doing some form of *encryption*&mdash;making things a little more hidden, piling up a little incidental
complexity&mdash;is always necessary to get something
to actually work on a real machine. The coder is thus always, to some extent, both an encryptor and a creator of details.
The goal, in light of the constrained optimization problem 
posed above, is to do as little encryption and to create as few details as possible. 


To that end, let's look *lambda-up* and try to think in reverse. One way we can reduce the amount of encryption is 
change our primitives: the basic elements we stack together to build higher abstractions. Let's see if 
we can think of runnable code without a baked-in assumption that we plan to run it on a 
<a href="http://en.wikipedia.org/wiki/Von_Neumann_architecture">Von Neumann machine</a> or a 
<a href="http://en.wikipedia.org/wiki/Turing_machine">Turing machine</a>. Instead, let's see how close we can get 
to the essence of the \\(n!\\) (which is simply the
product of the numbers \\(1\\) through \\(n\\)) 
and work backward from there. 

Here is some Clojure code that does just that:

```clojure
(defn factorial [n] (reduce * (range 1 (inc n))))
```
 
In this example, there is no time-dependence or bashing of memory locations. Of course, these things have
to ultimately happen inside of a modern machine, but from the perspective of thinking in reverse from the
factorial abstraction, we don't care. 

The code cuts close to the heart of the problem. But it's worth noting that, even here, there are some imperfections. 
One thing that requires a moment of thought is why we need to use the \\(inc\\) function. We have to do so because
\\(range\(1,n\)\\) returns the numbers from \\(1\\) to \\(n-1\\), which most of the time is exactly what we want,
but here results in a minor blemish. Another note is that Clojure's \\(reduce\\) function will multiply 
\\(1\\) and \\(2\\), then to that result multiply \\(3\\), and so on. But multiplication is 
<a href="http://en.wikipedia.org/wiki/Commutative_property">commutative</a>, so there
is no need to specify this exact means of multiplying our numbers together. One could imagine a clever platform 
on a multicore machine that could do the multiplication in parallel. But if I don't imagine that my code
will be running on such a machine, and if \\(n\\) is small, it would be tedious to define my own special version
of \\(reduce\\). Likewise, defining my own special version of \\(range\\) to include the ending value isn't ideal, 
because people are familiar with conventions, and now there would be one more line of code to read. 

The point of discussing these imperfections is to show that there are always some trade-offs to elegance. But that doesn't
mean that one solution to given problem can't still be decisively better than another. This is indeed the case
in the Clojure and Java code segments, if we measure them by the metrics of channelling, comprehending, and composing. 
Regarding channelling, the Clojure code requires less typing, but more importantly, the fact that it returns the 
product of the numbers \\(1\\) through \\(n\\) is
immediately obvious. The uniform syntax and lack of boilerplate make the code easier to 
comprehend. And finally, the Clojure
factorial function is more composable in the context of concurrency. Since we're not manually mutating memory locations,
the code is thread-safe and so can be confidently inserted into a concurrent application.

If you also like the idea of settling for nothing but the best in terms of quickly bringing clear and composable
abstractions into the world (aka "managing complexity" and "making it work yesterday"), then I hope that you enjoyed this post!
This intro naturally has plenty of loose ends, and there is much more to talk about. 

<!-- is a great help to have a name simply refer 
to an eternal and unchanging value (at least in its given scope). If we don't have this, 
then identifiers aren't truly names. Instead, they are a useful but still weak abstraction.
They are aliases for memory locations awaiting mutation. This makes it more difficult
to understand what an identifier means, because of the time-dependence. -->






