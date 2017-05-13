---
layout: post
title:  Deciphering meaning of NSlayoutConstraints Errors
date:   2017-05-14 10:12:16
desc:   How to debug constraints error
categories:
- iOS
tags:
- AutoLayout
- NSLayoutConstraints
---


Recently, I switched to creating all the UI programmatically in iOS. There are few reasons to support my decision.

- I wanted to learn about the internals of these **UIKit** components and would like to flag it out that this was the most important reason for me. I used to get scared whenever I saw **CGRect**, **Frames** in the code. My brain used to give up thinking that it is not comprehensible. I was unaware about how things get laid out on screen because of lack of basic understanding.

* Though it's great to have Interface Builder to create things using drag and drop which reminds me of Java **Swing** library, I did some **Swing** programming during college in where I used to struggle to customize smaller things like changing **Button** size or making it's corners rounded. It used to make me feel that I don't have control over what I am doing.

* People always ask: Why not **Storyboard** using **Interface Builder**? It is **Apple** recommended way. I agree but there are places where **Storyboards** are not appropriate tools and as a skilled programmer having as many tools as possible is always beneficial.


OK, now the reasons are over. Lets move on to why we are here. I will break the post in three parts.

* I will show an example project in which a Autolayout issue exists
* Now I will explore ways to remove the issues (Feel free to provide your own solution)
* Finally, we will have some learnings to take away 

### Example Project

You can download/checkout the project at [Github](https://github.com/rahulrrixe/nslayoutconstraints-example){:target="_blank"}.

This is a default single page application. I have removed my **Storyboard** file and my *AppDelegate.swift* and *ViewController.swift* files looks like:

```swift
  // As I have removed Storyboard file, I need to
  // set the rootViewController property to root window
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        
        window = UIWindow(frame: UIScreen.main.bounds)
        window?.makeKeyAndVisible()
        
        window?.rootViewController = ViewController()
        
        return true
    }

```

```swift

import UIKit

class ViewController: UIViewController {
    
    
    let titleLabel: UILabel = {
        let label = UILabel()
        label.text = "Testing out NSLayoutConstraints"
        label.backgroundColor = UIColor.blue
        label.textColor = UIColor.white
        label.textAlignment = .center
        label.translatesAutoresizingMaskIntoConstraints = false

        return label
    }()
    

    override func viewDidLoad() {
        super.viewDidLoad()
        
        view.backgroundColor = UIColor.white
        
        setupViews()
    }
    
    func setupViews() {
        view.addSubview(titleLabel)
        
        // Constraints: X, Y, Width, Height
        titleLabel.centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true
        titleLabel.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true
        titleLabel.widthAnchor.constraint(equalTo: view.widthAnchor).isActive = true
        titleLabel.heightAnchor.constraint(equalTo: view.heightAnchor).isActive = true
    }
   
}

```
That's it. We have a *titleText* label which I am trying to set to the center of the view using Autolayout constraints.


This is how the App looks. The **Label** is horizontally and vertically centered. Here is the image

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-05/app_screenshot.png" alt="ScreenShot of the App in simulator">
    <figcaption> ScreenShot of the App in simulator </figcaption>
  </div>
</figure>




## Bugs Injection

Now, let's introduce some bugs 

### 1. **TranslatesAutoresizingMaskIntoConstraints:**  

Remove the **translatesAutoresizingMaskIntoConstraints** from the *titleLabel* view or set it to **false**.

```Swift
label.translatesAutoresizingMaskIntoConstraints = false

```
After running this project I get first error mentioned below in **Error** section and so I set the **translatesAutoresizingMaskIntoConstraints** property correctly and hurray the App is running fine again.

```swift
label.translatesAutoresizingMaskIntoConstraints = false

```

### Error 1
When you haven't set **translatesAutoresizingMaskIntoConstraints** to *false*. You will get constraints error like below in console which looks all the similar to other errors (we will look into them later part of the blog) on first glance.
	
```bash
		2017-05-13 14:26:15.594780+0530 NSLayoutContrainstsExample[41595:4124608] [LayoutConstraints] Unable to simultaneously satisfy constraints.
	Probably at least one of the constraints in the following list is one you don't want. 
	Try this: 
		(1) look at each constraint and try to figure out which you don't expect; 
		(2) find the code that added the unwanted constraint or constraints and fix it. 
	(Note: If you're seeing NSAutoresizingMaskLayoutConstraints that you don't understand, refer to the documentation for the UIView property translatesAutoresizingMaskIntoConstraints) 
(
    "<NSAutoresizingMaskLayoutConstraint:0x6000000940a0 h=--& v=--& UILabel:0x7f9659605cc0'Testing out NSLayoutConst...'.width == 0   (active)>",
    "<NSLayoutConstraint:0x608000095860 UILabel:0x7f9659605cc0'Testing out NSLayoutConst...'.width == UIView:0x7f96597030a0.width   (active)>",
    "<NSLayoutConstraint:0x600000096da0 'UIView-Encapsulated-Layout-Width' UIView:0x7f96597030a0.width == 320   (active)>"
)
```

The things you need to look is **h=--& v=--&**, if it is there then the error is because you haven't set the *translatesAutoresizingMaskIntoConstraints* property to false. For info read Apple guide [here](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/AutolayoutPG/DebuggingTricksandTips.html#//apple_ref/doc/uid/TP40010853-CH21-SW1){:target="_blank"}.


### 2. **Unsatisfiable constraints:** 

Now lets create a bug in Autolayout constraints. Currently the **width** of the **titleLabel** is fixed to it's **SuperView** width. Let's make another constraints with a constant greater than **SuperView's** width. In code which will look something like below.

```swift
let viewWidth = view.frame.width
let titleLabelWidth = viewWidth + 100
        
// Constraints: X, Y, Width, Height
titleLabel.centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true
titleLabel.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true
titleLabel.widthAnchor.constraint(equalTo: view.widthAnchor).isActive = true

// Added this extra constant
titleLabel.widthAnchor.constraint(equalToConstant: titleLabelWidth).isActive = true

titleLabel.heightAnchor.constraint(equalTo: view.heightAnchor).isActive = true
```

Now I get an error, why because initially we have set the **width** of *titleLabel* to its *SuperView* width but now we have extra constraints which says it's width have constant value which doesn't satisfy the previous constraints.

### Error 2 

**Note:** Because you know the reason why we are getting the error, it makes it easy but in real world the scenario will be different. You will have many views and will not know what is causing the error.

```bash
2017-05-13 15:20:08.740153+0530 NSLayoutContrainstsExample[43393:4192925] [LayoutConstraints] Unable to simultaneously satisfy constraints.
	Probably at least one of the constraints in the following list is one you don't want. 
	Try this: 
		(1) look at each constraint and try to figure out which you don't expect; 
		(2) find the code that added the unwanted constraint or constraints and fix it. 
(
    "<NSLayoutConstraint:0x60800008c4e0 UILabel:0x7fbbc95067b0'Testing out NSLayoutConst...'.width == UIView:0x7fbbc9506a40.width   (active)>",
    "<NSLayoutConstraint:0x60800008c580 UILabel:0x7fbbc95067b0'Testing out NSLayoutConst...'.width == 420   (active)>",
    "<NSLayoutConstraint:0x600000089a10 'UIView-Encapsulated-Layout-Width' UIView:0x7fbbc9506a40.width == 320   (active)>"
)

Will attempt to recover by breaking constraint 
<NSLayoutConstraint:0x60800008c580 UILabel:0x7fbbc95067b0'Testing out NSLayoutConst...'.width == 420   (active)>

Make a symbolic breakpoint at UIViewAlertForUnsatisfiableConstraints to catch this in the debugger.
The methods in the UIConstraintBasedLayoutDebugging category on UIView listed in <UIKit/UIView.h> may also be helpful.
```

Does the log make sense?

Let me pin out a few points here:

* It is talking about a **UILabel** but I don't know whether it is *titleLabel* or some other one.
* Which particular constraints it is breaking, we can have multiple width constraints.
* The last line which is **Will attempt to recover by breaking constraint ...** means Autolayout engine will discard this constraint. 


Let resume our discussion, the biggest problem in debugging **NSLayoutConstraints** is finding the correct view. **Xcode** uses a label’s text, a button’s title, or a text field’s placeholder to identify these views and so we are able to find that this constraint belong to *titleLabel* as

```bash
<NSLayoutConstraint:0x60800008c4e0 UILabel:0x7fbbc95067b0'Testing out NSLayoutConst...'.width == UIView:0x7fbbc9506a40.width   (active)>"
```
Focus on **Testing out NSLayoutConst...'** which is the text we have setup on *titleLabel*. Hence most of the views can be found out using this way.


> What about the other views?

**Symbolic breakpoints** are here for rescue. The error log say 

```
Make a symbolic breakpoint at UIViewAlertForUnsatisfiableConstraints to catch this in the debugger.
The methods in the UIConstraintBasedLayoutDebugging category on UIView listed in <UIKit/UIView.h> may also be helpful.
```

when I was looking for how to create **symbolic breakpoints**, I tried everything but no success, then as always [stackOverflow](http://stackoverflow.com/questions/26389273/how-to-trap-on-uiviewalertforunsatisfiableconstraints){:target="_blank"} comes for rescue. 

This post also started assuming I know how to create breakpoints. Finally I found the crux i.e.

* Goto Breakpoint Navigator **cmd+7**
* Click the Add (+) button in the lower left corner
* Select Add Symbolic Breakpoint from the option
* Where it says Symbol just type in **UIViewAlertForUnsatisfiableConstraints**

The steps are shown in the figure below.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-05/breakpoint-1.png" alt="How to set symbolic breakpoint">
    <figcaption> 1. How to set symbolic breakpoint </figcaption>
  </div>
</figure>

<figure>
  <div class="medium">
    <img src="{{ site.url }}/assets/images/posts/2017-05/breakpoint-2.png" alt="Select Symbolic Breakpoint">
    <figcaption> 2. Select Symbolic Breakpoint </figcaption>
  </div>
  <div class="medium">
    <img src="{{ site.url }}/assets/images/posts/2017-05/breakpoint-3.png" alt="Add the correct class">
    <figcaption> 3. Add the correct class </figcaption>
  </div>
</figure>

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-05/breakpoint-4.png" alt="Final breakpoint view ">
    <figcaption> 4. Final breakpoint view </figcaption>
  </div>
</figure>


After adding this break point, you can use few method to get the description about a view. As I said, identifying correct view is the biggest hurdle.

```bash
(lldb) po 0x7ff7a0c093c0
<UILabel: 0x7ff7a0c093c0; frame = (0 0; 0 0); text = 'Testing out NSLayoutConst...'; userInteractionEnabled = NO; layer = <_UILabelLayer: 0x600000083c00>>

(lldb) po [0x7ff7a0c093c0 recursiveDescription]
<UILabel: 0x7ff7a0c093c0; frame = (0 0; 0 0); text = 'Testing out NSLayoutConst...'; userInteractionEnabled = NO; layer = <_UILabelLayer: 0x600000083c00>>

(lldb) po [0x7ff7a0c093c0 superview]
<UIView: 0x7ff7a0c050b0; frame = (0 0; 320 568); autoresize = W+H; layer = <CALayer: 0x600000222000>>

```


### 3. **Ambiguous Layout:** 

The above issue was about adding extra constraints (Unsatisfiable constraints) which can be discarded but what about ambiguous constraints.

[Ambiguous layouts](Ambiguous Layout) occur when the system of constraints has two or more valid solutions. There are two main causes:

* The layout needs additional constraints to uniquely specify the position and location of every view.
* After you determine which views are ambiguous, just add constraints to uniquely specify both the view’s position and its size.
* The layout has conflicting optional constraints with the same priority, and the system does not know which constraint it should break.
* Here, you need to tell the system which constraint it should break, by changing the priorities so that they are no longer equal. The system breaks the constraint having the lowest priority first.


Now, we will add a **Ambiguous** constraints. We can easily do in our project example by removing **Y** position constraint.

```swift
// titleLabel.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true
```


### Error 3

The console prints out this:

```bash
2017-05-13 17:20:42.834543+0530 NSLayoutContrainstsExample[45035:4345694] [LayoutConstraints] Unable to simultaneously satisfy constraints.
	Probably at least one of the constraints in the following list is one you don't want. 
	Try this: 
		(1) look at each constraint and try to figure out which you don't expect; 
		(2) find the code that added the unwanted constraint or constraints and fix it. 
(
    "<NSLayoutConstraint:0x600000091260 UILabel:0x7fd720e04230'Testing out NSLayoutConst...'.width == UIView:0x7fd720c07680.width   (active)>",
    "<NSLayoutConstraint:0x600000091300 UILabel:0x7fd720e04230'Testing out NSLayoutConst...'.width == 420   (active)>",
    "<NSLayoutConstraint:0x6000000911c0 'UIView-Encapsulated-Layout-Width' UIView:0x7fd720c07680.width == 320   (active)>"
)

Will attempt to recover by breaking constraint 
<NSLayoutConstraint:0x600000091300 UILabel:0x7fd720e04230'Testing out NSLayoutConst...'.width == 420   (active)>

Make a symbolic breakpoint at UIViewAlertForUnsatisfiableConstraints to catch this in the debugger.
The methods in the UIConstraintBasedLayoutDebugging category on UIView listed in <UIKit/UIView.h> may also be helpful.

```

The above error is same weired jargon which we have seen with **Unsatisfiable constraints** and not telling about the ambiguity. 

***Now what to do?*** 

From the [StackOverFlow](http://stackoverflow.com/questions/26389273/how-to-trap-on-uiviewalertforunsatisfiableconstraints){:target="_blank"} post mentioned above, we can also add **Debugger Command** in the symbolic breakpoint to show whole trace of views.

```bash
expr -l objc++ -O -- [[UIWindow keyWindow] _autolayoutTrace]
```

Now console logs the **Error 3** in below format:

```bash
•UIWindow:0x7fdb69d06bb0
|   •UIView:0x7fdb69e09f10
|   |   *UILabel:0x7fdb69d00f90'Testing out NSLayoutConst...'- AMBIGUOUS LAYOUT for UILabel:0x7fdb69d00f90'Testing out NSLayoutConst...'.minY{id: 25}

Legend:
	* - is laid out with auto layout
	+ - is laid out manually, but is represented in the layout engine because translatesAutoresizingMaskIntoConstraints = YES
	• - layout engine host
```


The above issue is understandable. It is saying we haven't provided the **Y** value.

I think, this is a good stopping point. I will explore more on debugging Autolayout issue for complex views in later posts.

I would love to have your feedback. Please write it in the comments.



[Ambiguous Layout]: <https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/AutolayoutPG/AmbiguousLayouts.html>


