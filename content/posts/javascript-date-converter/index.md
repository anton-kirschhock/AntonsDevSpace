---
title: Javascript date converter for Newtonsoft.Json
description: A quick post to highlight how a Javascript date timestamp can be converted to a .Net DateTime(Offset)
date: 2025-01-17T08:26:12.907Z
preview: ""
draft: false
tags:
  - dotnet
  - C#
  - Javascript
  - Date
  - Newtonsoft
  - Json
categories:
  - DotNet
slug: javascript-date-converter
ShowToc: false
---

Ever got the need for a converter to convert a Javascript date timestamp to a DateTime and just don't find the right one?

-Issue with the built-in was that it was using seconds instead of milliseconds

-Stack Overflow was not really giving a solution

-Copilot did even weirder stuff (especially because it didn't know the new DateTimeOffset functions)

Well, I encountered that this week and in the end, wrote one myself.
In the spirit of Don't Repeat Yourself, I'll share that class:

```cs
using Newtonsoft.Json;
using Newtonsoft.Json.Converters;

namespace Converters
{
    /// <summary>
    /// Converts a <see cref="DateTime"/> to and from Javascript Date Timestamp
    /// </summary>
    public class JsDateTimestampConverter : DateTimeConverterBase
    {
        /// <summary>
        /// Initializes a new instance of the <see cref="JsDateTimestampConverter"/> class.
        /// </summary>
        public JsDateTimestampConverter()
        {
        }

        public override object? ReadJson(JsonReader reader, Type objectType, object? existingValue, JsonSerializer serializer)
        {
            if (reader.TokenType == JsonToken.Null)
            {
                return null;
            }

            long mSeconds;

            if (reader.TokenType == JsonToken.Integer)
            {
                mSeconds = (long)reader.Value!;
            }
            else if (reader.TokenType == JsonToken.String)
            {
                if (!long.TryParse((string)reader.Value!, out mSeconds))
                {
                    throw new JsonSerializationException($"Cannot convert {reader.Path} due to invalid value: {reader.Value} (tokentype={reader.TokenType})");
                }
            }
            else
            {
                throw new JsonSerializationException($"Cannot convert {reader.Path}! Expected Integer or string: {reader.Value} (tokentype={reader.TokenType})");
            }
            var dto = DateTimeOffset.FromUnixTimeMilliseconds(mSeconds);
            if (objectType == typeof(DateTime))
            {
                return dto.DateTime;
            }
            else if (objectType == typeof(DateTimeOffset))
            {
                return dto;
            }
            else if (objectType == typeof(DateTime?))
            {
                return (DateTime?)(dto.DateTime);
            }
            else
            {
                return (DateTimeOffset?)dto;
            }
        }

        public override void WriteJson(JsonWriter writer, object? value, JsonSerializer serializer)
        {
            if (value == null)
            {
                writer.WriteNull();
                return;
            }

            long mSeconds = value switch
            {
                DateTime dateTime => new DateTimeOffset(dateTime).ToUnixTimeMilliseconds(),
                DateTimeOffset dateTimeOffset => dateTimeOffset.ToUnixTimeMilliseconds(),
                _ => throw new JsonSerializationException($"Expected date object value. Got {value.GetType()}")
            };

            writer.WriteValue(mSeconds);
        }
    }
}
```

Is it perfect? No, definitely not - but it got me where I needed to be.
I hope that this gets you where you need to be too!
Don't forget to C#! 👋
