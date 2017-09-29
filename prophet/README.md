## The Prophet of Floom predicts failures in distributed systems

This is dlv code. Download dlv from http://www.dlvsystem.com.

The dlv language is datalog with disjunction, under the answer set  semantics.
The code can be understood without delving deeply into the nonmonotonic reasoning literature, but I assume you know datalog.
I avoided situations where you have to think in terms of answer set semantics.
You can think of the code as datalog with rules that have disjunctions
in the heads, with a simple “quantum mechanics” semantics:
For a rule of the form
```
     a v b :- body.
```
if the body is true, then either a or b is picked; the world splits
into two possible worlds, one to which a is added, and another one in which b is added.

Strictly speaking, there is one place in the paxos code that uses nonstratified negation to run a little state machine, and in such a case the semantics isn’t that simple, but it’s still well-behaved because the ground program is stratified. (This could be done in a more elementary way, I just didn’t bother do fix this yet.)

All the special possible worlds code for reasoning about alternative computations is actually encapsulated by the delivery code (po.dlv and delivery.dlv) — only when a message is sent is a nondeterministic ordering decision made,
which in general creates alternative possible worlds.
So you can write normal datalog on top of delivery.dlv, and it would be just like in Bloom (but with straight datalog syntax) — you don’t need to worry about model checking. One could build a translator to map Bloom code to basic datalog and run it in this model checker.

I have written a simple unsafe key-value store (kv.dlv) and paxos (paxos.dlv, not worrying enough about corner cases yet).

There are some *_test.dlv files with instructions how to run stuff.

At the end, dlv produces an enumeration of possible worlds, each with the facts computable in that world (a trace of the computation that happened). You can kill worlds with constraints (vacuum decay, so to say), you can do analyses inside worlds, and you can perform brave (\exists world \phi) and cautious (\forall world \phi) reasoning over the set of possible worlds.



