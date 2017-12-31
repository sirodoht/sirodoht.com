+++
title = "The MIU formal system"
date = "2016-04-23"
template = "post.html"
+++

When I started my undergraduate studies on Computer Science I was very enthusiastic about the theoretical foundations I was about to learn. In this quest I googled “best computer science books”. This will get you most of the CS classic and among them you will find *[Gödel, Escher, Bach: An Eternal Golden Braid](https://en.wikipedia.org/wiki/G%C3%B6del,_Escher,_Bach)*, a quite peculiar book.

*Gödel, Escher, Bach: An Eternal Golden Braid* (GEB from here on) started as a treatise on the proof of Gödel’s [Incompleteness Theorems](https://en.wikipedia.org/wiki/G%C3%B6del%27s_incompleteness_theorems#First_incompleteness_theorem), two of the most disruptive theorems in the field of Mathematics.

The first one, states that in a *formal system* [like Maths] there exist truths that can never be proved.

Your response may be “whatever” but try to think it in the following visualization. Imagine Maths as a graph, with each node as a theorem.

Mathematicians started out with the obvious truths. Theorems that are well-established and obvious are called axioms. For instance, an example axiom: *It is possible to draw a straight line from any point to any other point* from Euclid’s *Elements*. So, using these nodes (aka theorems), mathematicians advanced these axioms’ consequences to get to their adjacent nodes. Continuing this way, more and more theories were created, more and more theorems were discovered.

So, what the First Incompleteness Theorem says is that there are nodes, that do exist, but you can never reach out to them using the consequences of their adjacent nodes. Only by pure luck can you discover them. This is amazing. I always considered Maths to be distinctly systematic knowledge, but this completely disproves it.

The second theorem takes one step further. It states that if in a formal system [like Maths] there is a statement which proves its own consistency, then this system is inconsistent. This essentially seals what the first theorem claimed. It's like claiming that you *always* lie. If you do, then the statement "I always lie" would be a lie itself. Paradox.

Douglas Hofstadter was also astonished by not only the theorems themselves, but also by the incredible proofs that Gödel provided. Thus, he started a treatise on that proof. However, Hofstadter thanks to his polymath personality discovered that the ideas underlying Gödel’s proof, apart from our mind, could also be perceived by our eyes and ears. He presents this to us through the works of Johann Sebastian Bach and M. C. Escher respectively.

In this journey he elaborates on many topics. One of them is formal systems and in this realm he presents a puzzle, the infamous MU puzzle.

## The MU Puzzle

Let us assume a formal language MIU. Its alphabet is three letters: `M`, `I` and `U`. The starting string is `MI`. Its production rules are:

1. If you possess a string whose last letter is `I`, you can add on a `U` at the end. For example, since you start with `MI`, you can go to `MIU`.

2. Suppose you have Mx. Then you may add Mxx to your collection. e.g.: `MIU -> MIUIU` or `MUM -> MUMUM`.

3. If `III` occurs in one of the strings in your collection, you can make a new string with `U` in place of `III`. e.g.: `UMIIIMU -> UMUMU` or `MIIII -> MIU` (or `MUI`).

4. If `UU` occurs inside one of your strings, you can drop it. e.g.: `UUU -> U` or `MUUUIII -> MUIII`.

The challenge is to produce the string `MU`, or prove it cannot be produced.

Nota bene: These are one way rules. In addition, sometimes, more than one rules may be valid to be applied; in this case you have to pick the best fitting one in order to reach the desired string, `MU`.

These theories, namely formal systems, grammars, languages, inference rules, etc, belong to the domain of [Computation Theory](https://en.wikipedia.org/wiki/Theory_of_computation). It’s a very interesting, though deeply theoretical domain of Mathematics and Computer Science.

So, this is the end of this post. Try to solve that puzzle now! It's not hard at all!
