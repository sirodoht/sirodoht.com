+++
title = "Building mataroa.blog"
date = 2020-06-09
template = "post.html"
+++

This article is about building [mataroa.blog](https://mataroa.blog/), a minimal blogging platform with export as a first-class feature, built with Python and Django.

According to git, I started the [mataroa](https://github.com/sirodoht/mataroa) [repo](https://sr.ht/~sirodoht/mataroa/) on May 27th, 2020, 20:37 UTC, just a few hours after my friend [Stavros](https://www.stavros.io/) sent me the link of [Bear Blog](https://bearblog.dev/). We thought it was genius —Bear Blog— and I decided to make something similar, mainly because I would enjoy building it. [1]

## RSS

After submitting to HN, the first comment I got was that the lack of RSS was a dealbreaker. Heartbreak. Quickly rushed to implement it. It took 47 minutes for the implementation, testing, and UI polishing.

The reason for this speed lies in Django having an excellent built-in "syndication-feed-generating framework". It's very simple to acquire basic functionality:

```py
# main/feeds.py
from django.contrib.syndication.views import Feed
from django.http import Http404

from main import models


class RSSBlogFeed(Feed):
    title = "Blog"
    link = ""
    description = "Cool blog resides here"

    def items(self):
        return models.Post.objects.filter().order_by("-created_at")

    def item_title(self, item):
        return item.title

    def item_description(self, item):
        return item.body
```

```py
# main/urls.py
urlpatterns += [
    path("rss/", feeds.RSSBlogFeed(), name="rss_feed"),
]
```

But, that didn't work for mataroa as it returns all (across all blogs) posts.
We wanted to get only those that were from the subdomain requested.

After looking into the extremely readable Django source code of the `Feed` class, the following addition was made in the `RSSBlogFeed` class.

```py
def __call__(self, request, *args, **kwargs):
    # check that user requests a subdomain (non-bare domain) site
    if not hasattr(request, "subdomain"):
        raise Http404()
    user = models.User.objects.get(username=request.subdomain)
    self.title = user.blog_title
    self.subdomain = request.subdomain
    return super(RSSBlogFeed, self).__call__(request, *args, **kwargs)
```

We want the request object, because `subdomain` resides in there. Based on that, we have the user (which means we have the blog title too) and finally we can define the queryset:

```py   
def items(self):
    return models.Post.objects.filter(owner__username=self.subdomain).order_by(
        "-created_at"
    )
```

## Models

These are mataroa's Django models.

```py
# main/models.py
import markdown
from django.conf import settings
from django.contrib.auth.models import AbstractUser
from django.db import models
from django.urls import reverse


class User(AbstractUser):
    about = models.TextField(blank=True, null=True)
    blog_title = models.CharField(max_length=500)

    def get_absolute_url(self):
        return reverse("user_detail", kwargs={"pk": self.pk})

    def __str__(self):
        return self.username


class Post(models.Model):
    title = models.CharField(max_length=300)
    slug = models.CharField(max_length=300)
    body = models.TextField(blank=True, null=True)
    owner = models.ForeignKey(User, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        ordering = ["-created_at"]
        unique_together = [["slug", "owner"]]

    @property
    def as_markdown(self):
        return markdown.markdown(
            self.body,
            extensions=[
                "markdown.extensions.fenced_code",
                "markdown.extensions.tables",
            ],
        )

    def get_absolute_url(self):
        path = reverse("post_detail", kwargs={"slug": self.slug})
        return f"//{self.owner.username}.{settings.CANONICAL_HOST}{path}"

    def __str__(self):
        return self.title
```

2 models, 46 lines.

The first idea towards simplicity here was that there's no need for Blog to be a separate model. It was a given that the User model would be overriden, and having multiple blogs under one user would be out of scope. Thus, why not just add `blog_title` in the User model.

Another matter of thought was how to handle `get_absolute_url`. Thankfully, we have all parts needed there. We just need to assemble them by using this f-string — of which versions come up numerous times across the app.

```py
f"//{self.owner.username}.{settings.CANONICAL_HOST}{path}"
```

## Subdomain middleware

This part is the core of how we handle subdomains using the same app.

```py
# main/middleware.py
def subdomain_middleware(get_response):
    def middleware(request):
        host = request.META.get("HTTP_HOST")
        if host and len(host.split(".")) == 3:
            request.subdomain = host.split(".")[0]

        response = get_response(request)
        return response

    return middleware
```

```py
# settings.py
MIDDLEWARE = [
    ...
    "main.middleware.subdomain_middleware",
]
```

A simple function-based Django middleware that checks the HTTP `Host` header. If there are 3 dots, it means we have something like `subdomain.mataroa.blog`. If so, we stick it in `request.subdomain` and have it there for the rest of the trip!

For example, (and most important case) when `/` is requested, we want to know whether we should serve the landing or a blog:

```sh
# main/views.py

# check if request has subdomain attr
if hasattr(request, "subdomain"):

    # check if this subdomain is a blog that exists
    if models.User.objects.filter(username=request.subdomain).exists():
        ...  # render blog index template
    else:
        # blog does not exist, redirect to landing
        return redirect("//" + settings.CANONICAL_HOST + reverse("index"))
```

## Interest form

For the premium plan interest form, we sent an email to the admin letting them know of the submission. A conscious decision to avoid a new model for subscribers was made here.

```py
# main/forms.py
class InterestForm(forms.Form):
    email = forms.EmailField()

    def send_email(self):
        body = "There is a person interested in Mataroa premium!"
        body += f"\nThis is their email: {self.cleaned_data.get('email')}"
        body += "\n"
        body += "\nBest,"
        body += "\nPython"

        mail_admins("Interest form response", body)
```

Above is the form. I usually send the mail inside the view but the [Generic editing view](https://docs.djangoproject.com/en/3.0/ref/class-based-views/generic-editing/#formview) Django docs had this exact example of sending email from the form.

The view method below, only 9 lines, by exploiting the succinct marvel of Django generic views.

```py
# main/views.py
class InterestView(SuccessMessageMixin, FormView):
    form_class = forms.InterestForm
    template_name = "main/interest.html"
    success_url = reverse_lazy("index")
    success_message = "thank you for your interest! we'll be in touch :)"

    def form_valid(self, form):
        form.send_email()
        return super().form_valid(form)
```

## Disallowed usernames

Since usernames are subdomains, some of them had to be disallowed. I found a rather extensive list online and trimmed it down to 50. Some of the most notable are `api`, `admin`, `cdn`, `static`, `random`.

The implementation includes `form.add_error`, which I don't recall ever using in the past.

```py
# main/views.py
def form_valid(self, form):
    if helpers.is_disallowed(form.cleaned_data.get("username")):
        form.add_error("username", "This username is not available.")
        return self.render_to_response(self.get_context_data(form=form))
    return super().form_valid(form)
```

## Export to Zola

The feature that makes mataroa an un-platform is that it helps you get off it. It minimizes vendor lock-in by enabling the blog owner, with a single click, to be able to setup a static website with all their posts.

Exporting to Zola was the first feature I wrote because I was too afraid of its implementation. Turns out it was easier than expected. The full view method is around 40 lines.

```py
# main/views.py

# get all posts and add them into export_posts encoded
posts = models.Post.objects.all()
export_posts = []
for p in posts:
    title = p.title.replace(":", "-") + ".md"  # no colons in filenames
    export_posts.append((title, io.BytesIO(p.body.encode())))

# create zip archive in memory
export_name = "export-" + str(uuid.uuid4())[:8]
zip_buffer = io.BytesIO()
with zipfile.ZipFile(
    zip_buffer, "a", zipfile.ZIP_DEFLATED, False
) as export_archive:
    # the directory structure is based on the paths of the name given to writestr
    export_archive.writestr(export_name + "/config.toml", zola_config)
    export_archive.writestr(export_name + "/static/style.css", zola_styles)
    export_archive.writestr(export_name + "/templates/index.html", zola_index)
    export_archive.writestr(export_name + "/templates/post.html", zola_post)
    for file_name, data in export_posts:
        export_archive.writestr(
            export_name + "/content/" + file_name, data.getvalue()
        )

# respond and make the file directly downloadable
response = HttpResponse(zip_buffer.getvalue(), content_type="application/zip")
response["Content-Disposition"] = f"attachment; filename={export_name}.zip"
return response
```

The `zola_` prefixed variables are strings (not list of strings) of those files (stored in the code) read like this:

```py
# main/views.py
with open("./zola_export_base/config.toml", "r") as zola_config_file:
    zola_config = (
        zola_config_file.read()
        .replace("example.com", f"{request.user.username}.mataroa.blog")
        .replace("Example blog title", f"{request.user.username} blog")
    )
```

## Permissions

For permission checking I considered the native Django solution but it was an overkill. Except for `LoginRequiredMixin` and `user.is_authenticated` the following lines are the core of every permission check:

```py
if request.user.username != request.subdomain:
    raise PermissionDenied()
```

Interesting bit is the preference of raising a `PermissionDenied` exception to the return of `HttpResponseForbidden`. The latter resulted in an empty page while the former returned a default text of black letters `403 Forbidden`.

## Post creation

On the post creation page we hide the slug field. It declutters the form a bit and lets you focus more on the actual writing than to find the best SEO-wise slug.

Thus, we generate the slug using yet another brilliant battery of Django: `django.utils.text.slugify`. Also, a check in case another identical slug (in the same blog) exists. This solution might be unideal but the number of infinite loops I have created in past projects solving this with `while` (countless) in contrast to the times one uuid suffix was not enough (zero) is a good reason.

We also inject the post owner, preventing any hijacking of users creating posts in others' blogs.

```py
# main/views.py
def form_valid(self, form):
    # commit=False to decrease SQL writes by one
    self.object = form.save(commit=False)

    # slugification
    self.object.slug = slugify(self.object.title)
    if models.Post.objects.filter(
        owner=self.request.user, slug=self.object.slug
    ).exists():
        self.object.slug += "-" + str(uuid.uuid4())[:8]
    
    self.object.owner = self.request.user
    self.object.save()  # sql write happens here
    return HttpResponseRedirect(self.get_success_url())
```

## Epilogue

It was a really enjoyable project as a whole and the above bits the most amusing to figure out. Undoubtedly, their elegance can be futher improved and I am looking forward to learning how.

As the project grows the above bits will change. The commit hash the above snippets of code are taken from is `48af918dd84a9a579db6dcc95461669e4cbf8d08`.

You can find the full code at [github.com/sirodoht/mataroa](https://github.com/sirodoht/mataroa) or [sr.ht/~sirodoht/mataroa/](https://sr.ht/~sirodoht/mataroa/). Or browse the above commit hash at [github](https://github.com/sirodoht/mataroa/tree/48af918dd84a9a579db6dcc95461669e4cbf8d08) and [srht](https://git.sr.ht/~sirodoht/mataroa/tree/48af918dd84a9a579db6dcc95461669e4cbf8d08).

\---

[1] Stavros' inspiration led him to [Quick Site](https://quicksite.stavros.io/).  
