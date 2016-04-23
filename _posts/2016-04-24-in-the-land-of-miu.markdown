---
layout: post
title:  "In the land of MIU"
date:   2016-04-24 15:27:32
categories: maths, puzzles
---

When I started my undergraduate studies on Computer Science I was very enthusiastic about the theoretical foundations I was about to learn. In this quest I googled “best computer science books”. This will get you most of the CS classic and among them you will find *Gödel, Escher, Bach: An Eternal Golden Braid*, a quite peculiar book.

*Gödel, Escher, Bach: An Eternal Golden Braid* (GEB from here on) started as a treatise on the proof of Gödel’s [Incompleteness Theorem], one of the most disruptive theorems in the field of Mathematics. Essentially, it states that in a *formal system* (like Maths) there exist truths that can never be proved.

Your response may be “whatever” but try to think it in the following visualization. Imagine Maths as a graph, with each node as a theorem.

Mathematicians started out with the obvious truths. Theorems that are well-established and obvious are called axioms. For instance, an example axiom: *It is possible to draw a straight line from any point to any other point* from Euclid’s *Elements*. So, using these nodes (aka theorems), mathematicians advanced these axioms’ consequences to get to their adjacent nodes. Continuing this way, more and more theories were created, more and more theorems were *discovered*. I am using *discover* here, and not *invent* because we consider Maths a truth independent of us. Even if humans didn’t exist, Maths would.

So, what the Incompleteness Theorem says is that there are nodes, that do exist, but you can never reach out to them using the consequences of their adjacent nodes. Only by pure luck can you discover them. This is amazing. I always considered Maths to be distinctly systematic knowledge, but this completely disproves it.

Douglas Hofstadter was also astonished by not only the theorem itself, but also by the indescribably unbelievable proof that Gödel provided.

GEB started as a treatise on that proof. However, Hofstadter thanks to his polymath personality discovered that the ideas underlying Gödel’s proof, apart from our mind, could also be perceived by our eyes and ears. He presents this to us through the works of Johann Sebastian Bach and M. C. Escher respectively.

In this journey he elaborates on many topics. One of them is formal systems and in this realm he presents a puzzle, the infamous MU puzzle.

## The MU Puzzle

Let us assume a formal language MIU. Its alphabet is three letters: `M`, `I` and `U`. The starting string is `MI`. Its production rules are:

1. If you possess a string whose last letter is `I`, you can add on a `U` at the end. e.g.: Given `MI` you can have `MIU`.

2. Suppose you have Mx. Then you may add Mxx to your collection. e.g.: `MIU -> MIUIU` or `MUM -> MUMUM`.

3. If `III` occurs in one of the strings in your collection, you can make a new string with `U` in place of `III`. e.g.: `UMIIIMU -> UMUMU` or `MIIII -> MIU` (or `MUI`).

4. If `UU` occurs inside one of your strings, you can drop it. e.g.: `UUU -> U` or `MUUUIII -> MUIII`.

The challenge is to produce the string `MU`, or prove it cannot be produced.

Nota bene: These are one way rules. In addition, sometimes, more than one rules may be valid to be applied; however, you have to find the best fitting one in order to reach the desired string, `MU`.

These theories, namely formal systems, grammars, languages, inference rules, etc, belong in the domain of [Computation Theory](https://en.wikipedia.org/wiki/Theory_of_computation). It’s a very interesting, though deeply theoretical domain of Mathematics and Computer Science.

**talk about the second incompleteness theorem on the first section**
