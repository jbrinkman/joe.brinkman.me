---
{
    Title: "Can You Hear Me Now? Part 1",
    Lead: "Building Your First Voice Application with Alexa, C# and Evoq Liquid Content",
    Published: "11/06/2017",
    Tags: ["Alexa","AWS","AWS Lambda","DNN","EVOQ"]
}
---

## Overview

*[GUI]: Graphical User Interface
*[VUI]: Voice User Interface
*[NLP]: Natural Language Processing
*[ASR]: Automatic Speech Recognition
Every decade or two since the advent of computers, there has been a revolutionary product that fundamentally alters the computing landscape and creates massive new business opportunities. In the 70s this revolution was led by the creation of personal computers and the Apple II, Commodore PET and Tandy TRS-80.  In the 80s we saw whole new businesses created as the result of the revolution brought about by the GUI as exemplified by the Mac OS and Windows. In the 90s some of the largest companies in the world were started based on the creation of the World Wide Web and Netscape Navigator. In 2007 the modern mobile computing era was fueled by the creation of touch based devices and the Apple iPhone. In late 2014, Amazon launched a device which I believe marked the start of another innovation wave.

In this series I'll provide some background on the current state of the industry and walk through creating the sample voice application that we used to demonstrate the API capabilities of Evoq Liquid Content. While the code will be specific to Amazon Alexa and Evoq, the concepts are exactly the same regardless of whether you are creating applications for Amazon Alexa, Google Assistant or Microsoft Cortana.

- **Part 1:** What are Voice Applications
- **Part 2:** Defining and Building the Application
- **Part 3:** Testing and Deployment

## Voice Applications

The way we interact with computers has changed dramatically in the last 50 years. Each advancement seeks to make the interaction more closely resemble human to human interaction. The latest innovation in machine-human interaction was the creation of a mass market device that was built around a [VUI](https://en.wikipedia.org/wiki/Voice_user_interface). Amazon Echo is a revolutionary product that popularized the current trend around "smart speakers", and also created an entire ecosystem around the development of voice applications.

![Voice Application architecture](/assets/image/Alexa-Skill/Alexa-Skill-Architecture.png){.pull-left .img-small}
Voice applications are multi-layered systems that define the interactions and behaviors of an application designed for use where voice is the primary user interaction paradigm. Voice applications are distinct from the traditional application model that relies on visual elements to convey information to users. This high-level architecture is used in the three major voice application platforms (Amazon Alexa, Google Assistant and Microsoft Cortana).

One of the unique aspects of voice application architecture is that the VUI is defined and hosted by the platform vendor without any coding required, while the application logic can be hosted anywhere. This architecture is the epitome of a microservices based architecture.

### Voice Engine

The magic of any voice application resides in the voice engine (layer #1) provided by the vendor. The developer is responsible for creating the interaction model that the voice engine will use when processing a user's voice interaction. The voice engine uses [Natural Language Processing](https://en.wikipedia.org/wiki/Natural_language_processing) (NLP) and [Automatic Speech Recognition](https://en.wikipedia.org/wiki/Speech_recognition) (ASR) to translate a user's voice command into a structured command that can be understood by your application.

Every interaction model starts by defining intents, slots, and sample utterances. More advanced engines also allow you to define dialog flows in order to describe complex interactions which cannot be expressed in a single utterance. The interaction model describes the full capabilities of your application and should be robust enough to handle the complexity of natural language. Like any user interface, the quality of your interaction model will directly impact the experience your users have with your application.

**Note:** Microsoft and Google use the term Entities instead of the term slots. Other than the terminology difference slots and entities are used the same way in the various platforms. {.bg-info}

An intent defines the action that the user would like your application to perform.  It could be querying for some information, changing the state of a device like a light or door, or playing some media. In general, applications should be focused on handling a small number of intents. As the number of intents grows, the user experience begins degrading. For the Alexa platform, in addition to your own intents, you will also need to handle some built-in system intents like help, cancel and stop.

Slots define the parameters that are used to provide details related to the intent. For example if you said "Alexa, Play the latest song by Katy Perry", **playsong** might be the intent, and **latest** and **Katy Perry** would be the slots. The intent and slots provide enough information for your application to determine the appropriate action to take.

At the heart of every voice engine is an NLP algorithm that must be trained to recognize how to translate a given phrase to the intents and slots that have been defined. The phrases that you train the voice engine with are called utterances. It is not necessary to provide every possible utterance permutation when training the voice application, but enough variety should be provided so that the NLP algorithm can identify the common phrasing patterns, and from that it will be able to extrapolate all of the ways that someone might express a given intent. Usually, I will define three to five utterances that I think someone might use. When I get into the testing phase I will come up with several alternatives and use those to verify if the model is able to handle those variations. I'll cover that in more detail in a later part of the series.

### Application

The heart of a voice application resides in the application layer (layer #2). The application layer exists as a web service that can be called by the voice engine once it detects an utterance associated with the application. While the specific service calls and data format for each voice platform is different, the basics remain the same.

The voice engine sends a message to the application layer for different application lifecycle events like launch or session end. In addition the engine will call the application when an utterance is matched to an intent. The application is responsible for either starting a dialog interaction to request additional information from the user or fulfilling the intent request. How the application processes each request is completely within the applications control.

Since the application layer is just a web-service that can receive requests from the voice engine, it can be created using any programming language, framework or service that is capable of exposing an appropriate endpoint. Due to the nature and small size of most voice applications, they are easily hosted using serverless systems like [AWS Lambda](https://aws.amazon.com/lambda/) or [Azure Functions](https://azure.microsoft.com/en-us/services/functions/). While you do not need to use AWS or Azure for hosting your application, those services do offer additional features specifically tailored to running application code for the associated voice engine.

### Backend Services

Most voice applications will have a lightweight application layer and will call various backend services and systems (layer #3) for performing the actual work or accessing application data. Often, the application layer just becomes a translation layer or façade for relaying commands from the voice engine to some pre-existing service API(s). In the example application that goes with this series the service layer will be handled by [Evoq Liquid Content](http://www.dnnsoftware.com/cms-features/about-liquid-content). As a result, building this layer will be strictly a matter of gaining access to the API via an appropriately scoped API key.

## Think Differently

Writing voice applications requires a fundamentally different approach from writing traditional GUI applications. Developers have spent the last 30 years building visually rich application interfaces. We've incorporated sound and color and motion into our user experiences which helps evoke just the right emotion as users navigate through our applications and websites. The world of VUI applications is very different. It is like going from gigabit Ethernet to a 14.4k modem. In the dialup world, every byte traveling across the wire takes on that much more importance. The same is true in the VUI world, where you need to prioritize the most important information to convey to the user.

We've all heard the saying "a picture is worth a thousand words", unfortunately for developers of voice applications the human brain has a very small amount of short term memory. In the VUI world, applications should be designed to present the user with just a few choices or a few pieces of information at one time. If too much information is presented at once, the user will suffer from information overload and won't be able to recall the first portion of the information provided. It is critical that the VUI design presents information in small, bite sized chunks and that information is prioritized so the most important information is presented first.

Since we can't present the user with all of the information that may be available, voice applications must build in methods to allow users to get the next "chunk" of data or to get help on what other options might be available. You see this quite often in voicemail systems which offer prompts like "press five for additional options". Rarely will a voice mail system provide 10 different choices for a user, because long before the user reads the 9th option, they will have forgotten options one, two and three.

## Putting It All Together

What should be apparent at this point is that voice applications are different from traditional applications. They require different design thinking and a different application architecture. Voice applications include a voice engine, provided by your voice platform, and they include a custom application layer. Building a voice app is a two step process involving configuring the voice engine, and developing the application layer as a web service. This is readily apparent when building an Alexa Skill as even the most trivial skill will require accessing two different Amazon developer portals: one for the [AWS Skill configuration](https://developer.amazon.com/edw/home.html#/skills), and one for [hosting your application code](https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions).

Now that the basics are out of the way, I am ready to dive into the details about how to build and host your own voice application running on Amazon Alexa. Stay tuned for part 2 and 3 of this series.