---
title: Looking to use OpenAI's Assistant?
description: Let me help you figuring this out - so you don't need to struggle 4h long!
date: 2025-02-20T12:00:00.907Z
preview: ""
draft: false
tags:
  - dotnet
  - C#
  - OpenAI
  - Assistant
  - NotSoQuickPost
categories:
  - DotNet
slug: dotnet-openai-assistant
ShowToc: false
---

So, lately I was working on experimenting with OpenAI's SDK to use an OpenAI Assistant.
So I went ahead, built my assistant which used a PDF file as a basis to analyse and summarize it, based on additional input that I send via the userprompt - I was happy with the outcome in the playground so went ahead and started writing a simple UI in Razor where you can upload a file and add the user prompt and got everything ready for the OpenAI interaction.

So being the trustworthy developer I am, I followed [OpenAI's documentation](https://github.com/openai/openai-dotnet?tab=readme-ov-file#how-to-use-assistants-with-retrieval-augmented-generation-rag) down to the bone - but then! 500 happend.
No-matter I did I got 500 Server errors left and right.
Then I used their playground to figure out in what order which calls were made to run the assistant:

1. Create a "blank" thread:

```cs
var thread = assistantClient.CreateThread(
    new ThreadCreationOptions()
    {
        // literally BLANK
    }
);
```

2. Create your messages you need to add:

```cs
assistantClient.CreateMessage(thread.Value.Id,
                              MessageRole.User,
                              new List<MessageContent>() { MessageContent.FromText(Userprompt)}.AsEnumerable()
                             );
```

3. Have a file to add? Here we go:

```cs
var fileRef = await fileClient.UploadFileAsync(fileStream, $"File-{Guid.NewGuid()}.pdf", OpenAI.Files.FileUploadPurpose.Assistants);
assistantClient.CreateMessage(thread.Value.Id,
                              MessageRole.User,
                              new List<MessageContent>() { MessageContent.FromText("File to read") }.AsEnumerable(),
                              new MessageCreationOptions {
                                Attachments = new List<MessageCreationAttachment>(){
                                    new MessageCreationAttachment(
                                        fileRef.Value.Id,
                                        new List<ToolDefinition>(){ToolDefinition.CreateFileSearch()}
                                        )}
                                  }
                            );
```

4. Run it!

```cs
await foreach (var update in assistantClient.CreateRunStreamingAsync(thread.Value.Id, "asst_IDYouFindInThePlayground"))
{
    if (update is MessageContentUpdate contentUpdate)
    {
        Output += contentUpdate?.Text ?? "";
    }
}
```

There we go! We got a working assistant, using C# and the OpenAI SDK!
I just hope that the OpenAI / Microsoft updates their documentation and/or their API soon.
But until then here is the full code:

```cs
// Used **NuGet**: Azure.AI.OpenAI@2.0.0

var assistantClient = openAiClient.GetAssistantClient();

// step 1 - create a blank thread
var thread = assistantClient.CreateThread(
    new ThreadCreationOptions()
    {
        // literally BLANK
    }
);

// step 2 - create the messages you need
assistantClient.CreateMessage(thread.Value.Id,
                              MessageRole.User,
                              new List<MessageContent>() { MessageContent.FromText(Userprompt)}.AsEnumerable()
                             );

// step 3 - upload a file
var fileClient = openAiClient.GetOpenAIFileClient();
var fileRef = await fileClient.UploadFileAsync(fileStream, $"File-{Guid.NewGuid()}.pdf", OpenAI.Files.FileUploadPurpose.Assistants);
assistantClient.CreateMessage(thread.Value.Id,
                              MessageRole.User,
                              new List<MessageContent>() { MessageContent.FromText("File to read") }.AsEnumerable(),
                              new MessageCreationOptions {
                                Attachments = new List<MessageCreationAttachment>(){
                                    new MessageCreationAttachment(
                                        fileRef.Value.Id,
                                        new List<ToolDefinition>(){ToolDefinition.CreateFileSearch()}
                                        )}
                                  }
                            );

// step 4 - run it
await foreach (var update in assistantClient.CreateRunStreamingAsync(thread.Value.Id, "asst_IDYouFindInThePlayground"))
{
    if (update is MessageContentUpdate contentUpdate)
    {
        Output += contentUpdate?.Text ?? "";
    }
}
```

Oh, one last thing: you might need to format the output here and there due to reference tags, that the AI adds.

So it is not really a quick-post, but I hope it helps!
Don't forget to C# too! 👋
