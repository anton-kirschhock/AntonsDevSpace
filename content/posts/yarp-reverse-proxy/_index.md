---
title: YARP - The perfect reverse proxy?
description: Can it be? A perfect reverse proxy? Lets see!
date: 2024-11-10T18:08:47.762Z
preview: ""
draft: true
tags:
  - .Net
  - dotnet
  - C#
  - yarp
  - reverse proxy
  - proxy
  - nginx
  - Microsoft
  - Azure
categories: []
slug: yarp-reverse-proxy
keywords:
  - Yarp
  - C#
  - Proxy
  - CSS
---

## The situation

Let's firstly see the what the current situation is:
Assume we have two (frontend) apps that are hosted under the same domain, let's call it `mydomain.app`.
App one can be found under - let's say `mydomain.app/app1`, and app two can be found at `mydomain.app/app2`.
Lastly, if you don't type in any other valid path, it should redirect to app1.

Also both apps use Supabase and it's authentication provider - which is awesome!

In some cases you could consider frontend federation and just create a microfrontend, but there could be two counter-arguments:

- the apps don't have anything to do with eachother
- you don't have the capacity to maintain a complex architecture (e.g. private projects)

So, you grab the best reverse proxy off the shelf, like Nginx - and slap a configuration and whahm - a reverse proxy.

All was good until, I started adding social logins (Facebook, Google,...) to the Supabase auth, which made the cookies rather large...

## Then the trouble came...

Everything was fine until, I started implementing authentication which requires cookie authentication:
`NGINX 400 Bad Request: Request Header Or Cookie Too Large`
Thing is, that cookie was indeed large, containing the access token (Supabase). So reworking anything there wasn't an option.
But, after reading a bit more about how Nginx deals with reverse proxies and their buffer thing.
Naturally, I increased the buffer. But the error kept returning (e.g. other cookies that were added by various tools we use).

I knew about YARP since Microsoft published it back in 2021 and what they wanted to do with it but never got the possibility to use it in production.
But here it was! It's time to shine!

## The project

The project is realy simple blank Asp.Net App with a single `Program.cs`.
I've installed the following additional package
// Packages
// code

```cs

```
