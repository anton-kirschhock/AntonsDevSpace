---
title: Building a Blog & Profile Site - How Hard Can It Be?
description: Building a blog site can sometimes be challenging! Let's dive into my process of building a profile and blog site!
date: 2024-09-10T08:26:12.907Z
preview: ""
draft: false
tags:
  - Blog site
  - Blogging
  - Hugo
  - Portfolio
  - Journey
categories:
  - Blogging
slug: building-blog-site
cover:
  image: "building-blog.png"
  caption: "A person building a blog site - this is an AI-generated image"
ShowToc: true
---

# Building a Blog & Profile Site - How Hard Can It Be? (1/2)

Well, if you found yourself in the same pickle as I have _Let's build a blog site!_, you might have found yourself in the same shoes as I have:
What technology should I use to do so... How should it look... Jeez, this is not easy!

Everything started about 4-5 years ago when I already wanted to do this but never got to finish it (the famous developer starting a project and never finishing it story):

## Attempt 1: Let's Build It from Scratch

Being the young motivated developer I was 4 years ago, I wanted to use Angular and a Headless CMS (powered by [OrchardCMS](https://orchardcore.net/)) backing it.
To be frank, it never left the drawing board - I sketched the whole architecture, defined all models. Heck, I even started the Angular project and scaffolded the CMS.
Then one day, the project got stale, as every project ever...

## Attempt 2: This Should Be Done More Easily

Fast forward 2 years - I did some research using TinaCMS for a work-related project and discovered the ease of use.
I researched [TinaCMS](https://tina.io/) together with NextJS for that work-related project and even tried to work in my spare time to build my portfolio.
I don't know why I never went further with this because TinaCMS does look nice and has some nice features.
But more about TinaCMS in part 2...

## Attempt 3: Okay, It Is Time to Start Blogging!

In 2024, in my spare time, I started writing down stuff I noticed while working on Skillerjobs. Mainly things where I did not find some good blog or tutorial about.
I wrote those things in my personal Notion collection and kept extending them while discovering my blog-writing style.
And what did I notice: I liked it.

I even continued to build demo projects, which will be part of the articles (subscribe to see those projects in action!!!!!).

Okay, I needed a site, with CMS tooling, easy to build, hostable in Azure but still cheap, written in .Net... Let me introduce [PiranhaCMS](https://piranhacms.org/)!

I loved every aspect of it:

- Had a great interface for managing content
- Extendability
- Written in .Net 8
- Creating custom blocks

And so I went ahead building my Portfolio / Blog site using Piranha.

BUT I wanted something new, not the default Bootstrap or Tailwind CSS site so I found something cool: [Bulma](https://bulma.io/).

Bulma is everything I was searching for in a simple CSS + HTML component library. It even looked very nice!
// Image of Bulma's site

So I started tinkering and built a portfolio site with it
// IMAGE OF THE SITE

I even got it up and running with a VM in Azure but realized the biggest issue for mankind: Money.
The VM would have cost 20 Euros per month - I needed a cheaper solution, so again ditched a project (while being production ready) and went back to the drawing board.

## Attempt 4: This Time, It Will Work!

I needed something simpler, for the time being.
I initially thought back to how TinaCMS worked: it used markdown files with YAML annotations and used GitHub (or your favorite GIT-based repository provider) as a database, thus reducing the "Cost" (both financially and performance-wise) needed to host a blog site.
Yet, I wanted to have all the nice things of a full-hosted CMS:

- Support for media management
- Tag management
- Category management
- SEO options
- Ease of use
- ...

Then one day I stumbled over HUGO. 'What is that beast HUGO?'. In summary: it was something I was looking for!
Why you might ask, you can also do SSG with Angular?
Yep, you are absolutely right concerning that, but it would become a little bit more complex.

Let me just dive into it a bit and you might understand.

Hugo is an SSG (Static Site Generation) CLI tool built using Go with markdown as your canvas for content writing.
Ideal if you are familiar with markdown (and like in my case, like to write markdown) powered by the known Go Templating engine.

If you really feel up for the challenge (and know Go), you can even write modules for it to control the process of building the content!
And it is really fast, has great documentation, and even has support to deploy to an Azure Storage Account! Incredible!

In part 2 I will dive a bit deeper into the setup, the tools that I used, and dive a bit deeper into how theming works.
Stay tuned and don't forget to C# too!
