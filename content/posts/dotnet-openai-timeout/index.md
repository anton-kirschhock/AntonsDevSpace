---
title: Timeout while using OpenAi's .Net API
description: A quick post to showcase how to resolve slow chatcompletions without hitting the default timeout
date: 2025-02-12T20:00:00.907Z
preview: ""
draft: false
tags:
  - dotnet
  - C#
  - OpenAi
  - QuickPost
categories:
  - DotNet
slug: dotnet-openai-timeout
ShowToc: false
---

Ever had the issue that you hit the timeout of the OpenAI client and could not find any quick resolution (due to the library has shifted owners a couple of times)?

Well, don't worry - 
```cs
// Used nuget: Azure.AI.OpenAI@2.0.0
using OpenAI;
using OpenAI.Chat;
// ...
var config = sp.GetRequiredService<IOptions<AIConfiguration>>().Value;
var apiKey = config.ApiKey;
var client = new OpenAIClient(new(config.ApiKey), new OpenAIClientOptions
                {
                    NetworkTimeout = TimeSpan.FromMinutes(3)
                });
```

That'll be it!
Don't forget to C#! 👋
