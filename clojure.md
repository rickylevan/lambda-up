---
layout: code
title: Clojure Collision Logic
---

Read [Reddit](http://www.reddit.com) for all of your reddit needs.

## My First Section
Here is an example of the underlying collision logic. 

{% highlight clojure %}


;; collision logic --- now the input balls are the mutable atoms 
(defn collide! 
  ([ball]
   (let [this-ball ball]
     (doseq [that-ball (disj @balls this-ball)]
       (if (overlapping? @this-ball @that-ball)
         (collide! this-ball that-ball)))))
  ([this-ball that-ball]
   ;; compute new velocities from impulse physics
   (let [this-new-vel 
         (Point. (+ (:x (:vel @this-ball))
                    (/ (:x (get-impulse @this-ball @that-ball)) (get-mass @this-ball)))
                 (+ (:y (:vel @this-ball))
                    (/ (:y (get-impulse @this-ball @that-ball)) (get-mass @this-ball))))
         that-new-vel
         (Point. (+ (:x (:vel @that-ball))
                    (/ (:x (get-impulse @that-ball @this-ball)) (get-mass @that-ball)))
                 (+ (:y (:vel @that-ball))
                    (/ (:y (get-impulse @that-ball @this-ball)) (get-mass @that-ball))))
         tstar (get-collision-time @this-ball @that-ball)]
     ;; rewind time at old velocity to negative time tstar, and redo time at new velocity
     (let [this-new-pos
           (Point. (+ (:x (:pos @this-ball)) 
                      (* tstar (:x (:vel @this-ball)))
                      (flip-sign (* nudge tstar (:x this-new-vel))))
                   (+ (:y (:pos @this-ball)) 
                      (* tstar (:y (:vel @this-ball)))
                      (flip-sign (* nudge tstar (:y this-new-vel)))))
           that-new-pos
           (Point. (+ (:x (:pos @that-ball)) 
                      (* tstar (:x (:vel @that-ball)))
                      (flip-sign (* nudge tstar (:x that-new-vel))))
                   (+ (:y (:pos @that-ball)) 
                      (* tstar (:y (:vel @that-ball)))
                      (flip-sign (* nudge tstar (:y that-new-vel)))))]

     (doseq []
       (swap! this-ball assoc :vel this-new-vel)
       (swap! that-ball assoc :vel that-new-vel)
       (swap! this-ball assoc :pos this-new-pos)
       (swap! that-ball assoc :pos that-new-pos))))))


{% endhighlight %}

This is quite different from the corresponding implementation in Java.
In that paradigm, we had various mutations. The atomic, single nature
of a state change was not as easily apparent. 
 
