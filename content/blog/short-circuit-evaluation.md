+++
title = "Short-circuit evaluation"
date = 2014-06-29
template = "post.html"
+++

Short-circuit evaluation is something that as a junior programmer I did not read about but I encountered it in practice.

In C [1] you can do something like this:

```c
if (i++ < 10 && j++ < 20)
{
  // do some stuff
}
```

In this case if `i < 10` is false, the C compiler will not care to check `j < 20` since it has already decided that it will not enter the if-statement. This is because there is an AND - `&&` operator and since the first part was not true, there is no way for the whole to be true. The problem, in this case, is that the condition that won't be checked also includes a variable assignment. This means that you may expect it to run at least one time, but it won't, since C understands there is no point in wasting time to do this.

Of course, after you learn this you can use it to your own ends.

Python also supports short-circuit evaluation (notice the word *supports*; it is a feature!).

We have something like this:

```python
if large_number % i == 0 and is_prime(i):
    prime = True
```

We have a two-part condition. The first is a division. The second is a function call which calculates something with high complexity. If we first check the easy part (short time), we may not have to check the hard part (long time) because of short-circuit evaluation. Respectively, if we first check the hard part, we may not have to check the easy part **but** we will already have wasted some time.

Of course, that's not always the case. The likelihood of one of the parts evaluating more often than the other as true is important. However, this example is enough to demonstrate how we can use short-circuit evaluation in our favor.

```python
if large_number % i == 0:
    if is_prime(i):
        prime = True
```

If we didn't have short-circuit evaluation and we wanted to avoid the needless computation of `is_prime(i)`, we would have to do something like the code above.

<div class="notes-separator"></div>

**Notes**

[1] This is true in other languages as well.
