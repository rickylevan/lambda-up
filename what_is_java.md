---
layout: default
title: What is Java?
---

Lately I have been interested in the theory of programming languages. 
I say *theory of programming languages* 
instead of *programming language theory*, because the latter is an established
field of research--one filled with brilliant ideas about which I know very little. 
My interest in theory is less in the sense of developing a formal, axiomatic
system, and more in the sense of finding intuitive ways to understand things
from first principles.

To this end, I want to ask some fuzzy questions, such as *What is a programming
language?* Instead of giving a formal definition, I want to think in a more 
relaxed, practical sense about why we use programming languages. What, exactly, 
do they buy us? In particular, to what extent is Java a good programming language?
Does Java give us as much power as we'd like to purchase the important abstractions?
To develop this line of thinking further, I will first need to explore that
ubiquitous, magical word in computer science: *abstraction*.

Abstraction is the pivotal concept. It is the reason why computers are useful
in the first place. Why have electrons furiously zap through our computers?
The reason is that computers are abstraction machines. To call them "information
processors" is to beg the question of what is processing. For some processing
to do something other than waste heat, it needs to be the servant of some
abstraction.

Abstractions 
come in many forms. It's tricky to see what exactly is the common thread between
them, other than that things are in some way getting "abstracted"--they're getting
simpler (or if you prefer, they're going lambda-up).
Here are some examples of abstraction, to make this concrete.

1. Photons hit my retina. My brain takes this information and abstracts the retinal pixel
grid into a world of discrete objects.

2. Sound waves hit your ear. Your brain first abstracts the frequencies into a 
stream of discrete words. Then it uses grammar (your brain must know the grammar
rules, even if you can't explictly state them!) to abstract the stream of words 
into their meaning.

3. An ASCII table abstracts the byte 00100001 into the character 'A'.

4. The economy abstracts the local phenomenon of individuals' desire for
purchasable objects into global phenomena such as supply and demand.

So we see there are some similarities between abstraction, parsing, and finding
out what things *mean*. The ultimate arbiter of meaning is in the human mind.
So, some abstractions at that highest sense we have is the ability to talk to 
family far away. 
So we could say that the telephone system abstracts electromagnetic phenomena 
into me feeling happy that I can talk to my family.

That the ultimate arbiter of meaning belongs in the mind is something illustrated 
nicely by this xkcd comic: http://xkcd.com/722/. Who's to judge that the metal rectangle
of lights is wrong? Of course, the real trouble is that the abstractions are wrong.
In particular, the mind judges that the abstractions are wrong.
That's what bugs and glitches essentially are: When our abstraction machines are not
abstracting the way that they are supposed to. If we forget about this, then we could 
that computers always work because they always follow the laws of physics.

Thinking about all this gets us closer to thinking about the essence (in a fuzzy) way 
of programming languages. The fundamental issue when programming--always--is that there
is some sort of abstraction I want, and there is some set of existing stuff already out 
there. (We're always standing on the shoulders of giants.) The language is some means of
abstracting existing stuff into what I want.

To illustrate, say I want to write a function to compute the factorial of a positive
integer *n*. In the abstract sense, I want a black box where I put in some *n*, wait for
some finite time, and then receive my *n!*. I want this abstraction to become real. I want
my reality to become a reality where this is a *thing*. The ability to put in an *n*, wait
for a while, and get back out an *n!* -- this needs to be a part of the set of things
that now exist.

The first imperative is to figure out how we can know in the first place what it is that
we are looking for. We're not concerned right now with how we're representing our numbers--
ints, doubles, roman numerals, tally marks. In a sense abstracted over each of the representations, 
what actually *is* the right answer? 

Then we must ask: What tools are at our disposal that we can use to abstract things with?
I could hire the guy to draw the circles, unfurling them in rows and then lining them all 
up then counting them at the end. This is dumb only in the sense that we have a built-in
conception of what is optimal: we instinctively know that---all things equal---we want
our solutions to be fast and inexpensive.

(Expensiveness is subtle because it exists on multiple fronts: Energy used by the computing
machines, as well as money paid to develop software.)

A separate tangent too: This stuff will need to be unified! What sorts of tools are at our
disposal? What are our primitive things that exist, and how sophisicate is our "grammar"
for assembling the things that exist into new things that we desire?

For example, here is a Java mode of thinking about the problem:

```java
public int factorial(int n) {
	int out = 1;
	for (int j = 2; j <= n; j++) {
		out = out*j;
	}
	return out;
}
```

In contrast, here is a Clojure means of thinking about it:

```clojure
(defn factorial [n] (reduce * (range 1 (inc n))))
```


There is a big difference here! The abstraction we care about is to return the product
of the numbers 1 through n. That's the abstract idea. The product of the numbers 1 
through n. The clojure program is a nice representation of this (with a slight wart 
that we must say (inc n), because *range* (for reasons that elsewhere usually make sense)
cuts off the final number). 

But now Java makes us think instead at the level of the machine. Instead of thinking about
returning the product of the numbers 1 through n, I think instead at the level of our computing
machines. Say, if you understand the way computing machines work: Say, they can do things 
like jump and branch and do arithmetic and move data between memory locations... You can 
assemble, using these primitives, an abstraction machine that does what you want. 

In the case of factorial it is simple enough to be harmless. But in general, there should always
be a sense of forboding when one must "encrypt" the desired abstraction into a much lower 
representation to get it to work. It adds to the complexity of things. (Where complexity is
a villian! Abstraction is the knight in shining armor!)

(Thinking of programming as a sort of encrypting also makes *coding* a really nice name for it.)

(Also, remember Knuth on pre-mature optimization.)

So what are some of the metrics we should consider from the higher-lambda perspective?
(Sometime you gotta explain your lambda-up model of computing). 
Three rates:
--Channelling
--Understanding
--Extending

For my purposes now, I ignore the expenditure of computing resources. Obviously this way of 
thinking is not always useful, but it undoubtedly has a place. There are certain way of thinking
that we can only unlock once we agree that certain things we will leave out our model.

Another funny thing is this design vs. user experience picture: http://i.imgur.com/hClOzhD.jpg.
An iPhone app provides a UI for the user to do something, to interact with the world. The
user is using the provided abstractions to achieve some goal. Programming is the same. The
extension of it is that it we are using the existing abstractions to generate new abstractions,
whereas the end-user (i.e., non-programmer) of some app isn't going to the meta-level of 
trying to build new abstractions with the existing abstractions. Rather he is just using
the abstractions already there for some terminal purpose. 

But! The principle is the same. Programming languages provide us with a user experience much
like a web page or a path for walking. How much is Java like the clean sidewalk where
in practice it ends up being so often more useful to cut through the grass? What price do
we pay for cutting through the grass? And also, what is it that determines how often 
we feel the need to walk through the grass in the first place? The answer to the latter
question has to do with the extent to which our programming language carves reality 
at the joints. 




