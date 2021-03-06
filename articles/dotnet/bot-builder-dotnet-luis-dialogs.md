---
title: Enable language understanding with LUIS | Microsoft Docs
description: Learn how to enable your bot to understand natural language by using LUIS dialogs in the Bot Builder SDK for .NET.
author: kbrandl
ms.author: v-kibran
manager: rstand
ms.topic: article
ms.prod: bot-framework
ms.date: 
ms.reviewer:
---

# Enable language understanding with LUIS

This article describes how to use <a href="https://www.luis.ai" target="_blank">LUIS</a> with dialogs to 
create an Alarm bot that a user can interact with using [natural language](../cognitive-services-bot-intelligence-overview.md#language-understanding). 

## Create the class

To create a dialog that uses LUIS, first create a class that derives from `LuisDialog` and 
specify the `LuisModel` attribute. 
To populate the parameters for the `LuisModel` attribute, use 
the `id` and `subscription-key` attribute values from your LUIS application's endpoint.

[!code-csharp[Class definition](../includes/code/dotnet-luis-dialogs.cs#classDefinition)]

## Create method(s) to handle intent

Within the class, create the methods that will execute when your LUIS model matches a user's utterance to intent. 
To designate the method that will execute when a specific intent is matched, specify the `LuisIntent` attribute. 
This code example defines the method that will execute when the `builtin.intent.alarm.turn_off_alarm` intent is matched.

[!code-csharp[Turn-off-alarm handler](../includes/code/dotnet-luis-dialogs.cs#turnOffAlarmHandler)]

In this example, if the bot finds the alarm that the user wants to turn off, 
it confirms the user's request by using the built-in `Prompt.Confirm` dialog. 
The confirm dialog will spawn a sub-dialog that asks the user to verify the request to turn off the alarm. 
If the user verifies the request, the dialog calls the `AfterConfirming_TurnOffAlarm` method to turn off the alarm. 

## Alarm bot implementation

This code example shows the full dialog implementation for the Alarm bot. 

[!code-csharp[Full LUIS dialog example](../includes/code/dotnet-luis-dialogs.cs#fullExample)]

## Additional resources

- [Dialogs](bot-builder-dotnet-dialogs.md)
- [Manage conversation flow with dialogs](bot-builder-dotnet-manage-conversation-flow.md)
- [Language understanding](../cognitive-services-bot-intelligence-overview.md#language-understanding)
- <a href="https://www.luis.ai" target="_blank">LUIS</a>
- <a href="https://docs.microsoft.com/en-us/dotnet/api/?view=botbuilder-3.8" target="_blank">Bot Builder SDK for .NET Reference</a>