---
author: David der Nederlanden
category:
  - webhosting
date: "2025-04-08T18:00:13+00:00"
tag:
  - experience
  - it
  - tech-recap
title: Converting this site from Wordpress to Hugo
url: /converting-wordpress-to-hugo/

---
I converted this site from Wordpress to Hugo with [wp2hugo](https://github.com/ashishb/wp2hugo) to get me started.

Reason behind this is that I really liked writing the blog in Markdown when I wrote a post for [AlmaLinux](https://almalinux.org/blog/2024-06-05-how-elevate-supports-business-needs/), besides that it also gives a great showcase for your abilities in working with Git and code on its own.

One of my goals was to maintain my search engine rankings by keeping the old pages at the same location, which it handled nicely.

To deploy the site to my webserver I currently use a simple pipeline on Github Actions which delivers me Artifacts, that I upload manually as of now.
I don't want to expose my webserver to Github's public runners and also a runner in my own network is something I don't like.
I'd much rather pull the Artifacts once in a while, something I will write a [script](https://github.com/randommen96/hugo-artifact-deploy) for in the future.

The [site source](https://github.com/randommen96/itty.nl) is made opensource and available on Github.

The fonts in my Hugo site were preloaded from Google's CDN, while they offer good services I wanted to avoid this dependency and used the [following guide](https://rednafi.com/misc/self_hosted_google_fonts_in_hugo/) to load the fonts from my own server.

It resulted in a nice [pagespeed](https://pagespeed.web.dev/analysis?url=https%3A%2F%2Fitty.nl%2F) upgrade! Currently it scores 100% in all tests.
