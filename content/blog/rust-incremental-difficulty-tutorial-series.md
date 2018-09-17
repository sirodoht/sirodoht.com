+++
title = "Rust incremental-difficulty tutorial series"
date = 2018-01-04
template = "post.html"
+++

> A response to Rust’s [Call for Community Blogposts](https://blog.rust-lang.org/2018/01/03/new-years-rust-a-call-for-community-blogposts.html) #Rust2018

This is a documentation improvement on learning Rust, derived from personal experience after picking up Rust and reading the Book v1, a few months ago.

## The problem

For me picking up a new programming language is hard because finding the successful learning path is hard.

The first step is usually obvious, it’s a “Getting started” article on the official docs. This includes the basic syntax and concepts. With Rust, the second step is easy too, it’s [The Book](https://doc.rust-lang.org/book/second-edition/). The third step would be to write your own thing, to solve a problem of your own; create a small project.

The problems with this are:
* What this project will be
* How hard it should be
* How I can learn if the result is low, medium or high quality

When learning, and especially when you are new to programming, you may pick up the wrong problems to solve with the tools you want to learn. Learning JavaScript by coding mathematical computation algorithms might not be the best idea and similarly learning Rust by building web applications is not either [1].

Secondly, you can’t know how hard the problem you want to tackle is when using a new programming language [2]. Coding a mass file renamer might be 10 times more time-consuming and difficult in C than in Python [3].

Thirdly, you can’t assess the result; whether it’s high quality Rust code or not. There might be open source clones, but who says they’re better or worse? In contrast with the previous problems, this is much harder to overcome, and again, especially if you are a beginner.

To sum up, we need:
* To know the correct problems to solve
* The level of difficulty of each one
* The reference solution of an expert


## The solution proposal

Along with the Book and Rust By Example add a series of high quality, Rust-suitable project examples.

These projects’ difficulty could escalate proportionately.

Here is a proposal from someone who doesn’t know Rust:  
0. Hello World
1. [Guessing game](https://doc.rust-lang.org/book/second-edition/ch02-00-guessing-game-tutorial.html)
2. JSON validator
3. curl clone
4. Poker
5. Lite Git clone

A Rust learner after completing those will have written a good chunk of Rust LOCs, assess their results and improve iteratively!

The requirements of these projects need to be described in detail so the novice can know exactly what they will need to create.

And of course, the solutions of these projects need to be available, heavily commented and written with best practices in mind. It should not be the best possible code nor the most efficient, probably the most readable and correct, though.

With these, a Rust learner can refer to exemplary, readable, beginner-friendly code that can guide them. Steps after that could be to create step-by-step tutorials for the projects (like the existing Guessing Game book chapter), or even screencasts, like [Gophercises](https://gophercises.com/) for Golang.

The existence of official tutorials, part of Rust docs, means that there will be a go-to resource for all new users, and a few example projects that will always be up-to-date and available for studying.


—

[1] At least for now.  
[2] Well, guessing might work, but we want to improve things here anyway.  
[3] Yes, C might be a more suitable language for this task, but Python is ok for learning.  


---

*This article was also published on [Medium](https://medium.com/@sirodoht/rust-incremental-difficulty-tutorial-series-8c09ecdd38e7).*
