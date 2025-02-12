---
title: Specify the timeout while using OpenAI's .NET library
description: A quick post to showcase how to resolve slow chat completions without hitting the default timeout
date: 2025-02-12T12:00:00.907Z
preview: ""
draft: false
tags:
  - dotnet
  - C#
  - OpenAI
  - QuickPost
categories:
  - DotNet
slug: dotnet-openai-timeout
ShowToc: false
---

Ever had the issue that you hit the timeout of the OpenAI client and could not find any quick resolution?

Well, don't worry - Here you go!

```cs
// Used NuGet: Azure.AI.OpenAI@2.0.0
using OpenAI;
using OpenAI.Chat;
// ...
var config = sp.GetRequiredService<IOptions<AIConfiguration>>().Value;
var apiKey = config.ApiKey;
var client = new OpenAIClient(new(config.ApiKey), new OpenAIClientOptions
                {
                    NetworkTimeout = TimeSpan.FromMinutes(3) // Specify your timeout here
                });
```

That'll be it!
Don't forget to C#! 👋
