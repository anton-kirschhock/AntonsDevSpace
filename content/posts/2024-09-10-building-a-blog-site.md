---
title: Building a blog & profile site - How hard can it be?
description: Building a Blog site sometimes can be challenging! Let's dive into my process of building a profile and blog site!
date: 2024-09-10T08:26:12.907Z
preview: ""
draft: true
tags:
  - Blog site
  - Blogging
  - Hugo
  - Portfolio
  - Journey
categories:
  - Blogging
slug: building-blog-site
---

# Building a blog & profile site - How hard can it be?

Well, if you found your self in the same pickle as I have _Lets build a blog site!_, you might have found your self in the same shoe as I have:
What technology should I use to do so... How should it look like... Djees this is not easy!

Everything started about 4-5 years ago, where I already wanted to do this but never got to finish it (the famous developer starting a project and never ending it story):

## Attempt 1: Let's build it from scratch

Being that young motivated developer I was 4 years ago, I wanted to use Angular and a Headless CMS (powered by [OrchardCMS](https://orchardcore.net/)) backing it.
To be frankly, it never left the drawing board - I sketched the whole architecture, defined all models. Heck, I even started the angular project and scaffolded the CMS.
Then one day, the project got stale, as every project ever...

## Attempt 2: This should be done more easier

Fast forward, 2 years - I did some research using TinaCMS for a work related project and discovered the ease of use to use it.
I researched [TinaCMS](https://tina.io/) together with NextJS for that work related project and even tried to work in my spare time to build my portfolio.
I don't know why I never went further with this, cause Tina CMS does look nice and has some nice features.
But more about TinaCMS later...

## Attempt 3: Okay It is time to start blogging!

In 2024, in my spare time I started writing down stuff what I noticed while working on a project called Skillerjobs. Mainly things where I did not find some good blog or tutorial about.
I wrote those things in my personal Notion collection and kept extending them while discovering my blog-writing style.
And what did I notice: I liked it

I even continued to build demo projects, which will be part of the articles (subscribe to see those projects in action!!!!!)

Okay I needed a site, with a CMS tooling, easy to build, hostable in Azure but still cheap, written in .Net... Let me introduce [PiranhaCMS](https://piranhacms.org/)!

I loved every aspect of it:

- Had a great interface of managing content
- Extendability
- Written in .Net 8
- Creating custom blocks

And so I went ahead building my Portfolio / Blog site using Piranha.

BUT I wanted something new, not the default bootstrap or Tailwind css site so I found something cool: [Bulma](https://bulma.io/).

Bulma is everything I was searching for in a Simple CSS + HTML component library. It even looked very nice!
// Image of Bulma's site

So I started tinkering and build a portfolio site with it
// IMAGE OF THE SITE

I even got it up running with a VM in Azure but realized the biggest issue for mankind: Money.
The vm would have cost 20 Euro per month - I needed a cheaper solution, so again ditched a project (while being production ready) and went back to the drawing board.

## Attempt 4: This time, it will work!

I needed something more simple, for the time being.
I initially thought back of how TinaCMS worked: it used markdown files with yaml annotations and used GitHub (or your favorite GIT based repository provider) as a database, thus reducing the "Cost" (both financially as performance) needed to host a blog site.
Yet, I want to have all the nice things as a full-hosted CMS:

- Support for media management
- Tag management
- Category management
- SEO options
- ease of use
- ...

Then one day I stumbled over HUGO. 'What is that beast HUGO?'. In a Summary: it was something I was looking for!
Why you might ask, you can also do SSG with Angular?
Yep you are absolutely right conserning that, but it would become a little bit more complex.

Let me just dive into it a bit and you might understand.

Hugo is a SSG (Static Site Generation) CLI tool build using Go with markdown as your canvas for content writing.
Ideal if you are familiar with markdown (and like in my case, like to write markdown) powered by the known Go Templating engine.

If you realy feel up for the challenge (and know Go), you can even write modules for it to control the process of building the content!
