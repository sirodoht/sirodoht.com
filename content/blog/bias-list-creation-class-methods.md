+++
title = "The bias of list creation in the form of class methods"
date = 2015-09-10
template = "post.html"
+++

It's interesting how human biases carry on to writing code and how they evolve in this transition.

Recently, at my job, we wanted to create a metrics endpoint. In order to do this task, we copy-pasted the controller implementation from the users-list endpoint to the metrics one.

Of course, after using such a technique we had to comb through the users-list code and check for possible edits or removal of parts of code that are not useful for the metrics functionality.

However, there is a psychological phenomenon that caused us hours tracking a bug! In this phenomenon, given a list and being asked to divide, depending on your way of operation, different sets of lists will be created, even with the same comparing function.

To illustrate this, let us assume you have a list and someone asks you to *create a new list* with the most important items.

You have two ways of operating:

* Create an empty new list and check out every item of the original list. If it is important, copy it into the new list.

* Duplicate the original list. Check out every item of the new list, and if it not important remove it.

If you pick the first way, you will have a shorter *important* list than the second way. The reason is that on those items that you are torn whether they are important, you will act with the default action. In the first case the default is not copying them to the new list. In the second case the default action is not removing them from the new list.

A way which wouldn't cause a bias, is one with no default action. In this case it would be to create two new lists. One is the unimportant items and the other the important ones. Subsequently, there is no default aka *easier* act; either you write the item in the first list or in the second.

This phenomenon applies to the way we wrote the new endpoint controller. Essentially, the *list* was the list of methods in the controllers and the way we operated was the second one, using duplication.

As a result, the new list of methods was larger. The default action of not removing code/methods that *might be useful later* was followed. One of them was to keep the pagination functionality enabled. However, the dummy data set in our local installation was smaller than the production one. As a result, it wasn't possible to get new metrics summaries in the production after a few, because the request was actually only for page 1. We had to dive through the stack, front, back layers and check database durability ([sorry Mongo](http://www.sarahmei.com/blog/2013/11/11/why-you-should-never-use-mongodb/)) in order to locate this extra method at the end.
