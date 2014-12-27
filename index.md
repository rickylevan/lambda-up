---
layout: default
title: Demos
---

Here is some simple Clojure:

```clojure
(defn square [x] (* x x))
(= 16 (square 4))
```


A little bit of Java: 

```java
public static void main(String[] args) {
	System.out.println("Hello from Java!");
}

public int factorial(int n) {
	if (n == 1) {
		return 1;
	} else {
		return n*factorial(n-1);
	}
}
```

And here is another example of Clojure code:
Don't things just seem *cleaner*? And text. And text. And here is some more text I'm writing
just for the sake of tseeing how things wrap. Will they wrap? Will we ever know? What a mystery!



```clojure
(defn collatz [n]
	(loop [n n out 1]
		(if (= n 1) (conj out 1)
			(recur (if (odd? n) (inc (* 3 n)) (/ n 2)) (conj out n)))))
(defn get-delta-pos [this-ball that-ball]
    [(- (:x (:pos that-ball)) (:x (:pos this-ball)))
     (- (:y (:pos that-ball)) (:y (:pos this-ball)))])
```


<!-- And numbered:

	1. apples
	2. oranges
	3. pears -->

<!-- ![Christmas kid](http://i.imgur.com/X4dlJkT.jpg) -->
