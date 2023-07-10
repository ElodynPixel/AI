# AI fundamentals-Exam tips
*************************************************
Notes for Exam tips AI exam certification

### Introduction:
 AI-900 indicates fundamentals
Ai focus is more for cognitive service, bots and Azure ML
Non AI focus is Microsoft responsible AI principles (ASCO framework)

***************************************************

# Artificial intelligence in Azure
Reasoning
	Draw conclusions from imperfect data
Understanding
	Interpret meaning of data such as images, video, audio
Interacting
	Communicate in more natural ways

# AI workloads
ML (prediction)
Anomaly detection (Fraud and failure detection)
Computer vision (Classify or detect objects)
Natural language processing (Interpret language)
Conversational AI (Chatbots)


# 3 Technological advancements
## Big data
Cheaper and faster storage

## High compute
GPU and sale-out clusters

## Algorithms
Advancements in AI and ML algorithms

*******************************************************

## Cognitive services
-Building AI infused apps with no ML /AI knowledge
-Highly refined models
-Ample language support
-Privacy assured
-Low cost including free tier

## Cognitive service pillars
Vision (Custom vision)
Speech (Speech studio)
Language (LUIS)
Decision (Content moderator)
Web search (Big custom search)
Create your own AI model

## Cognitive Services decision workflow
Generic (Use generic service)
Custom (custom service/ create own)

## Cognitive Services lifecycle
### Labs (labs.cognitive.microsoft.com)
### Preview (speaker recognition and anomaly detector)
### GA (Generally available)
### Retired

****************************************

# Microsoft Responsible AI
## Microsoft responsible AI Principles
Fairness
Reliability and safety
Privacy and security
Inclusiveness
Transparency
Accountability

***************************************

# Vision
## Computer vision (CATCH ALL)
`Colors and descriptions
`Age, gender and face location
`Thumbnails
`Categories, tags, brands and objects
`Handwriting and OCR

`Adult, racy and gory
`Line drawing and clipart
`Landmarks and celebrities

## Face API
1. Create a person group (Or larger person group)
2. Register each person
3. Upload face pictures
4. Train the model

## Form and ink recognizers

### Form recognizer services
Custom models (key/value pair and table extractions)
US receipt format
Layout API (text and table structures)

### Ink recognizer

Process
Ink stroke input--API---Recognition tree

## Custom Vision

### Two main capabilities of custom vision
#### Classification
#### Object detection

### Custom vision details
Interactive portal (www.customvision.ai)
Two separate end point and keys (for training and prediction)
Several specialized domains
Supports edge computing (compact models)

### Custom vision best practices
-Ideally at least 50 images/tag
-Balanced input of images (bananas and oranges)
-Add negative images (neither banana nor orange)
-Fix wrong past predictions to improve the model

Resources and additional resources
https://aidemos.microsoft.com
https://azure.microsoft.com/en-us/services/cognitive-services/face
customvision.ai/projects

additional resources
https://aka.ms/explore-computer-vision
https://aischool.microsoft.com/en-us/home
https://aidemos.microsoft.com
https://docs.microsoft.com/en-us/azure/cognitive-services
https://github.com/microsoft

LinkedIn learning
Microsoft cognitive services for developers: 1 Vision with Sahil Malik


******************************************************
# Natural language processing
### Speech
-Speech to text (STT)
-Text to speech (TTS)
-Speech translation
-Speaker recognition
-Speech services
-Speech studio

### Language
-Text analytics
-Translator and custom translator
-LUIS
-QnA maker

### Speech technologies
 The Microsoft speech API's are quite mature, as they rely on models already used by Microsoft for many years on tools such as Skype, Xbox, and Cortana. 
 They are Low latency on the sub second level after the last byte is received. 
 Also, they support over 45 languages the paint job API, they also natively integrate with a Bot Framework which is simplifies the creation of voice bots.

## Speech API's

### STT
**Three recognition modes**
-Recognize once
-Continuous
-Dictation

**Handles profanity**
-Raw (allows profanity)
-Masked (Covered with asterisks)
-Removed (deletes profanity)

**Batch transcriptions**
-Audio processing (Customer services)

**Speech devices SDK**
-Speech enabled devices

### TTS
**Three voice types**
-Standard (more language options, robotic)
-Neural (less languages, more humanlike)
-Custom 

SSML (XML based) (Speech synthesis markup language)
-Controls speed, pitch, volume, pronunciation

**Speech translation**
-60 Languages
-Translation returned as text/ optionally synthesized voice (not available for all languages)
-Handles profanity (Raw, Masked (default), Removed)

**Speaker recognition**
-Speaker verification (authentication purposes)
	-Set up
		(voice) Enrollment phase (Passphase)
		Voice signature is generated
		Use it to grant access
-Speaker identification (recognize speaker from audio file)
	-Simpler enrollment process



## Speech services and speech studio
### Speech studio (custom speech portal on Azure) (at least 8h audio + corresponding transcripts)
**Acoustic models**
-Environment
-Speaker
-Audio equipment

**Language models**
-Language model (pharma, medical, sci fi)
-Pronunciation models
-Voice fonts



************************************
# Creating a bot

## Conversational AI

## Bot framework

************************************
# Workingg with ML solutions

## Introduction to Machine Learning

## Classification on Azure ML

## Create a custom Azure ML resource

## Automated ML

*************************************
# Prepare for the Microsoft Azure AI Fundamentals (AI-900) certification
