+++
title = "An anecdotic tour on the history of programming languages"
date = 2017-04-09
template = "post.html"
+++

> Disclaimer: The following 2514 words might not be wholly accurate.

Once upon a time, in 1972, the year of the last manned Moon landing, a programming language was born:

C, a general purpose, procedural language was designed by Dennis Ritchie, one of the two Unix legends, at Bell Labs (which as of 2016 are a subsidiary of Nokia).

It was named C because it was an improved B, a previous programming language, which was a simplified BCPL (hence its name).

After they wrote C, they decided to re-write Unix to it. This venture was completed steadily and in parts.

During the end of the decade, and in the next one (80s) versions of C were implemented for a wide variety of computers, including the IBM PC. This resulted in C becoming ubiquitous and the go-to language for systems.

Many people worshipped C. They created religions, cults, sects. Mind control techniques were discovered in old journals, and then, it happened.

An old tomb was discovered in Mesopotamia with its walls covered in C code. How could it be? A language for computers written in 1972 being a part of an ancient religion?

Only joking.

But really, many people loved C, like the creator of the Linux kernel, Linus Torvalds. Others didn’t like it so much, maybe they felt that something was missing. Such is the case of Bjarne Stroustrup, the man behind C++.

Bjarne was into Object Oriented Programming, so one sunny day in 1982 he thought:

> Maybe I should create a language like C, but with classes. I’ll name it ‘C with Classes’.

When one year later:

> Maybe that was not such a good name. I’ll rename it to C++. Yeah. That’s better.

Linus was not thrilled at all by C++. To be precise, he resented it. Mainly because of lack of portability and *inefficient abstracted programming models*, as he says.

Five years later, in 1987, Larry Wall started working on Perl and at the end of the year version 1.0 was ready. Unfortunately, Larry, like all programmers, was more interested in writing code than its documentation, so it took 4 years and the wide adoption of the language for the Camel Book, the classic Perl book, to be written.

At the same year, in Portland, OR, the Functional Programming Languages and Computer Architecture (FPCA ’87) conference was held. It was an academic conference. One of its outcomes was the participants’ decision that they really like *Miranda* (a proprietary lazy functional language) and its descendants, and they should better create a committee to define an open standard for all these languages.

It took them three years, and in 1990 the *Haskell Language and Library Committee* announced version 1.0.

Due to this history, Haskell is considered an academic language and does not have much adoption in the industry. However, there are various companies across the world that do use it.

One year later, only in 1991, Guido van Rossum released the first version of Python. 🎉. He really enjoyed Monty Python, so he thought to use half their name. After all, it’s also a snake.

Guido didn’t want to just create a language. He had a vision, and a mantra. The Zen of Python, as they call it, is the core philosophy of the language. It includes abstract comparisons between concepts such as beauty, simplicity, and complexity, and it is adored by all Pythoneers.

Despite and along with all that, a lot of people came to like Python. It is also very multi-paradigm. It is imperative, object-oriented and with multiple Lisp-like functional features. It was the first language to put first the intuitiveness of the user in contrast of the underlying mechanisms of the compiler.

Four years later, in 1995, NASA’s Galileo Probe entered Jupiter’s atmosphere and the Sudden Oak Death (SOD) was first reported. *Phytophthora ramorum*, the oomycete plant pathogen behind SOD, is the reason that many oak populations in California and Oregon died. It is also believed that this organism is the cause of a proportionally large number of successful programming languages being created this year, both in California and in other areas too.

The spotlight on Java, JavaScript, PHP, and Ruby.

Yukihiro Matsumoto was writing mostly Perl and he was happy about it. He was also quite intrigued by Python, but with some complaints present:

> It seems to me that Python is not a true object oriented language. I’d say it’s an imposter. OOP features appear to be some kind of add-on. As if they said, “yeah, throw that inside too”.

It was obvious that Guido wanted to support many paradigms, so object-oriented concepts were not top priority in the language design process.

But Matz really believed that OOP is the future, and not one of the features. And thus, Ruby was born, with its name, of course, paying homage to Perl.

In Ruby everything is a function call, even arithmetic operations with `+` and `-`. And thus, parenthesis in function calls are in most cases optional.

The above decisions polarized the software community to:

> Oh my god! This is so beautiful! I’ll write everything in Ruby now!

and

> Oh my god! This is fucking insane! How could one think of such atrocity?

Features such as `5.times { do_this }` contributed to further polarization, even in the UK:

> Ruby lover: Oh my god! This is so expressive! Even more expressive than Python! I love it!

> Ruby skeptic: Oh my god! This is bloody mental! Oh, the horror…

Evidently, apart from successful, 1995 programming languages were also very contentious.

It was a fine day of 1995 when Rasmus Lerdorf thought:

Why not extract all those CGIs written in C that I have for my home page in something separate? I’ll add web forms integrations and db libs and I’ll call it Personal Home Page/Forms Interpreter, or just PHP/FI!

In hindsight, it was one of the most controversial ideas of the web. PHP was unique in the development speed of a dynamic website, and that made a lot of people choose it even though Rasmus didn’t like that his fast hack became one of the most used programming languages. It still lacked good design and its independent development resulted in various inconsistencies inside the language. Undeniably, [worse is better](https://en.wikipedia.org/wiki/Worse_is_better).

The Sudden Oak Disease took effect even in large companies, like Sun Microsystems. They somehow got the idea that they should create a new *write-once run-everywhere* programming language. They would do that by creating a virtual machine for all platforms, with a common API. Its name: *Oak*; named after an oak tree that stood outside its creator’s, James Gosling’s, office. This, of course, verifies the theory that the Sudden Oak Disease is accountable for the creation and success of the four languages of 1995.

Oak was later renamed to *Green* and finally *Java*.

Java follows a classical inheritance object oriented paradigm. This, according to James, was not a good idea after all and had he been asked to re-create Java he would throw the inheritance hierarchy idea under a tree (probably an Oak) in favor of object delegation.

This is quite interesting as it turns out, because the language that does fulfill Java’s dream for write-once run-everywhere turned out to be JavaScript, which has object delegation.

And thus, we reach the final item on the 1995 list. JavaScript.

There are many programming languages in this world, and their distribution with respect to language design is [Gaussian](https://en.wikipedia.org/wiki/Normal_distribution). The majority has a good design; some have somewhat good or somewhat bad design; and very few have an outstanding design or a horrifying one. Had you been asked to choose from one of those categories for the language that would run to the greatest number of computers ever, which would you pick? As it turns out, we did end up beyond three sigma, just not the positive edge. The spread was gradual, few noticed.

It was a cold afternoon of 1995, at the Netscape Communications HQ in Mountain View, CA, when the company hired Brendan Eich to embed Scheme inside their browser, Netscape Navigator. It was only Scheme, a Lisp dialect; what could go wrong? However, as fast a developer as he was, he wasn’t able to start working on it until something, well… everything changed.

It took Brendan ten days to create a prototype of a language called *Mocha*. *Another* coffee related word you might think? Might there be an off chance they are related? Indeed, Netscape made a deal with Sun Microsystems to include a lightweight scripting Java-like language to compete with Microsoft. Mocha seemed an appropriate name. It was a beautiful name, but it was deemed as a missed opportunity to advertise Java; so after a brief stint with *LiveScript*, *JavaScript* was conceived.

Brendan had a vision with Mocha, and JavaScript is influenced by a wide variety of different paradigms of languages. Features like first class functions, prototypal inheritance, and event driven are what make JavaScript such an interesting language to work with. Furthermore, JavaScript due to its quirks and design flaws is a difficult language to master given its simple (yet elusive) features. Some say this perpetual challenge motivates them; others stay away while appreciating their lack of masochism.

After 1995 and until the end of the decade not much happened.

Then in 2000, Microsoft decided to create its own Java. The outcome was C#.

Java’s creator James Gosling noticed that and didn’t refrain from giving voice to his thoughts:

> C# is sort of Java with reliability, productivity and security deleted.

Thankfully, C# diverged from Java with its subsequent versions and with the introduction of a wide variety of features. It is, also, the main language of the .NET platform, Microsoft’s web platform.

2004 came and Martin Odersky’s resolve to make his vision a blissful reality was being accomplished. His dream was to merge the old philosophy of functional programming and the new of object orienticism. The result: Scala, a programming language that encapsulates the functional paradigm inside object orienticism. Scala has a strong type system like Java, though very concise, unlike Java. It has many other connections with it, like the fact that Scala can be compiled to JVM bytecode and also, quite predictably, call Java libraries directly from Scala code.

Three years later, in 2007, Rich Hickey, who, like Martin liked the JVM and functional things, published his 2½-years work on creating a modern Lisp. *Clojure* has acquired a following over the last years, and there is a variety of companies that use it on production web environments. Along with the implementation for the JVM, there is also ClojureScript, which compiles to JavaScript. This means you can write Clojure for the frontend. 🎊.

Then, in 2009, at Google, something of eminent importance happened. Ken Thompson (the second Unix legend), Rob Pike, and another person on whom there is no Wikipedia article, Robert Griesemer, created Go. These gentlemen were also in the C++ hate club because C++’s complexity served as a *primary* (!) *motivation for the initiative*. It is speculated that the colloquy at Google at that time was:

> Ken: “Oh man, I just hate C++!”  
> Rob: “I know. It sucks…”  
> Robert: “Hey, let’s create our own language that would be super simple. It won’t have classes. Or destructors. Or-”  
> Ken: “Or generics!”  
> Rob: “Or exceptions!”  
> Robert: “Or operator overloading!”  
> Ken: “Or inheritance.”  
> Rob: “Or malloc.”  
> Robert: “Or while.”  
> Rob: “Not even while? Neat :wink:”  
> Ken: “Or variables!”  
> *(all three look puzzled)*  
> Ken continues: “OK, let’s have variables. But we’ll have type inference.”

Go has been widely criticized that it threw some decades of programming experience out of the window, and did not include the above — and many other — features. This decision, however, had the effect of having a gradual learning curve while over-protecting you from making common mistakes.

As far as concurrency is concerned, there are two primitives in Go, namely goroutines and channels, which implement what is known as *Communicating Sequential Processes*, an idea first described by Tony Hoare (the human who invented *quicksort*, and other important CS theories). This is considered one of the strong points of Go.

One year later, in 2010, a personal project of Graydon Hoare’s was announced by Mozilla that it is being sponsored. The beautifully named *Rust* lang was quietly born in 2006 and it took only 9 years to reach 1.0, in 2015. Since then, it has been one of the [most loved](https://stackoverflow.com/insights/survey/2017#most-loved-dreaded-and-wanted) programming languages.

It is fascinating how much thought has been poured into the design of this language, and particularly the design of its type system, its unique feature. Rust is designed to be memory safe. It achieves this through concepts such as *owned variables*, *borrowed pointers* and *variable lifetime management*. In addition, it does not support classical inheritance but it has a *trait* system, inspired by Haskell.

Then in 2011, something exciting happened. Ruby and Erlang had an offspring. It’s called *Elixir*, and many people think very highly of it.

Before talking about Elixir, though, let’s do a background check on its less known procreator.

Erlang is a language from 1986, created at Ericsson, and remaining proprietary until 1998. Erlang is not just a language, it’s a cult. People who believe in Erlang have a specific [worldview](https://en.wikipedia.org/wiki/Erlang_%28programming_language%29#Erlang_Worldview) which includes arcane decrees such as *Everything is a process* and *Error handling is non-local*. Joe Armstrong, one of the three inventors, has said:

> If Java is ‘write once, run anywhere’, then Erlang is ‘write once, run forever’.

Given that he said this in 2013 can we hold him accountable for Erlang if Java doesn’t turn out to be “run everywhere”? 😏

Erlang has a proven track record of large scale, distributed, high availability web services. Furthermore, it has some magnificent characteristics like fault tolerance, hot code swapping, and pattern matching. José Valim decided to merge these breathtaking features with some other, friendlier ones, along with some Ruby ideas. The result is Elixir.

Elixir is fully compatible with Erlang’s VM, *BEAM*. It also provides nice tooling, which Erlang does not have, and it has successfully won over people, mainly from the Ruby community. Its flagship web framework is *Phoenix* which has accumulated rave reviews.

Chris Lattner, the legend behind LLVM, while at Apple, invented and led the development of *Swift*. It began in 2010 but it wasn’t until 2014 that we learnt about it. Swift has both influenced and been influenced by Rust. It is a compiled language with a strong static type system while it adheres to protocol-oriented programming, an idea also known as interfaces.

The memory management is done using *Automatic Reference Counting* (ARC), which includes compile-time memory deallocation decisions, a Rust resemblance. Swift, a year after its announcement became open source, which enabled developers to extend it beyond Apple’s interfaces. Its use on other domains like the web is rising, as does the adoption from other companies.

The history of programming languages is very interesting to read about. It urges you to make predictions for the future. My bet is that Swift, Rust, and Go will win over many domains, with the largest one being that of C and C++.

Hopefully, after 45 years, C will pass the scepter and let us prove to ourselves that we now know software better.

<div class="notes-separator"></div>

**Notes**

*This article was originally published on [HackerNoon](https://hackernoon.com/an-anecdotic-tour-on-the-history-of-programming-languages-928bc6e9a9a8).*
