---
layout: proj
title: Wanderer
---
# Wanderer

<hr>
### ABSTRACT
Wanderer is an android app that allows anyone to memorialize a moment or a loss that is tied to a specific location by a tag. Anyone can browse the map and its submitted tags. The tags can also be used as remembering new location which are not available on the google map (say your friend place)

Over time, the map adds more tags on the map and compare with what other people has tagged at the same location. When it finds, the accurancy of the tagged it, it sends this to google map api server as a request to add the tag. Another feature is it can proximity alert for a location and sends push notification when you are that place.

It also shows the distance in meters the person has traveled to arrive at its current location is displayed under its text. It constantly query google map api to get nearby locations and keep updating you with that.

### WHY?
Hospitals in general experience high financial and operational stress. Adding new physical capacity is often out of question and they are in dire need innovative solutions. One of the solution is Real Time Location System.

Hospitals effeciency lies in improving patient flows and throughput by streamlining routine workflow in hospitals. Monitor patient movement history and activity/inactivity without surveillance solutions. Now days RTLS is also used in Mobile Assets Management i.e. monitoring of
theft and misplacement of critical assets.

For Example. One can imagine Hospitals in cities like Mumbai where ratio of nurse to patients is 1:60. It impossible to monitor all of the patients and provide better healthcare facilities. I think that most of the problem can be solved by using RTLS.

Wanderer has been made to solve above problem using mobile phones integrated with GPS.

### SNAPSHOTS
<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/projects/research/hmm/patient-movement2.png" alt="system design">
    <figcaption>Fig1.1 Patient initial movements near hospital</figcaption>
  </div>
  <div class="large">
    <img src="{{ site.url }}/assets/images/projects/research/hmm/patient-movement1.png" alt="system design">
    <figcaption>Fig1.2 Patient 3 days tracking movement details</figcaption>
  </div>
</figure>

### ANDROID APP
<figure>
  <div class="small">
    <img src="{{ site.url }}/assets/images/projects/research/hmm/1.png" alt="system design">
    <figcaption>Fig2.1 Showing nearby Point of Interest (POI) </figcaption>
  </div>
  <div class="small">
    <img src="{{ site.url }}/assets/images/projects/research/hmm/2.png" alt="system design">
    <figcaption>Fig2.2 If user comes nearby POI, a even triggers </figcaption>
  </div>
  <div class="small">
    <img src="{{ site.url }}/assets/images/projects/research/hmm/3.png" alt="system design">
    <figcaption>Fig2.3 User location saved in database </figcaption>
  </div>
  <div class="small">
    <img src="{{ site.url }}/assets/images/projects/research/hmm/4.png" alt="system design">
    <figcaption>Fig2.4 Next time automic proximity alerts </figcaption>
  </div>
</figure>

Click <a href="{{ site.url }}/assets/apps/wanderer.apk" target="_blank">here</a> to download the Android APK.

### MENTOR
1. [Kshitij Marwah](http://www.kshitijmarwah.com/)


### ACRONYMNS
RTLS: RealTime Location Tracking System

