---
layout: post
title:  SOLID Principles In Swift
date:   2017-03-14 10:12:16
desc:   Learn how to apply SOLID principle in Swift
categories:
- iOS
tags:
- Swift
- Design Principles
---

This is story about Swifty who is like a god programmer at Swiftzen planet. On his planet, he is regarded as one of the greatest programmer ever born. He can code anything within minute. He also won the planet highest competition on coding DNA sequencing within a minute. Swifty recent work was on inter planet communication and one day finally he received a message "♍︎♈︎♨︎♒︎♇✜" on his screen. He was not able to decipher these weired shape and so he decided to make changes to his program to display it correctly.

Now, this is the first time Swifty was trying to extend the functionality of the program, till now almost all of his work were on frozen programs.

> Walking on water and developing software from a specification are easy if both are frozen.

-- Edward V. Berard


Later on this journey we will learn how swifty was able to conquer create a software which can withstand the test of time.

#### Single Responsibility Principle

Let first take a look into Swifty's communication program.

```
import Foundation

class InterPlanetMessageReceiver {

    func receive() {
        print("Received the Message!")
    }

    func displayMessageOnGUI() {
      print("Displaying Message on Screen!")
    }
}
```
Now let's understand what is Single Responsibilty Principle and how above program doesn't obey it.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/srp.png" alt="Single Responsibility Principle">
  </div>
</figure>
SRP says, "Just because you can implement all the features in a single device, you shouldn't".

**Why?**
Because it adds a lot of manageability problems for you in the long run.

In Object Oriented terms it means: ***There should never be more than one reason for a class to change.*** it doesn't mean you can't have multiple methods but only condition is they should meet one single purpose.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/interplanet.png" alt="Single Responsibility Principle">
    <figcaption> Class hierarchy </figcaption>
  </div>
</figure>

Here, the *InterPlanetMessageReceiver* class does the following:

* It send receive the message.
* It renders it on UI.

And, two applications are using this *InterPlanetMessageReceiver* class:

* A messaging application uses this class to receive the message
* A graphical application uses this class to draw the message on the UI

Do you think it is violeting the SRP?

**YES**

The InterPlanetMessageReceiver class is actually performing two different things. First, it handles the messaging, and then displaying the message on GUI. This causes to some interesting problems:

1. Swifty must include the GUI into the messaging application and also while deploying the messaging application, we must include the GUI library.
2. A change to the InterPlanetMessageReceiver class for the graphical application may lead to a change, build, and test for the messaging application, and vice-versa.

Swifty was frustrated with the amount to changes it required. He thought it would be a minute job but now he has already spends hours on it. So he decided do make a change into his program and fix this dependency.

This is what Swifty came up with

```
import Foundation

// Handles received message
class InterPlanetMessageReceiver {

    func receive() {
        print("Received the Message!")
    }
}

// Handles the display part
class InterPlanetMessageDisplay {

    func displayMessageOnGUI() {
      print("Displaying Message on Screen!")
    }
}

```

Here how Swifty explained to his colleague:

InterPlanetMessageReceiver class will be used by the messaging application, and the InterPlanetMessageDisplay class will be used by the graphical application. We could even separate the classes into two separate files, and that will allow us not to touch the other in case a change is needed to be implemented in one.

Finally Swifty noted down on his online journal.

Why we need SRP?
* Each responsibility is an agent of change.
* Code becomes coupled if classes have more than one responsibility.


#### Open-Close Principle
<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/ocp.png" alt="Open Close Principle">
  </div>
</figure>

#### Liskov Subsitution Principle
<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/lsp.png" alt="Liskov Subsitution Principle">
  </div>
</figure>

#### Interface Segregation Principle
<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/isp.png" alt="Interface Segregation Principle">
  </div>
</figure>

#### Dependency Inversion Principle
<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/dip.png" alt=" Dependency Inversion Principle">
  </div>
</figure>

