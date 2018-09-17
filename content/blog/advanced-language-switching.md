+++
title = "Advanced Language Switching"
date = 2014-12-08
template = "post.html"
+++

One field where there is not as much development as I would like is language input, other than English. This is understandable for many reasons, but there is so much room for improvement. I am Greek and the situation is pretty good, but I cannot imagine how Chinese or Japanese and other people with hundred letters in their alphabet, write in their language. I have read there is (or was) much debate about how many Japanese letters will be included in the UTF* format.

In Greek, as I said, you can easily setup you keyboard layout in any operating system I have seen, but there is none with advanced keyboard layout switching techniques.

## Advanced Keyboard Layout Switching Techniques

One very common thing, which always causes time to be lost is that specific fields always take English, and never Greek. For instance, the browser URL bar. You are never going to enter Greek characters there, so it would be a very good idea to *lock* this input field on Greek. Of course, this would happen on a OS level, which means that somehow the operating system should understand which text input field is active, on any open program.

Of course, the problem starts with the fact that there are not (and can't be) enough letters on the keyboard. So, we devise keyboard layout switching mechanisms, that is specific keyboard shortcuts. These need to be easy and fast to make. Apple gave the most thought into this matter and assigned `Cmd+Space`. Microsoft, until Windows 7, had `Alt+Shift` by default and some other bad choices. Most Linux DEs, following the quantitative mass had assigned Windows' `Alt+Shift`, but of course you could change it to (almost) anything you wanted. Since Windows 8, Microsoft overhauled the language switching widget and introduced, along with their old shortcut, `Win+Space` too. Since then, I think, some Linux DE's have followed.

The last hindrance was configuring `Win+Space` on Linux. It was not supported out of the box by the X window system utilities, and I did not want to mess with anything else or their endless manuals. Thankfully, I found [this](https://github.com/ierton/xkb-switch) awesome utility on the ArchWiki, and have been content ever since!

## Autocorrect and prediction

Another grievance of mine is the fact that there is still no mainstream auto-correct / prediction software for language input on desktop systems. SwiftKey is awesome on mobile, why not something similar for Skype et al instant messaging applications?

I wonder if those who thought of it, tried it and it didn't work, but sometimes you have to type really quickly, and do not care about the mistakes. Maybe next-word prediction is too much, I do not use it on my mobile either.
