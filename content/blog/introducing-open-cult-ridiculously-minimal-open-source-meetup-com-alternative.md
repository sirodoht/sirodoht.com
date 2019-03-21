+++
title = "Introducing Open Cult: Ridiculously minimal open source meetup.com alternative"
date = 2018-03-05
template = "post.html"
+++

After the latest redesign meetup.com feels a bit clunky; somehow less usable. I really like the idea of Meetup though, so I thought to take a stab at creating an alternative. It will probably not meet most people’s aesthetic principles, as it is a bit eccentric, but do see for yourself!

Enter [Open Cult](https://opencult.com/), a ridiculously minimal, [open source](https://github.com/sirodoht/opencult.com), Meetup.com alternative.

The ideas behind [opencult.com](https://opencult.com/) are based on minimalism, speed, simplicity and a text-only approach.

Comparing with Meetup, instead of meetup groups, we have cults, hence the name. The rest of the core functionality is the same. You can join a cult; RSVP at an event; leave a cult or un-RSVP.

The differences are that you receive exactly one email per event announcement. You receive no confirmation email once you RSVPed in contrast to meetup.com; you know you will go, no reason to archive one more email.

The design is inspired by YC Hacker News. After using HN for many years I’ve come to appreciate its spartan approach. It’s an unpopular opinion (and probably an overreaction for some web design trends) but in the case of meetups, I just want the content; no wide margins, no large icons, no images. The content is the event title and description, time & date, location, one email reminder when the event is announced and maybe a few comments to review the event or clarify details.


Open Cult loads pretty fast. Here is a speed test [from Stockholm/Europe](https://tools.pingdom.com/#!/eQDknu/https://opencult.com/) and here is [one from NYC/US](https://tools.pingdom.com/#!/dCARVS/https://opencult.com/). The frontend is currently less than 20KB and everything is served with 2 HTTP/2 requests.

As far as mobile responsiveness, a major pain point for me with meetup.com, Open Cult performs marvelously. Apart from the Lilliputian size, its barebones HTML elements will use the OS native date and time pickers, making new event submissions on mobile a breeze.

Finally, Open Cult is built on Python and Django, and [lives on GitHub](https://github.com/sirodoht/opencult.com) as an open source project. Please feel free to contribute, as one pair of eyeballs is not nearly enough for all bugs. Also, consider proposing and discussing new features and UX-first design improvements. Check some ideas [here](https://github.com/sirodoht/opencult.com/issues).
