---
layout: proj
title: Wanderer
desc: Using Hidden Markov Model to determine patients movements pattern.
---
# Wanderer

<hr>
### INTRODUCTION
Wanderer is an android app that allows anyone to memorialize a moment or a loss that is tied to a specific location by using custom tag and intelligently recommend you what next destination you should go. Anyone can browse the map and all the available tags. The tags can also be used as remembering new location which are not available on the Google map (say your friend place) or any custom location which might be intresting to you.

Over time, the map adds more and more tags on the map and compare it with what other people has tagged at the same location. When it finds, the accuracy of the tags have more than 70% percent(Just a random selection) then it sends this to Google map API server as a request to add the tag. Another feature is: it can give proximity alert for a location and sends push notification when you are that place and what next place you can visit. It uses Hidden Markov Model to predict your next destination.

It also shows the distance in meters the person has traveled to arrive at its current location is displayed under the detailed info. It constantly query Google map API to get nearby locations and keep updating you with that.

### WHY?
The use case for this application was: Solving the patients movement in the hospitals. Hospitals in general experience high financial and operational stress. Adding new physical capacity is often out of question and they are in dire need innovative solutions. One of the solution is Real Time Location System. Hidden Markov Model fits better here because the patients movments are alomost similar and fairly depends on last few movements. 

Hospitals efficiency lies in improving patient flows and throughput by streamlining routine work-flow in hospitals. Monitor patient movement history and activity/inactivity without surveillance solutions. Now days RTLS is also used in Mobile Assets Management i.e. monitoring of theft and misplacement of critical assets.

For Example. One can imagine Hospitals in cities like Mumbai where ratio of nurse to patients is 1:60. It impossible to monitor all of the patients and provide better health-care facilities. The hospitals gives patients a cheap Android devices when they are admitted with Wanderer installed and asks them to carry around. It also provide them reminders and info about their treatment and progress.

### LIMITS
1. We haven't done studies on radiation effect of keeping phone with patients
2. We had studies done a single hostpital with 100 patients and 7 doctors along with 12 nurses.
3. The response we got from doctors were postive as they were able to make informed decision about their own schedules.
4. Patients movements were tracked with their acknowledgement.
5. We hadn't had live tracking system, we have to collect the phone and get the GPX file.


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
    <figcaption>Fig2.4 Next time automatic proximity alerts </figcaption>
  </div>
</figure>

Click <a href="https://www.dropbox.com/s/f4lyjja9b8318i3/wanderer.apk?dl=0" target="_blank">here</a> to download the Android APK.

### MENTOR
1. [Kshitij Marwah](http://www.kshitijmarwah.com/)


### ACRONYMNS
RTLS: RealTime Location Tracking System

