---
{
    Title: "Can You Hear Me Now? Part 2",
    Lead: "Building Your First Voice Application with Alexa, C# and Evoq Liquid Content",
    Published: "11/07/2017",
    Tags: ["Alexa","AWS","AWS Lambda","DNN","EVOQ"],
    Image: ""
}
---

## Overview

Every decade or two since the advent of computers, there has been a revolutionary product that fundamentally alters the computing landscape and creates massive new business opportunities. In the 70s this revolution was led by the creation of personal computers and the Apple II, Commodore PET and Tandy TRS-80.  In the 80s we saw whole new businesses created as the result of the revolution brought about by Graphical User Interfaces, Macintosh and Windows. In the 90s some of the largest companies in the world were started based on the creation of the World Wide Web and Netscape Navigator. In 2007 the modern mobile computing era was fueled by the creation of touch based devices and the Apple iPhone. In late 2014, Amazon launched a device which I believe marked the start of another innovation wave.

In this series I'll provide some background on the current state of the industry and walk through creating the sample voice application that we used to demonstrate the API capabilities of Evoq Liquid Content. While the code will be specific to Amazon Alexa and Evoq, the concepts are exactly the same regardless of whether you are creating applications for Amazon Alexa, Google Assistant or Microsoft Cortana.

## Voice Applications

The way we interact with computers has changed dramatically in the last 50 years. Each advancement seeks to make the interaction more closely resemble human to human interaction. The latest innovation in machine-human interaction was the creation of a mass market device that was built around a [Voice User Interface (VUI)](https://en.wikipedia.org/wiki/Voice_user_interface). Amazon Echo is a revolutionary product that popularized the current trend around "smart speakers", and also created an entire ecosystem around the development of voice applications.

![Voice Application architecture](/assets/image/alexa-skill/alexa-skill-architecture.png){.pull-left .img-small}
Voice Applications are multi-layered systems that define the interactions and behaviors of an application designed for use where voice is the primary user interaction paradigm. This high-level architecture is used in every major voice application platform (Amazon Alexa, Google Assistant and Microsoft Cortana).

The intelligence of any voice application resides in the voice engine provided by the vendor. The developer is responsible for creating the interaction model that the voice engine will use when processing a user's voice interaction. The voice engine uses Natural Language Processing (NLP) and Automatic Speech Recognition (ASR) to translate a user's voice command into a structured command that can be understand by your application.

Every interaction model starts by defining intents, slots (or entities), and sample utterances. More advanced engines also allow you to define dialog flows 

## The Challenge

## Build AWS Lambda function

## Accessing Liquid Content

## Configure New Alexa Skill

## Test, Test, Test 