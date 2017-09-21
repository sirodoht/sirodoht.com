---
layout: post
title: "Coming from Node.js: Ruby on Rails and Django"
date: 2017-08-22 17:27:32
categories: web
---

For almost three years now I have been working with Node.js, along with the rest of the gang, Express, Mongo, Angular and React.

I had never worked with Ruby on Rails, Django or any other batteries-included web frameworks, but I had been always hearing that the pros outweigh the cons in many cases, and especially in a CRUD web application. CRUDs did play a major role on the Node.js applications I was working on, so I decided to try Rails and Django to see if indeed and particularly how much better they are.

I decided to play with those two, since they were the most famous and appealing.

## Ruby on Rails

Ruby on Rails was created by [DHH](https://twitter.com/dhh), the CTO of Basecamp (then 37signals) who extracted Rails after working with Ruby on 37signals.

One of the most surprising features of Rails is the underlying philosophy of [Convention over Configuration](http://rubyonrails.org/doctrine/#convention-over-configuration).

For example, if you have a controller method named `new`, then if Rails finds an HTML template named `new.erb.html` it will automatically render it! It is the convention that if there is a template with the same name as the method, in a directory with the controller name, it will be rendered.

That, at first, seemed kind of over the top and scary, but I have grown to really liking it. It saves time and lines while not getting in the way.

The next thing that amazed me was the way you can have a model with REST endpoints.

Assuming we have a model, `Post`, you can just say `resources :posts` in your routes file and you get all REST endpoints, just like that, one line.

In order to do this using Node.js and Express quite a few hours have to be spent. Additionally to the hours you need to setup the whole project, file architecture, ORM, routing, testing, etc.

The last, of the top 3 things that impressed me is how Rails passes view parameters from the controller methods to the template. They just pass every variable defined! You don’t have to create an object with the ones you want, Rails sends everything for you, and you can use the one you want.

This makes so much sense. If you defined a variable in the controller, 90% you are going to use it in the template; there is no need to tweak that object all the time.

Also, separation of development, production and testing environments is done by default, which is neat.

The things I didn’t like include the quite complex templating language, especially for forms (more details below) and the fact that Rails is very keen on breaking changes. This also makes googling very annoying because you don’t know if that specific StackOverflow answer works for 5.X version.

## Django

Django has a similar birth, open sourced after being developed for the website of the Lawrence Journal-World newspaper. Its creators are Adrian Holovaty and Simon Willison.

One of Django’s core philosophy, that inherits from Python, is [Explicit is better than implicit](https://docs.djangoproject.com/en/1.11/misc/design-philosophies/#explicit-is-better-than-implicit), which actually is the exact opposite of Rails’ one with convention over configuration. Despite all that, one of the things that I like about Django is how much fewer files and directories I had in my project than in the case of Rails.

Always using REST models, separate controllers, various namespacing techniques and other architecture decisions make Rails grow a large number of files even for a small project. Of course, those files are usually much smaller than the Django ones, but I have come to prefer to have, e.g., all my forms in one 100-lines `forms.py` file instead of 10 separate files, with 10 lines each, inside a `forms` directory.

Django follows this philosophy. One `models.py` file, one `forms.py`, one `views.py` file; when a project grows large enough you can transition to multiple files.

Since I talked about `views.py`, now is a good time to talk about naming. Django calls its controllers `views` and its views `templates` (and its models `models`). In case you were wondering, its “controller” is the framework itself.

One of the major features of Django is its apps. It is a way to divide a web application into parts, and it’s not optional. This frustrated me in the beginning; had I wanted to break my app into parts I would go microservices which are more hip.

Thankfully, I scraped that incarnation and followed [Stavros](https://www.stavros.io/)’ advice (he’s a Django oldtimer) to have a `main` app and throw all business logic inside there.

Of the things I liked the most in Django is the way it handles forms. Rails does forms on the templates, and the `erb` templating language wasn’t the easiest to work with. Various confusing tags like `label` and `label_tag`, along with too much logic made it the most frustrating thing using Rails.

Django’s handling was *almost* like a breeze. You can have a `ModelForm` which automatically creates all input fields for a model, and then you can override the things you want. Some were harder to find than others, but once you understand the philosophy and the terms (`Field`, `Widget`, etc) it becomes pretty easy.

Another nice thing is that Django has an integrated admin interface in the `/admin` endpoint of your application. It is pretty useful, I missed it in Rails.

While, as I said, I didn’t like the large number of files and directories in Rails, there were some things that I also missed in Django.

Firstly, Django refuses to serve static files in production. It does not have a suitable module for doing that, and you either need to install a separate package, `whitenoise`, or upload and serve static assets directly from a CDN. In my use case though, with dokku (and with Heroku) a module to do this would be useful.

This, along with with the fact that Django doesn’t handle by default stuff like separation of development/production/testing environments and database url parsing made the deployment a little bit more cumbersome than Rails and Node.js, but still pretty easy with dokku.

To conclude with Django, the only thing I’m concerned with is REST endpoints. There is Django REST framework but I have not tried it, and I’ve heard it doesn’t have the the most straightforward documentation.

All in all, I liked Rails and Django and I’m very interested in working more with them. Finally, despite risking oversimplification of any project’s requirements I’d say that I would choose Django for CRUDs, and Rails for REST APIs. The shortcuts they provide, respectively for those use cases, are awesome.

---

*This article was also published on [HackerNoon](https://hackernoon.com/coming-from-node-js-ruby-on-rails-and-django-6c6c9390e31a).*
