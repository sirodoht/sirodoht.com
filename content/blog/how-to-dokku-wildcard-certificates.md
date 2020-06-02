+++
title = "How to: dokku wildcard certificates"
date = 2020-05-31
template = "post.html"
+++

Everybody knows that [dokku](https://github.com/dokku/dokku) is the best thing ever when it comes to deploying web applications. Unfortunately, though, the best thing's Let's Encrypt plugin [dokku-letsencrypt](https://github.com/dokku/dokku-letsencrypt) does not support wildcard certificates.

This is how to succeed when faced with such challenge.

## dokku certs inner workings

Dokku stores everything around the deployment of an app in a aptly named directory inside `/home/dokku`. It also stores the certificates there, which are referenced from the app's nginx.conf.

An app's nginx.conf is customizable via the sigil template dokku uses.

Assuming we get a wildcard certificate, one way to install it would be to copy the cert files there and let the templated nginx config find it. This course of action would also require changing the `DOKKU_PROXY_PORT_MAP` and `DOKKU_PROXY_SSL_PORT` app environment variables to include the 443 port mapping so that the template understands that certificates exist and accepts requests at 443.

But there is a better way, by using the `dokku certs` command.

## Getting the wildcard cert

First we need to get our wildcard cert manually. [certbot](https://certbot.eff.org/) supports wildcard certficates with this command:

```
certbot certonly --manual
```

When asked for the domain, enter both the bare root domain and the wildcard one. I.e. `example.com, *.example.com`. Dokku's wish is to have one cert/key pair per app and we must respect it.

The command asks for both DNS and HTTP challenges. TXT record on a subdomain and a 88-character string served on a `/.well-known/acme-challenge` path.

After following all the steps methodically, it generates the cert and the private key at: `/etc/letsencrypt/live/<you-domain>/fullchain.pem`.

## Installing the cert into dokku

[Dokku states](http://dokku.viewdocs.io/dokku~v0.20.4/configuration/ssl/#certificate-setting) it is intelligent enough to understand which is which even when they are not named `server.key` and `server.crt`. Yet I still renamed them — not that I don't trust software. Then tar'ed them as per dokku's desire with:

```sh
tar cvf certs.tar server.key server.crt
```

Finally, the actual installation process, which was much less complicated than expected:

```sh
dokku certs:add mataroa < certs.tar
```

And that's it. [mataroa.blog](https://mataroa.blog/) was wildcardly certificated.

## Renewal

Let's Encrypt certificates are valid for 3 months, at which point a simple `certbot renew` should suffice, as long as the challenges continue to be valid. Cron is probably the way to go here.
