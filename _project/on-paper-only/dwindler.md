---
layout: proj
title: dwindler
---

# Dwindler

<hr>
### INTRODUCTION

Dwindler aims at automating the switches in common household and universities. It plans to save electricity by selective power distribution to the region where the user is present.It is a system based on RFIDs [1]  which aims on saving electricity.A person can enter the room/lab by tapping his/her unique ID[2]  at the RFID detector mounted at the entrance of room.Within few seconds his/her system along with all the lights and fans in his area are switched on.There will also be a provision for his/her system remaining on till a specific time say 10 minutes, This system allows only specified people access to the lab which can avoid unauthorised people from accessing the lab.It can also be used to eradicate the pen-paper entry system in various buildings and can be used for authentication purpose.

### FEATURES
* Person Authentication: UID, identify person
* Attendance, Log of time of use of systems
* Result, comparison of normal usage and reduced usage, analysis
* Manual override: Functionality for keeping system on
* Safe shutdown with admin (root access) (Optional)

### BENEFITS OF PROJECT

The project aims at saving huge chunks of power that is wasted to light up some homes in  a village. It is a win-win for both, mother nature and cost reduction on the end of the user.

### INNOVATION

RFID has been used for authentication purposes but its utility has not been exploited in energy saving applications. Most appliances aim at making device more efficient to save power. We plan to automate their usage time to save the power.

### PRINCIPLES OF OPERATION:

RFID reader will detect the unique person and pass the information to the controller. The controller has a look up table that has the data of where the person sits in a lab.It turns on the power (Socket, lights and fans) for that section of the room. It keeps a track of the user’s session . It issues a lease (For say an hour) and checks whether the person has left the room after timeout. If the lease is not re-issued (By tapping on the RFID reader), It will initiate shutdown of the appliances in that area Appropriate options will be given in case the user chooses to end the session early.

### DEVELOPMENT PLAN

We will first experiment with a couple RFID tag and readers and make a small database.We would then play around with switches like SCR[3] to control the triggering of various appliances.Then we would interface a controller in between the two developed systems  and map a RFID tag with particular switches .Finally, we plan to model the prototype with a 240 Volts AC[4] supply.

### SYSTEM ORGANIZATION

<figure>
<img  src="{{ site.url }}/assets/images/projects/paper/system-design/dwindler.png" alt="system design">
<figcaption>Fig1.1 Overview of the Dwindler design</figcaption>
</figure>

### Equiptments

*   RFID Tag and Reader
*   Microcontroller board
*   SCR and other various components (wire, breadboard etc.)

### OUTCOMES

By the end of the project, we expect to have a working prototype that models the problem statement . We hope the model would be easily adoptable for ready and direct use in the regular household and laboratories.

### DEFINITIONS/ACRONYMS

1. RFID : Radio-frequency identification.
2. ID : Identity
3. SCR : Silicon Controlled Rectifier.
4. AC : Alternating Current.

### CREDITS
1. Yatharath
2. Medhavi