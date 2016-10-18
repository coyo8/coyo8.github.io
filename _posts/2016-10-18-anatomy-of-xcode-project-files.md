---
layout: post
title:  "Anatomy of Xcode Project files"
date:   2016-10-18 22:48:45
description: Learn what each Xcode project files means.
categories:
- iOS
tags:
- Xcode
- iOS
- App Development
---

I started developing iOS apps again and I found myself struggling with all nitty-gritty aspects of Xcode environment. This will be a short guide to know things before you start the app development.

I will be taking project **Falcon** as demo and the content of it can be seen in below snapshot.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2016-10/cmd-file.png" alt="Project file snapshots">
  </div>
</figure>

<figure>
  <div class="small">
    <img src="{{ site.url }}/assets/images/posts/2016-10/project-file.png" alt="Xcode project explorer">
  </div>
</figure>

### Key Concepts

**Targets**

It specify in detail how a product/binary is built. They include build settings, such as compiler and linker flags, and they define which files (source code and resources) actually belong to a product. When you build/run, you always select one specific target.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2016-10/target.png" alt="Target">
  </div>
  <figcaption> Each target have it's own setting </figcaption>
</figure>

In above figure you can see that we have three targets.

* Falcon
* FalconTests
* FalconUITests

All these three target will have different settings.

**projects**

Now, it is very likely that we will have multiple targets and they will share common resources. So we will need to group them these related target and that is what a project is.

In above example Falcon is a project.

**workspaces**

Guess, what is workspaces then? Workspaces contain and manage projects. All the directly included projects  are on the same level and their targets can depend on each other. So let suppose if I add a new project

<figure>
  <div class="small">
    <img src="{{ site.url }}/assets/images/posts/2016-10/workspace.png" alt="Target">
  </div>
  <figcaption> Another Application is different project added to Falcon workspace </figcaption>
</figure>

### Takeaways

* Most of the time project scope is sufficient.

Now you can easily figure out why [CocoaPods](http://www.cocoapods.org/){:target="_blank"} uses `workspaces`. They manage third party libraries or projects for us.

Now let move on to Xcode files.


### Xcode Files

*All the Xcode file **location** is with respect to the root folder of the project.*

**.pbxproj**

`Location: {{your-app-name}}.xcodeproj/{{your-app-name}}.pbxproj`

PBXPROJ is an Xcode data file that saves all the project project data such as the list of source code, resource files, and build properties.

> It is a critically important file.

The biggest challenge comes when you are working in a team and fix the merge conflict arising due to distribute changes. Unfortunately, there's not much you can do except to make the changes manually.

The Xcode team has put a lot of effort into making the file merge-friendly. In managing several large projects via SVN, I've generally found that the merges are automatic and painless.

People have tried [automating](https://gist.github.com/xslim/1790379){:target="_blank"} it but I wouldn't not recommend until you check manually whether it is working fine or not.

***Should I add it to .gitignore?***

NO

**.xcscheme**

`Location: {{your-app-name}}.xcodeproj/xcuserdata/{{computer-user-name}}.xcuserdatad/xcschemes/{{your-app-name}}.xcscheme`

Instead of just ignoring the scheme file, you can ignore whole folder

```
# Exclude personal Xcode user settings
xcuserdata/
```

***Should I add it to .gitignore?***

YES

**.xcworkspacedata**

`Location: {{your-app-name}}.xcworkspace/`

A workspace is XML document which contains data of projects groups and other documents so you can work on them together. It can contain any number of Xcode projects, plus any other files you want to include. In addition to organizing all the files in each Xcode project, a workspace provides implicit and explicit relationships among the included projects and their targets. For example. The Falcon project workspace file looks like this.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Workspace
   version = "1.0">
   <FileRef
      location = "group:Falcon.xcodeproj">
   </FileRef>
   <FileRef
      location = "group:Pods/Pods.xcodeproj">
   </FileRef>
</Workspace>
```
From above, it can inferred that workspace is trying to keep the reference for Falcon and Pods projects.

***Should I add it to .gitignore?***

NO and YES if you are not using CocoaPods

At last I will recommend to go through the [official documentation](https://developer.apple.com/library/content/featuredarticles/XcodeConcepts/Concept-Targets.html){:target="_blank"} to learn more about above files.

Let me know if above content helped you!

### References

[1] [Xcode Project File Format](http://www.monobjc.net/xcode-project-file-format.html){:target="_blank"}.





