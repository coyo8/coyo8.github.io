---
layout: proj
title: SmartXplorer
desc: Voice based question recognition system. No one will need to type a question again.
---

# SmartXplorer

<hr>
### INTRODUCTION

SmartXplorer is a mobile app in which user can ask question directly in his voice related to any topic (Life, Science, Technology, etc) and App will be able to provide best possible answer to user by analyzing the data of Social Platforms such as Quora, Facebook, and other question answer websites. The App will also provide suggestions for similar questions and answers.

### FEATURE
* Speech_to_text (Indian Accent too)
* Database(indexing) – Quora API –mongoDB for partial search
* Best recommended answer
* App/Web API


### WHY?
Input can be given directly by using natural speech, eliminating the need of typing the question.
Instead of relevant links it directly provides answers as well as suggests related answers. It saves lots of user time and is very handy in finding the answers on web.

### INNOVATION
Traditional search system are limited to suggesting web links which are relevant to our query or in very few cases direct answers, but as we are more interested in answers rather than web links, this application takes the traditional search to another level, where users will directly provided with answers. This application mainly targets questions that are asked very frequently.

### SYSTEM ORGANIZATION

<figure>
<div class="large">
  <img  src="{{ site.url }}/assets/images/projects/paper/system-design/smartxplorer.png" alt="system design">
  <figcaption>Fig1.1 Overview of the SmartXplorer implementation design</figcaption>
</div>
</figure>

### DEVELOPMENT PLAN
The first step would be to detect the finger position which is to be used then the next would be to connect the movement to the phone screen.
At the end, we would have to accept an user voice input to correct the drawing on some pre-existing objects.


### Equipment Required
The system consist of following hardware modules.
* Microphone for speech detection.
* Smartphone with INTERNET connectivity.
* Database for storing English language words.
* Web crawler for fetching the data from web links.
* Text parser that will store the words in indexed form.

### OUTCOME
At the end of this project, we expect to have a working application that will detect the voice input and display the most relevant answer and suggestion on a nice user interface.

### CREDITS
1. Atul
