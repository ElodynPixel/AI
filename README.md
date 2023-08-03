# NLP
# Analyzing text with the Language service
# Introduction

Analyzing text is a process where you evaluate different aspects of a document or phrase, in order to gain insights into the content of that text. For the most part, humans are able to read some text and understand the meaning behind it. Even without considering grammar rules for the language the text is written in, specific insights can be identified in the text.

As an example, you might read some text and identify some key phrases that indicate the main talking points of the text. You might also recognize names of people or well-known landmarks such as the Eiffel Tower. Although difficult at times, you might also be able to get a sense for how the person was feeling when they wrote the text, also commonly known as sentiment.

## Text Analytics Techniques

Text analytics is a process where an artificial intelligence (AI) algorithm, running on a computer, evaluates these same attributes in text, to determine specific insights. A person will typically rely on their own experiences and knowledge to achieve the insights. A computer must be provided with similar knowledge to be able to perform the task. There are some commonly used techniques that can be used to build software to analyze text, including:

- Statistical analysis of terms used in the text. For example, removing common "stop words" (words like "the" or "a", which reveal little semantic information about the text), and performing _frequency analysis_ of the remaining words (counting how often each word appears) can provide clues about the main subject of the text.
- Extending frequency analysis to multi-term phrases, commonly known as _N-grams_ (a two-word phrase is a _bi-gram_, a three-word phrase is a _tri-gram_, and so on).
- Applying _stemming_ or _lemmatization_ algorithms to normalize words before counting them - for example, so that words like "power", "powered", and "powerful" are interpreted as being the same word.
- Applying linguistic structure rules to analyze sentences - for example, breaking down sentences into tree-like structures such as a _noun phrase_, which itself contains _nouns_, _verbs_, _adjectives_, and so on.
- Encoding words or terms as numeric features that can be used to train a machine learning model. For example, to classify a text document based on the terms it contains. This technique is often used to perform _sentiment analysis_, in which a document is classified as positive or negative.
- Creating _vectorized_ models that capture semantic relationships between words by assigning them to locations in n-dimensional space. This modeling technique might, for example, assign values to the words "flower" and "plant" that locate them close to one another, while "skateboard" might be given a value that positions it much further away.

While these techniques can be used to great effect, programming them can be complex. In Microsoft Azure, the **Language** cognitive service can help simplify application development by using pre-trained models that can:

- Determine the language of a document or text (for example, French or English).
- Perform sentiment analysis on text to determine a positive or negative sentiment.
- Extract key phrases from text that might indicate its main talking points.
- Identify and categorize entities in the text. Entities can be people, places, organizations, or even everyday items such as dates, times, quantities, and so on.

In this module, you'll explore some of these capabilities and gain an understanding of how you might apply them to applications such as:

- A social media feed analyzer to detect sentiment around a political campaign or a product in market.
- A document search application that extracts key phrases to help summarize the main subject matter of documents in a catalog.
- A tool to extract brand information or company names from documents or other text for identification purposes.

These examples are just a small sample of the many areas that the Language service can help with text analytics.

# Get started with text analysis

The Language service is a part of the Azure Cognitive Services offerings that can perform advanced natural language processing over raw text.

## Azure resources for the Language service

To use the Language service in an application, you must provision an appropriate resource in your Azure subscription. You can choose to provision either of the following types of resource:

- A **Language** resource - choose this resource type if you only plan to use natural language processing services, or if you want to manage access and billing for the resource separately from other services.
- A **Cognitive Services** resource - choose this resource type if you plan to use the Language service in combination with other cognitive services, and you want to manage access and billing for these services together.

## Language detection

Use the language detection capability of the Language service to identify the language in which text is written. You can submit multiple documents at a time for analysis. For each document submitted to it, the service will detect:

- The language name (for example "English").
- The ISO 639-1 language code (for example, "en").
- A score indicating a level of confidence in the language detection.

For example, consider a scenario where you own and operate a restaurant where customers can complete surveys and provide feedback on the food, the service, staff, and so on. Suppose you have received the following reviews from customers:

> **Review 1**: "_A fantastic place for lunch. The soup was delicious._"
> 
> **Review 2**: "_Comida maravillosa y gran servicio._"
> 
> **Review 3**: "_The croque monsieur avec frites was terrific. Bon appetit!_"

You can use the text analytics capabilities in the Language service to detect the language for each of these reviews; and it might respond with the following results:

|Document|Language Name|ISO 6391 Code|Score|
|---|---|---|---|
|Review 1|English|en|1.0|
|Review 2|Spanish|es|1.0|
|Review 3|English|en|0.9|

Notice that the language detected for review 3 is English, despite the text containing a mix of English and French. The language detection service will focus on the _**predominant**_ language in the text. The service uses an algorithm to determine the predominant language, such as length of phrases or total amount of text for the language compared to other languages in the text. The predominant language will be the value returned, along with the language code. The confidence score may be less than 1 as a result of the mixed language text.

### Ambiguous or mixed language content

There may be text that is ambiguous in nature, or that has mixed language content. These situations can present a challenge to the service. An ambiguous content example would be a case where the document contains limited text, or only punctuation. For example, using the service to analyze the text ":-)", results in a value of **unknown** for the language name and the language identifier, and a score of **NaN** (which is used to indicate _not a number_).

## Sentiment analysis

The text analytics capabilities in the Language service can evaluate text and return sentiment scores and labels for each sentence. This capability is useful for detecting positive and negative sentiment in social media, customer reviews, discussion forums and more.

Using the pre-built machine learning classification model, the service evaluates the text and returns a sentiment score in the range of 0 to 1, with values closer to 1 being a positive sentiment. Scores that are close to the middle of the range (0.5) are considered neutral or indeterminate.

For example, the following two restaurant reviews could be analyzed for sentiment:

> "_We had dinner at this restaurant last night and the first thing I noticed was how courteous the staff was. We were greeted in a friendly manner and taken to our table right away. The table was clean, the chairs were comfortable, and the food was amazing._"

and

> "_Our dining experience at this restaurant was one of the worst I've ever had. The service was slow, and the food was awful. I'll never eat at this establishment again._"

The sentiment score for the first review might be around 0.9, indicating a positive sentiment; while the score for the second review might be closer to 0.1, indicating a negative sentiment.

### Indeterminate sentiment

A score of 0.5 might indicate that the sentiment of the text is indeterminate, and could result from text that does not have sufficient context to discern a sentiment or insufficient phrasing. For example, a list of words in a sentence that has no structure, could result in an indeterminate score. Another example where a score may be 0.5 is in the case where the wrong language code was used. A language code (such as "en" for English, or "fr" for French) is used to inform the service which language the text is in. If you pass text in French but tell the service the language code is **en** for English, the service will return a score of precisely 0.5.

## Key phrase extraction

Key phrase extraction is the concept of evaluating the text of a document, or documents, and then identifying the main talking points of the document(s). Consider the restaurant scenario discussed previously. Depending on the volume of surveys that you have collected, it can take a long time to read through the reviews. Instead, you can use the key phrase extraction capabilities of the Language service to summarize the main points.

You might receive a review such as:

> "_We had dinner here for a birthday celebration and had a fantastic experience. We were greeted by a friendly hostess and taken to our table right away. The ambiance was relaxed, the food was amazing, and service was terrific. If you like great food and attentive service, you should try this place._"

Key phrase extraction can provide some context to this review by extracting the following phrases:

- attentive service
- great food
- birthday celebration
- fantastic experience
- table
- friendly hostess
- dinner
- ambiance
- place

Not only can you use sentiment analysis to determine that this review is positive, you can use the key phrases to identify important elements of the review.

## Entity recognition

You can provide the Language service with unstructured text and it will return a list of _entities_ in the text that it recognizes. The service can also provide links to more information about that entity on the web. An entity is essentially an item of a particular type or a category; and in some cases, subtype, such as those as shown in the following table.

|Type|SubType|Example|
|---|---|---|
|Person||"Bill Gates", "John"|
|Location||"Paris", "New York"|
|Organization||"Microsoft"|
|Quantity|Number|"6" or "six"|
|Quantity|Percentage|"25%" or "fifty percent"|
|Quantity|Ordinal|"1st" or "first"|
|Quantity|Age|"90 day old" or "30 years old"|
|Quantity|Currency|"10.99"|
|Quantity|Dimension|"10 miles", "40 cm"|
|Quantity|Temperature|"45 degrees"|
|DateTime||"6:30PM February 4, 2012"|
|DateTime|Date|"May 2nd, 2017" or "05/02/2017"|
|DateTime|Time|"8am" or "8:00"|
|DateTime|DateRange|"May 2nd to May 5th"|
|DateTime|TimeRange|"6pm to 7pm"|
|DateTime|Duration|"1 minute and 45 seconds"|
|DateTime|Set|"every Tuesday"|
|URL||"`https://www.bing.com`"|
|Email||"`support@microsoft.com`"|
|US-based Phone Number||"(312) 555-0176"|
|IP Address||"10.0.1.125"|

The service also supports _entity linking_ to help disambiguate entities by linking to a specific reference. For recognized entities, the service returns a URL for a relevant _Wikipedia_ article.

For example, suppose you use the Language service to detect entities in the following restaurant review extract:

> "_I ate at the restaurant in Seattle last week._"

|Entity|Type|SubType|Wikipedia URL|
|---|---|---|---|
|Seattle|Location||https://en.wikipedia.org/wiki/Seattle|
|last week|DateTime|DateRange||

# Recognize and synthesize speech
# Introduction

Increasingly, we expect artificial intelligence (AI) solutions to accept vocal commands and provide spoken responses. Consider the growing number of home and auto systems that you can control by speaking to them - issuing commands such as "turn off the lights", and soliciting verbal answers to questions such as "will it rain today?"

To enable this kind of interaction, the AI system must support two capabilities:

- **Speech recognition** - the ability to detect and interpret spoken input.
- **Speech synthesis** - the ability to generate spoken output.

## Speech recognition

Speech recognition is concerned with taking the spoken word and converting it into data that can be processed - often by transcribing it into a text representation. The spoken words can be in the form of a recorded voice in an audio file, or live audio from a microphone. Speech patterns are analyzed in the audio to determine recognizable patterns that are mapped to words. To accomplish this feat, the software typically uses multiple types of models, including:

- An _acoustic_ model that converts the audio signal into phonemes (representations of specific sounds).
- A _language_ model that maps phonemes to words, usually using a statistical algorithm that predicts the most probable sequence of words based on the phonemes.

The recognized words are typically converted to text, which you can use for various purposes, such as.

- Providing closed captions for recorded or live videos
- Creating a transcript of a phone call or meeting
- Automated note dictation
- Determining intended user input for further processing

## Speech synthesis

Speech synthesis is in many respects the reverse of speech recognition. It is concerned with vocalizing data, usually by converting text to speech. A speech synthesis solution typically requires the following information:

- The text to be spoken.
- The voice to be used to vocalize the speech.

To synthesize speech, the system typically _tokenizes_ the text to break it down into individual words, and assigns phonetic sounds to each word. It then breaks the phonetic transcription into _prosodic_ units (such as phrases, clauses, or sentences) to create phonemes that will be converted to audio format. These phonemes are then synthesized as audio by applying a voice, which will determine parameters such as pitch and timbre; and generating an audio wave form that can be output to a speaker or written to a file.

You can use the output of speech synthesis for many purposes, including:

- Generating spoken responses to user input.
- Creating voice menus for telephone systems.
- Reading email or text messages aloud in hands-free scenarios.
- Broadcasting announcements in public locations, such as railway stations or airports.

# Get started with speech on Azure

Microsoft Azure offers both speech recognition and speech synthesis capabilities through the **Speech** cognitive service, which includes the following application programming interfaces (APIs):

- The **Speech to text** API
- The **Text to speech** API

## Azure resources for the Speech service

To use the Speech service in an application, you must create an appropriate resource in your Azure subscription. You can choose to create either of the following types of resource:

- A **Speech** resource - choose this resource type if you only plan to use the Speech service, or if you want to manage access and billing for the resource separately from other services.
- A **Cognitive Services** resource - choose this resource type if you plan to use the Speech service in combination with other cognitive services, and you want to manage access and billing for these services together.

## The Speech to text API

You can use the Speech to text API to perform real-time or batch transcription of audio into a text format. The audio source for transcription can be a real-time audio stream from a microphone or an audio file.

The model that is used by the Speech to text API, is based on the Universal Language Model that was trained by Microsoft. The data for the model is Microsoft-owned and deployed to Microsoft Azure. The model is optimized for two scenarios, conversational and dictation. You can also create and train your own custom models including acoustics, language, and pronunciation if the pre-built models from Microsoft do not provide what you need.

### Real-time transcription

Real-time speech to text allows you to transcribe text in audio streams. You can use real-time transcription for presentations, demos, or any other scenario where a person is speaking.

In order for real-time transcription to work, your application will need to be listening for incoming audio from a microphone, or other audio input source such as an audio file. Your application code streams the audio to the service, which returns the transcribed text.

### Batch transcription

Not all speech to text scenarios are real time. You may have audio recordings stored on a file share, a remote server, or even on Azure storage. You can point to audio files with a shared access signature (SAS) URI and asynchronously receive transcription results.

Batch transcription should be run in an asynchronous manner because the batch jobs are scheduled on a _best-effort basis_. Normally a job will start executing within minutes of the request but there is no estimate for when a job changes into the running state.

## The text to speech API

The text to speech API enables you to convert text input to audible speech, which can either be played directly through a computer speaker or written to an audio file.

### Speech synthesis voices

When you use the text to speech API, you can specify the voice to be used to vocalize the text. This capability offers you the flexibility to personalize your speech synthesis solution and give it a specific character.

The service includes multiple pre-defined voices with support for multiple languages and regional pronunciation, including _standard_ voices as well as _neural_ voices that leverage _neural networks_ to overcome common limitations in speech synthesis with regard to intonation, resulting in a more natural sounding voice. You can also develop custom voices and use them with the text to speech API

## Supported Languages

Both the speech to text and text to speech APIs support a variety of languages. Use the links below to find details about the supported languages:

- [Speech to text languages](https://learn.microsoft.com/en-us/azure/cognitive-services/speech-service/language-support#speech-to-text).
- [Text to speech languages](https://learn.microsoft.com/en-us/azure/cognitive-services/speech-service/language-support#text-to-speech).

# Summary

Speech recognition is concerned with taking the spoken word and converting it into a text representation, while speech synthesis is the process of converting text data to audible speech. Both of these tasks are supported by the Speech cognitive service.

# Summary

The Language service provides advanced natural language processing over raw text, and includes four main functions: sentiment analysis, key phrase extraction, language detection, and named entity recognition.

# Translate Text and Speech
# Introduction


As organizations and individuals increasingly need to collaborate with people in other cultures and geographic locations, the removal of language barriers has become a significant problem.

One solution is to find bilingual, or even multilingual, people to translate between languages. However the scarcity of such skills, and the number of possible language combinations can make this approach difficult to scale. Increasingly, automated translation, sometimes known as _machine translation_, is being employed to solve this problem.

## Literal and semantic translation

Early attempts at machine translation applied _literal_ translations. A literal translation is where each word is translated to the corresponding word in the target language. This approach presents some issues. For one case, there may not be an equivalent word in the target language. Another case is where literal translation can change the meaning of the phrase or not get the context correct.

For example, the French phrase "_éteindre la lumière_" can be translated to English as "_turn off the light_". However, in French you might also say "_fermer la lumiere_" to mean the same thing. The French verb _fermer_ literally means to "_close_", so a literal translation based only on the words would indicate, in English, "_close the light_"; which for the average English speaker, doesn't really make sense, so to be useful, a translation service should take into account the semantic context and return an English translation of "_turn off the light_".

Artificial intelligence systems must be able to understand, not only the words, but also the _semantic_ context in which they are used. In this way, the service can return a more accurate translation of the input phrase or phrases. The grammar rules, formal versus informal, and colloquialisms all need to be considered.

## Text and speech translation

_Text translation_ can be used to translate documents from one language to another, translate email communications that come from foreign governments, and even provide the ability to translate web pages on the Internet. Many times you will see a _Translate_ option for posts on social media sites, or the Bing search engine can offer to translate entire web pages that are returned in search results.

_Speech translation_ is used to translate between spoken languages, sometimes directly (speech-to-speech translation) and sometimes by translating to an intermediary text format (speech-to-text translation).

# Get started with translation in Azure

Microsoft Azure provides cognitive services that support translation. Specifically, you can use the following services:

- The **Translator** service, which supports text-to-text translation.
- The **Speech** service, which enables speech to text and speech-to-speech translation.

## Azure resources for Translator and Speech

Before you can use the Translator or Speech services, you must provision appropriate resources in your Azure subscription.

There are dedicated **Translator** and **Speech** resource types for these services, which you can use if you want to manage access and billing for each service individually.

Alternatively, you can create a **Cognitive Services** resource that provides access to both services through a single Azure resource, consolidating billing and enabling applications to access both services through a single endpoint and authentication key.

## Text translation with the Translator service

The Translator service is easy to integrate in your applications, websites, tools, and solutions. The service uses a Neural Machine Translation (NMT) model for translation, which analyzes the semantic context of the text and renders a more accurate and complete translation as a result.

### Translator service language support

The Translator service supports text-to-text translation between [more than 60 languages](https://learn.microsoft.com/en-us/azure/cognitive-services/translator/languages). When using the service, you must specify the language you are translating _**from**_ and the language you are translating _**to**_ using ISO 639-1 language codes, such as _en_ for English, _fr_ for French, and _zh_ for Chinese. Alternatively, you can specify cultural variants of languages by extending the language code with the appropriate 3166-1 cultural code - for example, _en-US_ for US English, _en-GB_ for British English, or _fr-CA_ for Canadian French.

When using the Translator service, you can specify one _**from**_ language with multiple _**to**_ languages, enabling you to simultaneously translate a source document into multiple languages.

### Optional Configurations

The Translator API offers some optional configuration to help you fine-tune the results that are returned, including:

- **Profanity filtering**. Without any configuration, the service will translate the input text, without filtering out profanity. Profanity levels are typically culture-specific but you can control profanity translation by either marking the translated text as profane or by omitting it in the results.
- **Selective translation**. You can tag content so that it isn't translated. For example, you may want to tag code, a brand name, or a word/phrase that doesn't make sense when localized.

## Speech translation with the Speech service

The Speech service includes the following application programming interfaces (APIs):

- **Speech to text** - used to transcribe speech from an audio source to text format.
- **Text to speech** - used to generate spoken audio from a text source.
- **Speech Translation** - used to translate speech in one language to text or speech in another.

You can use the **Speech Translation** API to translate spoken audio from a streaming source, such as a microphone or audio file, and return the translation as text or an audio stream. This enables scenarios such as real-time closed captioning for a speech or simultaneous two-way translation of a spoken conversation.

### Speech service language support

As with the Translator service, you can specify one source language and one or more target languages to which the source should be translated. You can translate speech into [over 60 languages](https://learn.microsoft.com/en-us/azure/cognitive-services/speech-service/language-support#speech-translation).

The source language must be specified using the extended language and culture code format, such as _es-US_ for American Spanish. This requirement helps ensure that the source is understood properly, allowing for localized pronunciation and linguistic idioms.

The target languages must be specified using a two-character language code, such as _en_ for English or _de_ for German.

# Create a language model with conversational Language understanding

# Introduction

In 1950, the British mathematician Alan Turing devised the _Imitation Game_, which has become known as the _Turing Test_ and hypothesizes that if a dialog is natural enough, you may not know whether you're conversing with a human or a computer. As artificial intelligence (AI) grows ever more sophisticated, this kind of conversational interaction with applications and digital assistants is becoming more and more common, and in specific scenarios can result in human-like interactions with AI agents. Common scenarios for this kind of solution include customer support applications, reservation systems, and home automation among others.

To realize the aspiration of the imitation game, computers need not only to be able to accept language as input (either in text or audio format), but also to be able to interpret the semantic meaning of the input - in other words, _understand_ what is being said.

On Microsoft Azure, conversational language understanding is supported through the **Language Service**. To work with Conversational Language Understanding, you need to take into account three core concepts: _utterances_, _entities_, and _intents_.

## Utterances

An utterance is an example of something a user might say, and which your application must interpret. For example, when using a home automation system, a user might use the following utterances:

> "_Switch the fan on._"
> 
> "_Turn on the light._"

## Entities

An entity is an item to which an utterance refers. For example, **fan** and **light** in the following utterances:

> "_Switch the _**fan**_ on._"
> 
> "_Turn on the _**light**_._"

You can think of the **fan** and **light** entities as being specific instances of a general **device** entity.

## Intents

An intent represents the purpose, or goal, expressed in a user's utterance. For example, for both of the previously considered utterances, the intent is to turn a device on; so in your Conversational Language Understanding application, you might define a **TurnOn** intent that is related to these utterances.

A Language Understanding application defines a model consisting of intents and entities. Utterances are used to train the model to identify the most likely intent and the entities to which it should be applied based on a given input. The home assistant application we've been considering might include multiple intents, like the following examples:

|Intent|Related Utterances|Entities|
|---|---|---|
|Greeting|"Hello"||
||"Hi"||
||"Hey"||
||"Good morning"||
|TurnOn|"Switch the fan on"|fan (device)|
||"Turn the light on"|light (device)|
||"Turn on the light"|light (device)|
|TurnOff|"Switch the fan off"|fan (device)|
||"Turn the light off"|light (device)|
||"Turn off the light"|light (device)|
|CheckWeather|"What is the weather for today?"|today (datetime)|
||"Give me the weather forecast"||
||"What is the forecast for Paris?"|Paris (location)|
||"What will the weather be like in Seattle tomorrow?"|Seattle (location), tomorrow (datetime)|
|None|"What is the meaning of life?"||
||"Is this thing on?"||

In this table there are numerous utterances used for each of the intents. The intent should be a concise way of grouping the utterance tasks. Of special interest is the _**None**_ intent. You should consider always using the None intent to help handle utterances that do not map any of the utterances you have entered. The None intent is considered a fallback, and is typically used to provide a generic response to users when their requests don't match any other intent.

Tip

In a Conversational Language Understanding application, the **None** intent is created but left empty on purpose. The None intent is a required intent and can't be deleted or renamed. Fill it with utterances that are outside of your domain.

After defining the entities and intents with sample utterances in your Conversational Language Understanding application, you can train a language model to predict intents and entities from user input - even if it doesn't match the sample utterances exactly. You can then use the model from a client application to retrieve predictions and respond appropriately.

# Getting started with Conversational Language Understanding

Creating an application with Conversational Language Understanding consists of two main tasks. First you must define entities, intents, and utterances with which to train the language model - referred to as _authoring_ the model. Then you must publish the model so that client applications can use it for intent and entity _prediction_ based on user input.

## Azure resources for Conversational Language Understanding

For each of the authoring and prediction tasks, you need a resource in your Azure subscription. You can use the following types of resource:

- **Language Service**: A resource that enables you to build apps with industry-leading natural language understanding capabilities without machine learning expertise.
- **Cognitive Services**: A general cognitive services resource that includes Conversational Language Understanding along with many other cognitive services. You can only use this type of resource for _prediction_.

The separation of resources is useful when you want to track resource utilization for Language Service use separately from client applications using all Cognitive Services applications.

When your client application uses a Cognitive Services resource, you can manage access to all of the cognitive services being used, including the Language Service, through a single endpoint and key.

## Authoring

After you've created an authoring resource, you can use it to author and train a Conversational Language Understanding application by defining the entities and intents that your application will predict as well as utterances for each intent that can be used to train the predictive model.

Conversational Language Understanding provides a comprehensive collection of prebuilt _domains_ that include pre-defined intents and entities for common scenarios; which you can use as a starting point for your model. You can also create your own entities and intents.

When you create entities and intents, you can do so in any order. You can create an intent, and select words in the sample utterances you define for it to create entities for them; or you can create the entities ahead of time and then map them to words in utterances as you're creating the intents.

You can write code to define the elements of your model, but in most cases it's easiest to author your model using the Language Understanding portal - a web-based interface for creating and managing Conversational Language Understanding applications.

Tip

Best practice is to use the Language portal for authoring and to use the SDK for runtime predictions.

### Creating intents

Define intents based on actions a user would want to perform with your application. For each intent, you should include a variety of utterances that provide examples of how a user might express the intent.

If an intent can be applied to multiple entities, be sure to include sample utterances for each potential entity; and ensure that each entity is identified in the utterance.

### Creating entities

There are four types of entities:

- **Machine-Learned**: Entities that are learned by your model during training from context in the sample utterances you provide.
- **List**: Entities that are defined as a hierarchy of lists and sublists. For example, a **device** list might include sublists for **light** and **fan**. For each list entry, you can specify synonyms, such as **lamp** for **light**.
- **RegEx**: Entities that are defined as a _regular expression_ that describes a pattern - for example, you might define a pattern like **[0-9]{3}-[0-9]{3}-[0-9]{4}** for telephone numbers of the form _**555-123-4567**_.
- **Pattern.any**: Entities that are used with _patterns_ to define complex entities that may be hard to extract from sample utterances.

### Training the model

After you have defined the intents and entities in your model, and included a suitable set of sample utterances; the next step is to train the model. Training is the process of using your sample utterances to teach your model to match natural language expressions that a user might say to probable intents and entities.

After training the model, you can test it by submitting text and reviewing the predicted intents. Training and testing is an iterative process. After you train your model, you test it with sample utterances to see if the intents and entities are recognized correctly. If they're not, make updates, retrain, and test again.

## Predicting

When you are satisfied with the results from the training and testing, you can publish your Conversational Language Understanding application to a prediction resource for consumption.

Client applications can use the model by connecting to the endpoint for the prediction resource, specifying the appropriate authentication key; and submit user input to get predicted intents and entities. The predictions are returned to the client application, which can then take appropriate action based on the predicted intent.

# Summary

You can use Conversational Language Understanding to build a model that predicts intents and entities from natural language utterances. A client application can then use this trained model to respond to natural language user input.

You can find out more about Conversational Language Understanding in the [service documentation](https://learn.microsoft.com/en-us/azure/cognitive-services/language-service/conversational-language-understanding/overview).

