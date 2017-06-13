---
layout: post
title: "33 Questions and numeral systems"
date: 2014-06-27 16:27:32
categories: fun, puzzle
---

[33 Questions](https://github.com/MarkDunne/33-questions) is a GitHub repository with the purpose of coming up with exactly 33 polar questions (yes or no questions) which will be able to identify every person living on Earth.

## How they plan to do it

### Short Answer
Every answer to those questions is mapped to either 0 or 1 (depending on whether it's a yes or a no). Answering all 33 means we have 33 bits, which form a binary number, which will be unique for every alive person.

### Long Answer

#### Binary
Firstly, we need to understand binary numbers. We, everyday people, think and operate on a base 10 (decimal) numeral system. That means, we have 10 unique digits to identify all numbers, from -∞ to +∞. 0, 1, 2, 3, 4, 5, 6, 7, 8, 9. Every number we write is composed only by these 10 symbols. We could have other systems, but history decided that base 10 is the best choice since (a) we have 10 fingers which we can use to count and (b) it is a balanced number, meaning (i) not there are not many digits to learn by heart and (ii) not many digits needed to represent big numbers.

We will explore (i) and (ii) later on. For now let's focus on how numeral systems work.

#### Decimal
To understand and learn how to count on different systems we need to understand how we count on our base 10 system. We learn this skill early on our lives and we do not bother understanding it internally (we can't at that time anyhow), so we just learn it intuitively. This is good for learning it, but not for understanding it algorithmically, with a cold logic.

Now, let's count!

         0
         1
         2
         3
         4
         5
         6
         7
         8
         9
        10
        11
        ..
        19
        20
        21
        22
        ..
        98
        99
       100
       101
       102
       ...
       998
       999
      1000

Notice the way I put each number after another: the units on the rightmost "column", decades on the second from the right, the hundreds on the third from the right, and so on. Now pay attention to this: we start counting from 1, then 2, continuing 3, 4, ..., until 9. That is where we finish with our digits, there are no more, and when this happens we reset our counter and add 1 on the left of the number, which means we already have counted 1 decade and we continue from there. So 11 means we have one decade, a 10 plus 1.

      10
    +  1
    ----
      11

We could write it like this:

      10
    + 01
    ----
      11

Here decades and units seem more clearly separated and it is noticeable the fact that at the beginning we have 0 decades, which we do not represent explicitly. Every time we max a column we reset it and add 1 on the left of it. When we count from 0 to 9 we max the column of units, because we have reached 9 which is the last digit. Then we reset it and add 1 on the left, which is incrementing the column of decades since we already counted one. The same thing happens when we count from 120 to 129. The next number is 130, which is resetting units (0 at the rightmost column) and adding 1 to the next on the left (2 becomes 3).

A nice visualization is with old kilometer or miles counters. Each "column" was represented by a thin cylinder which had all digits on its circular edge. When we would travel the counting would begin and the cylinders would spin, and when there was a full circle and it would reach 0, the next from the left cylinder would also be incremented by 1. At the beginning it was like this, all zeros, and it would develop as such:

     00000
     00001
     00002
       ...
     00010
     00011
       ...
     00019
     00020
     00021
     00022
       ...
     00098
     00099
     00100
     00101
     00102
       ...
     00998
     00999
     01000


#### Let's count binary!

Binary (base 2) system has two digits, 0 and 1. We will count binary using the way we count decimal with a slight difference: we will not reset when we reach 9 but when we reach the last digit of binary, which is 1.

    Base   10       2
           0        000000
           1        000001

Now we have to reset units since we have reached the last digit of our system.

    Base   10       2
           0        000000
           1        000001
           2        000010

Units were reset and the next left column was incremented by 1. Next:

    Base   10       2
           0        000000
           1        000001
           2        000010
           3        000011
           4        000100
           5        000101
           6        000110
           7        000111
           8        001000
           9        001001
          10        001010
          11        001011

Notice that it goes exactly as we said: when a column reaches max it resets and the next from the left is incremented by 1.

In base 8 we would count as such:

    Base   10       8
           0        000000
           1        000001
           2        000002
           3        000003
           4        000004
           5        000005
           6        000006
           7        000007
           8        000010
           9        000011
          10        000012
          11        000013


### 33 Questions
Now, to come back to the [33 Questions](https://github.com/MarkDunne/33-questions).

In order to identify every human on Earth we need to assign something unique to each one of them. The simplest is to assign a number. We need [~7 billions](http://www.wolframalpha.com/input/?i=world+population+2014) of them. In binary, in order to represent the maximum number we need 33 binary digits. With 32 we can represent until 4 294 967 296 numbers/humans, which is a little over 4 billion. That is not enough, so we go to 33 digits. So, by having 33 polar questions we get 33 answers for each person. We map "no" to 0 and "yes" to 1. This gives us a series of 0s and 1s, 33 of them, which we treat as a binary number. Then, we can convert this number from base 2 to base 10. The goal is from every person to have a different number, which means that the questions must be picked in such a way that no one will answer all 33 questions with the same way. The purpose of this GitHub repository is to find those questions, a very difficult task!



## Complementary section

### Why units, decades and hundreds?
The reason that we have units, decades, hundreds, etc, in our decimal system is because these are powers of 10 and we have a base 10 system. Example for 2482.

     2        4        8        2
     2x10^3   4x10^2   8x10^1   2x10^0

The columns are 10^3, 10^2, 10^1 and 10^0

Let's suppose we have a base 8 system. This means that we have 8 digits: 0, 1, 2, 3, 4, 5, 6, 7. There the columns would be powers of 8. That is 1, 8, 64, 512, and so on. So for representing 10 we would need one from the 8s and 2 from the units, which is: 12.

So 12 in base 8 is our decimal 10.

10 in base 8 means that we have 1 from the 8s plus 0 from the units, which is our decimal base 8.


### Why 10?
I said that 10 is a balanced number for a numeral system. The balance here is between (i) the number of different digits you need to know to make up larger numbers and (ii) the number of digits needed to represent large numbers.
In our case you need to learn 10 different digits, and then you can represent every number there is. In binary system you need to learn only 2 digits to represent every number. The drawback here is that in binary you need many digits to represent large numbers. As we saw, in order to represent the number of 4 billions in binary you need 32 digits while in decimal you need 10 digits (4 + 9 zeros). The Babylonias had a system of base 64! That means they would need to learn 64 different symbols which would be isomorphically (one by one) mapped to the 64 digits of the numeral system. What is interesting, though, is that it is considered by [some](https://www.youtube.com/watch?v=U6xJfP7-HCc) that we should have gone with a base 12 system [Duodecimal system](https://en.wikipedia.org/wiki/Duodecimal), because 12 is a [superior highly composite number](https://en.wikipedia.org/wiki/Superior_highly_composite_number) meaning that it has a higher number of divisors scaled relative to the number itself than all other numbers. Also, it is noteworthy the fact that the English language has distinct words ([morphemes](https://en.wikipedia.org/wiki/Morpheme)) for the extra digits of a base 12 system, that is, for eleven and twelve. We don't call them one-teen and two-teen. but we say thir-teen, four-teen, etc.
