---
{
    Title: "Can You Hear Me Now? Part 1",
    Lead: "Building Your First Voice Application with Alexa, C# and Evoq Liquid Content",
    Published: "10/27/2017",
    Tags: ["Alexa","AWS","AWS Lambda","DNN","EVOQ"]
}
---

## Overview

Every decade or two since the advent of computers, there has been a revolutionary product that fundamentally alters the computing landscape and creates massive new business opportunities. In the 70s this revolution was led by the creation of personal computers and the Apple II, Commodore PET and Tandy TRS-80.  In the 80s we saw whole new businesses created as the result of the revolution brought about by Graphical User Interfaces, Macintosh and Windows. In the 90s some of the largest companies in the world were started based on the creation of the World Wide Web and Netscape Navigator. In 2007 the modern mobile computing era was fueled by the creation of touch based devices and the Apple iPhone. In late 2014, Amazon launched a device which I believe marked the start of another innovation wave.

In this series I'll provide some background on the current state of the industry and walk through creating the sample voice application that we used to demonstrate the API capabilities of Evoq Liquid Content. While the code will be specific to Amazon Alexa and Evoq, the concepts are exactly the same regardless of whether you are creating applications for Amazon Alexa, Google Assistant or Microsoft Cortana.

- Part 1: What are Voice Applications
- Part 2: Defining and Building the Application
- Part 3: Testing and Deployment

## Voice Applications

The way we interact with computers has changed dramatically in the last 50 years. Each advancement seeks to make the interaction more closely resemble human to human interaction. The latest innovation in machine-human interaction was the creation of a mass market device that was built around a [Voice User Interface (VUI)](https://en.wikipedia.org/wiki/Voice_user_interface). Amazon Echo is a revolutionary product that popularized the current trend around "smart speakers", and also created an entire ecosystem around the development of voice applications.

![Voice Application architecture](/assets/image/alexa-skill/alexa-skill-architecture.png){.pull-left .img-small}
Voice Applications are multi-layered systems that define the interactions and behaviors of an application designed for use where voice is the primary user interaction paradigm. Voice applications are distinct from the traditional application model that relies on visual elements to convey information to users. This high-level architecture is used in every major voice application platform (Amazon Alexa, Google Assistant and Microsoft Cortana).

### Voice Engine

The magic of any voice application resides in the voice engine (layer #1) provided by the vendor. The developer is responsible for creating the interaction model that the voice engine will use when processing a user's voice interaction. The voice engine uses Natural Language Processing (NLP) and Automatic Speech Recognition (ASR) to translate a user's voice command into a structured command that can be understood by your application.

Every interaction model starts by defining intents, slots, and sample utterances. More advanced engines also allow you to define dialog flows in order to describe complex interactions which cannot be expressed in a single utterance. The interaction model describes the full capabilities of your application and should be robust enough to handle the complexity of natural language. Like any user interface, the quality of your interaction model will directly impact the experience your users have with your application.

**Note:** Microsoft and Google use the term Entities instead of the term slots. Other than the terminology difference slots and entities are used the same way in the various platforms. {.bg-info}

An intent defines the action that the user would like your application to perform.  It could be querying for some information, changing the state of a device like a light or door, or playing some media. In general, applications should be focused on handling a small number of intents. As the number of intents grows, the user experience begins degrading. For the Alexa platform, in addition to your own intents, you will also need to handle some built-in system intents like help, cancel and stop.

Slots define the parameters that are used to provide details related to the intent. For example if you said "Alexa, Play the latest song by Katy Perry", "playsong" might be the intent, and "latest" and "Katy Perry" would be the slots. The intent and slots provide enough information for your application to determine the appropriate action to take.

At the heart of every voice engine is an NLP algorithm that must be trained to recognize how to translate a given phrase to the intents and slots that have been defined. The phrases that you train the voice engine with are called utterances. It is not necessary to provide every possible utterance permutation when training the voice application, but enough variety should be provided so that the NLP algorithm can identify the common phrasing patterns, and from that it will be able to extrapolate all of the ways that someone might express a given intent. Usually, I will define three to five utterances that I think someone might use. When I get into the testing phase I will come up with several alternatives and use those to verify if the model is able to handle those variations. I'll cover that in more detail in a later part of the series.

### Application

The heart of a voice application resides in the application layer (layer #2). The application layer exists as a web service that can be called by the voice engine once it detects an utterance associated with the application. While the specific service calls and data format for each voice platform is different, the basics remain the same.

The voice engine sends a message to the application layer for different application lifecycle events like launch or session end. In addition the engine will call the application when an utterance is matched to an intent. The application is responsible for either starting a dialog interaction to request additional information from the user or fulfilling the intent request. How the application processes each request is completely within the applications control.

Since the application layer is just a web-service that can receive requests from the voice engine, it can be created using any programming language, framework or service that is capable of exposing an appropriate service endpoint.