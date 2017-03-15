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

This is a story about Swifty who is a god programmer at Swiftzen planet. On this planet, he is regarded as one of the greatest programmer ever born. He can code anything within minutes. He has also won planet's biggest coding competition on DNA sequencing by solving it within a minute. Swifty's recent work is on inter planet communication and one day he received a message **"♍︎♈︎♨︎♒︎♇✜"** on his screen. He was not able to decipher these weired shapes and so he decided to make changes in his program to display them in known shapes.

Now, this is the first time Swifty was trying to extend the functionality of the program, till now almost all of his work was on frozen programs.

> Walking on water and developing software from a specification are easy if both are frozen.

-- Edward V. Berard


Later on this journey we will learn how Swifty was able to conquer and create a software which can withstand the test of time.

### Single Responsibility Principle

Let's take a look into Swifty's communication program.

```swift
import Foundation

class InterPlanetMessageReceiver {

    func receiveMessage() {
        print("Received the Message!")
    }

    func displayMessageOnGUI() {
      print("Displaying Message on Screen!")
    }
}
```
Now let's understand what is `Single Responsibility Principle(SRP)` and how the above program doesn't obey it.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/srp.png" alt="Single Responsibility Principle">
  </div>
</figure>

SRP says, "Just because you can implement all the features in a single device, you shouldn't".

In Object Oriented terms it means: ***There should never be more than one reason for a class to change.*** It doesn't mean you can't have multiple methods but the only condition is that they should have one single purpose.

**Why?**
Because it adds a lot of manageability problems for you in the long run.


<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/interplanet.png" alt="Single Responsibility Principle">
    <figcaption> Class hierarchy </figcaption>
  </div>
</figure>

Here, the *InterPlanetMessageReceiver* class does the following:

* It receives the message.
* It renders it on UI.

And, two applications are using this *InterPlanetMessageReceiver* class:

* A messaging application uses this class to receive the message
* A graphical application uses this class to draw the message on the UI

Do you think it is violating the SRP?

**YES**

The InterPlanetMessageReceiver class is actually performing two different things. First, it handles the messaging, and second, displaying the message on GUI. This causes some interesting problems:

1. Swifty must include the GUI into the messaging application and also while deploying the messaging application, we must include the GUI library.
2. A change to the InterPlanetMessageReceiver class for the graphical application may lead to a change, build, and test for the messaging application, and vice-versa.

Swifty got frustrated with the amount of changes it required. He thought it would be a minute job but now he has already spent hours on it. So he decided do make a change into his program and fix this dependency.

This is what Swifty came up with

```swift
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

Here's how Swifty explained this:

InterPlanetMessageReceiver class will be used by the messaging application, and the InterPlanetMessageDisplay class will be used by the graphical application. We could even separate the classes into two separate files, and that will allow us not to touch the other in case a change is needed to be implemented in one.

Finally, Swifty noted down on his online journal.

Why we need SRP?
* Each responsibility is an agent of change.
* Code becomes coupled if classes have more than one responsibility.


### Open-Close Principle
Swifty was quite happy with these change and later he celebrated it with a drink in Swiftzen's best pub and there his eyes fell upon an artifact hanging on the front wall and he found all the symbols he received in the message. Quickly, he opened his diary and completed deciphering all those shapes. It looks like this

* ♍︎ = ▢
* ♈ = ▭
* ♨ = ⊖
* ♒ = △
* ♇ = ☆
* ✜ = ⌓

These were all geometric shapes. Next day when he returned back, he thought why not fix the DrawGraphic class which draws only circle shape, to include the rest of the shapes and display the message correctly.


```swift

// This is the DrawGraphic
class DrawGraphic {

  func drawShape() {
     print("Circle is drawn!")
  }
}

// Updated Class code

enum Shape {
  case circle
  case rectangle
  case square
  case triangle
  case pentagon
  case semicircle
}
class circle {

}

// This is the DrawGraphic
class DrawGraphic {

  func drawShape(shape: Shape) {
     switch shape {
        case .circle:
          print("Circle is drawn")
        case .rectangle:
          print("Rectangle is drawn")
        case square:
          print("Square is drawn")
        case triangle:
          print("Triangle is drawn")
        case pentagon:
          print("Pentagon is drawn")
        case semicircle:
          print("Semicircle is drawn")
        default:
          print("Shape not provided")
     }
  }
}
```

<figure>
  <div class="small">
    <img src="{{ site.url }}/assets/images/posts/2017-03/shape.png" alt="Open Close Principle">
    <figcaption> Showing concrete relation between Shape and DrawGraphic </figcaption>
  </div>
</figure>

Swifty was not happy with these changes, what if in future a new shape shows up, after all he saw in the artifacts that there were around 123 shapes. This class will become one fat class. Also, **DrawGraphics** class is used by other applications and so they also have to adapt to this change. it was nightmare for Swifty.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/ocp.png" alt="Open Close Principle">
  </div>
</figure>

Open Closed Principle says **Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.** At the most basic level, this means, you should be able to extend a class behavior without modifying it. It's just like I should be able to put on a dress without doing any change to my body. Imagine what would happen if for every dress I have to change my body.

After hours of thinking, Swifty came up with below implementation of DrawGraphic class.

```swift

protocol Draw {
    func draw()
}

class Circle: Draw {
    func draw() {
        print("Circle is drawn!")
    }
}

class Rectangle: Draw {
    func draw() {
        print("Rectangle is drawn!")
    }
}

class DrawGraphic {
    func drawShape(shape: Draw) {
        shape.draw()
    }
}

let circle = Circle()
let rectangle = Rectangle()
let drawGraphic = DrawGraphic()

drawGraphic.drawShape(shape: circle)  // Circle is drawn!
drawGraphic.drawShape(shape: rectangle) // Rectangle is drawn!

```

Since the DrawGraphic is responsible for drawing all the shapes, and because the shape design is unique to each individual shape, it seems only logical to move the drawing for each shape into its respective class.

<figure>
  <div class="medium">
    <img src="{{ site.url }}/assets/images/posts/2017-03/draw.png" alt="Open Close Principle">
    <figcaption> Showing correct implementation of Open Closed Principle </figcaption>
  </div>
</figure>


Hmmm, but that means the DrawGraphic still have to know about all the shapes, right? Because how does it know that the object it’s iterating over has a draw method? Sure, this could be solved with having each of the shape classes inherit from a protocol: the Draw protocol (this can be an abstract class too):

Circle and Rectangle classes holds a reference to the protocol, and the concrete DrawGraphic class implements the protocol Draw class. So, if for any reason the DrawGraphic implementation is changed, the Circle and Rectangle classes are not likely to require any change or vice-versa.


### Liskov Subsitution Principle

Swifty was wondering why he never learned all these before. Then he remember the quote

> Necessity is the mother of invention.

He can now feel the code smell. Moving ahead, Swifty was implementing the SenderOrigin class to know whether the sender is from a Planet or not.

You can learn more about definition of planet [here](http://en.wikipedia.org/wiki/IAU_definition_of_planet){:target="_blank"}.

The Sender class looked something like this

```swift

Class Planet {
  func orbitAroundSun() {
  }
}

class Earth: Planet {
  func description() {
    print("It is Earth!")
  }
}

class Pluto: Planet {
  func description() {
    print("It is Pluto!")
  }
}

class Sender {
  func senderOrigin(planet: Planet) {
    planet.description()
  }
}

```
So, even if in real world this seems natural, in the class design, Pluto should not inherit the Planet class because it is a dwarf planet, and there should be a separate class for Planet that has not cleared the neighborhood around its orbit and Pluto should inherit that.

<figure>
  <div class="medium">
    <img src="{{ site.url }}/assets/images/posts/2017-03/planet.png" alt="Liskov Subsitution Principle">
  </div>
  <figcaption>Pluto is dwarf planet not a planet</figcaption>
</figure>

Now let's describe Liskov Substitution Principle

***"Subtypes must be substitutable for their base types."***

Or, if said differently:

Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/lsp.png" alt="Liskov Subsitution Principle">
  </div>
</figure>

Swifty whispered it is the polymorphism. Yes it is. "Inheritance" is usually described as an "is a" relationship. If a "Planet" is a "Dwarf", then the "Planet" class should inherit the "Dwarf" class. Such "Is a" relationships are very important in class designs, but it's easy to get carried away and end up with a wrong design and a bad inheritance.

The "Liskov's Substitution Principle" is just a way of ensuring that inheritance is used correctly.

In the above case, both Earth and Pluto can orbit around the Sun but Pluto is not a planet. It has not cleared the neighborhood around its orbit. Swifty understood this and changed the program.

```swift

class Planet {
    func oribitAroundSun() {
        print("This planet Orbit around Sun!")
    }
}

class Earth: Planet {
    func description() {
        print("Earth")
    }
}

class DwarfPlanet: Planet {
    func notClearedNeighbourhoodOrbit() {

    }
}

class Pluto: DwarfPlanet {
  func description() {
        print("Pluto")
    }
}

class Sender {
    func senderOrigin(from: Planet) {
        from.description()
    }
}

let pluto = Pluto()
let earth = Earth()

let sender = Sender()
sender.senderOrigin(from: pluto) // Pluto
sender.senderOrigin(from: earth) // Earth

```
<figure>
  <div class="medium">
    <img src="{{ site.url }}/assets/images/posts/2017-03/planet-2.png" alt="Liskov Subsitution Principle">
  </div>
  <figcaption>Correct Inheritance Order following LSP </figcaption>
</figure>

Here, Pluto inherited the planet but added the notClearedNeigbourhood method which distinguishes a dwarf and regular planet.

* If LSP is not maintained, class hierarchies would be a mess, and if a subclass instance was passed as parameter to methods, strange behavior might occur.
* If LSP is not maintained, unit tests for the base classes would never succeed for the subclass.

Swifty can design objects and apply LSP as a verification tool to test the hierarchy whether inheritance is properly done.


### Interface Segregation Principle

Swifty was quite astonished with the improvement in his program. All the changes were making more sense. Now, it was time to share this code with different planet. Swiftzen 50% GDP was dependent on selling softwares and many planet has requested and signed MOU for the Inter Planet communication system.

Swifty was ready to sell the program and but he was not satisfied with current client interface. Let's us look into it.

```swift

protocol interPlanetCommunication {
  func switchOnAntenna()
  func setAntennaAngle()
  func transmitMessage()
  func receivedMessage()
  func displayMessageOnGUI()
}
```
Now for anyone who want to use interPlanetCommunication, he has to implement all the five methods even-though they might not required.

Here comes the Interface Segregation principle.
***"Clients should not be forced to depend upon interfaces that they do not use."***

In more simple term: Many client-specific interfaces are better than one general purpose interface.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/isp.png" alt="Interface Segregation Principle">
  </div>
</figure>

The Interface Segregation principle ensures that Interfaces are developed so that each of them have their own responsibility and thus they are specific, easily understandable, and re-usable.

Swifty quickly made changes to his program interface:

```swift

protocol antenna {
  func switchOnAntenna()
  func setAntennaAngle()
}

protocol message {
  func transmitMessage()
  func receivedMessage()
}

protocol dispaly {
  func displayMessageOnGUI()
}

```

### Dependency Inversion Principle

Before finally shipping the program to all the clients, Swifty was trying to fix the password reminder class which looks like this

```swift
class PasswordReminder {
  func connectToDatabase(db: SwiftZenDB) {
    print("Database Connected to SwiftzenDB")
  }

  func sendReminder() {
    print("Send Reminder")
  }
}

```
PasswordReminder class is dependent on a lower level module i.e. database connection. Now, let suppose that you want to change the database connection from Swiftzen to Objective-Czen, you will have to edit the PasswordReminder class.

Finally the last principle, Dependency Inversion principle states that
***"High level modules should not depend upon low level modules. Rather, both should depend upon abstractions."***

Or in other terms "Entities must depend on abstractions not on concretions."

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/dip.png" alt=" Dependency Inversion Principle">
  </div>
</figure>

To fix above program Swifty made these changes

```swift

protocol DBConnection {
  func connection()
}

class SwiftzenDB: DBConnection {
  func connection() {
    print("Connected to SwiftzenDB")
  }
}

class PasswordReminder {
  func connectToDatabase(db: DBConnection) {
    db.connection()
  }

  func sendReminder() {
    print("Send Reminder")
  }
}

```
The DBConnection protocol has a connection method and the SwiftzenDB class implements this protocol, also instead of directly type-hinting SwiftzenDB class in PasswordReminder, Swifty instead type-hint the protocol and no matter the type of database your application uses, the PasswordReminder class can easily connect to the database without any problems and OCP is not violated.

The point is rather than directly depending on the SwiftzenDB, the passwordReminder depends on the abstraction of some specification of Database so that if any the Database conforms to the abstraction, it can be connection with the PasswordReminder and it will work.


#### Info
📖 Descriptions from: [The Principles of OOD by Uncle Bob](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod){:target="_blank"}
