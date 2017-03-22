---
layout: post
title:  Exploring concurrency in iOS and in general
date:   2017-03-21 10:12:16
desc:   Learn what iOS offer to make your programs concurrent
categories:
- iOS
tags:
- GCD
- Concurrency
---

Let me introduce you to Bob, he is currently enjoying post-retirement days of his life after spending years working on computer chips. He has seen transition of transistors from centimeters to nanometers. He still uses his **Pentium pro (232 MHz)** running Windows 95 for most of his tasks which includes writing and do you know why? you will come to know later.

Want to know how Bob computer looks like, check out the below video.

<div class="videowrapper">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/3STKYEBTiFU" frameborder="0" allowfullscreen></iframe>
</div>

His best friend Rob was coming to visit him in the afternoon. They were meeting after a year as Rob went to a different country for his software assignment. Finally, the time has come when Rob arrived. He was very excited to see Bob's old machine is still working. Contrary to Bob, Rob is a tech fanatics, he likes new machines and updated softwares. He upgrades to the new version as soon as they get launched and uses it to flaunt. Recently when iPhone 7 launched, he became the first customer to own it.

*Rob asked Bob why are you still stuck with this old computer?*

Bob replied: I hate multitasking!

> To do two things at once is to do neither

--Publilius Syrus

Rob was not surprised with his reply, after all, he has known Bob for years. He is a kind of a person who immerses himself into one thing and doesn't want any distractions. His old machine helps him to achieve it at a great level by not providing swift multitasking at first place. Finally, Rob saw an article "Threading Vs Concurrency". Rob told Bob that concurrency is same as threading and Parallelism.

Bob replied: **No.** A code is concurrent if it is broken up into pieces which could be treated in parallel, whereas Parallelism implies that those pieces are actually running at the same time.

Bob quickly made a diagram showing the architecture of his computer vs Rob's **iPhone 7** (A10 chip has a dual-core) to make him understand the difference.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/dualcore_vs_singlecore.png" alt="Dual Core VS Single Core">
    <figcaption> Architecture of Pentinum 1 vs iPhone 7 wrt number of cores </figcaption>
  </div>
</figure>

Bob continued: My computer has a single CPU and is ideally capable of executing a single program at a time. Later due to advancement in software **multitasking** came which meant that computers could execute multiple programs (or processes) at the same time. The single CPU was shared between the programs. The operating system would switch between the programs running, executing each of them for a little while before switching.

Later came **multithreading** which means that you could have multiple threads of execution inside the same program. A thread of execution can be thought of as a CPU executing the program. When you have multiple threads executing the same program, it is like having multiple CPUs executing within the same program.

Finally came **Concurrency**, which means that you can process multiple requests/tasks at a time inside a thread. It makes it appear that tasks are executing in parallel.


Rob: We do a lot of asynchronous programming and it is same as parallel programming.

Bob: It feels like you are executing in parallel but if you deep dive underneath, it's not.

Let's divide our discussion into a simple matrix:

|              | Synchronous | Asynchronous
Single Threaded | single-threaded synchronous | single-threaded asynchronous
Multi-Threaded | multi-threaded synchronous | multi-threaded asynchronous

### Synchronous execution
When you execute something synchronously, you wait for one task to finish before moving on to another task. For example you cannot go for running without waking up.

In programs, it means when a thread is assigned to one task and start executing. It will wait till the taken task is completed before taking another one.

#### Single Threaded:
Say you have several tasks to be executed and have a single thread. In a single thread, these tasks will be picked up one by one and processed as

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/single_sync.png" alt="Single Threaded Synchronous execution">
    <figcaption> Single Threaded Synchronous execution of tasks </figcaption>
  </div>
</figure>

In above figure, thread 1 is having four tasks and they are getting executed one by one. The order of priority in which tasks were picked up doesn't matter what matter is that they will execute inside the thread one after another.

#### Multi-Threaded:
Say you have several tasks to be executed but also have multiple threads on your disposal. In a multi-thread scenario, tasks will be picked by different threads and whose-ever finished first will take another.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/multi_sync.png" alt="Multi Threaded Synchronous execution">
    <figcaption> Multi Threaded Synchronous execution of tasks </figcaption>
  </div>
</figure>

We have four threads and four tasks, this doesn't happen in the real world most of the times, you will have more tasks than the number of threads. In the above case also, after the task has been picked it will be processed in their respective thread. Now, if a new task arrives it will be put in the thread which will get free first.

### Asynchronous
Asynchronous is an antonym for synchronous which means when you execute something asynchronously, you can move on to another task before it finishes.

#### Single Threaded

You will have one thread in which the same task can be interleaved with each other. A figure will give much better perspective.

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/single_async.png" alt="Single Threaded Asynchronous execution">
    <figcaption> Single Threaded Asynchronous execution of tasks </figcaption>
  </div>
</figure>

As you can see, in asynchronous execution one tasks doesn't wait for another to be finished. A thread saves task state and moves on to execute another one.

#### Multi-Threaded
The above same model can be extended for the Multi-Thread. Let's look into the diagram below

<figure>
  <div class="large">
    <img src="{{ site.url }}/assets/images/posts/2017-03/multi_async.png" alt="Multi Threaded Asynchronous execution">
    <figcaption> Multi Threaded Asynchronous execution of tasks </figcaption>
  </div>
</figure>

As you can see Task 4, Task 5, Task 8 are handled by a different thread. So how does a thread is able to do it? As said above, thread saves the current state of the task and later it gets picked up from the saved state.

*For Asynchronous execution, always make your tasks independent entity unless it will lead to data corruption and crashing of the program.*


Out of above four cases, three are concurrent. ***What are those?***

1. Synchronous Multi-Threaded
2. Asynchronous Single Threaded
3. Asynchronous Multi-Threaded

**Why?**
Concurrency simply means executing independent blocks code at the same time and above three paradigm provides it.

Rob was very happy with the explanation. He told Bob that lately he was using concurrency in iOS apps but never knew the subtle difference in parallelism.


### iOS Concurrency
Apple Foundation framework has provided a higher level APIs for multi-threading using **Operation** and **GCD (Grand Central Dispatch)**. If you are more interested into threading then you can also look upon **Thread** and **pthread**.


Let's first learn about the **Operation**. We will walk through what capabilities operation have used examples.

### Operation

The Operation class is an abstract class you use to encapsulate the code and data associated with a single task. Because it is abstract, you do not use this class directly but instead subclass or use one of the system-defined subclasses (Invocation​Operation or Block​Operation) to perform the actual task.

Rob created a sub-class of operation with a sum task which is mentioned below. He also told Bob that there are various properties and methods which can be overridden to suit the need of a task.
Read more about it [here](https://developer.apple.com/reference/foundation/operation){:target="_blank"}

```swift
// A simple operation class which sums up two number
class SumOperation : Operation {
    let a: Int
    let b: Int

    init(a: Int, b: Int) {
        self.a = a
        self.b = b
    }

    func sum()  {
        let s = self.a + self.b
        print("Sum of \(a) and \(b) is: \(s)")
    }

    // This method call the task
    override func main() {

        // Check if operation has been cancelled
        if self.isCancelled {
            return
        }
        self.sum()
    }
}

// Operation queue will execute this task concurrently
let opQueue = OperationQueue()
let op1 = SumOperation(a: 20, b: 50)
let op2 = SumOperation(a: 30, b: 70)

opQueue.addOperation(op1)
opQueue.addOperation(op2)

Output:
Sum of 20 and 50 is: 70
Sum of 30 and 70 is: 100
```

Moving ahead, An operation object (op1, op2) is a single-shot object—that is, it executes its task once and cannot be used to execute it again. You typically execute operations by adding them to an operation queue (an instance of the Operation​Queue class) as shown in above example.

We have created a **Operation** by subclassing the abstract Operation class. Operation can be also created using

* [NSInvocationOperation](https://developer.apple.com/reference/foundation/nsinvocationoperation?language=objc){:target="_blank"}
* [BlockOperation](https://developer.apple.com/reference/foundation/blockoperation){:target="_blank"}

```swift

class SumClosure {
    let queue = OperationQueue()
    var a, b: Int

    init(a: Int, b: Int) {
        self.a = a
        self.b = b
    }

    func sum() {
        // add task using block/closure to the queue
        queue.addOperation({ [weak self] in
            print(self.a + self.b)
        })
    }
}

let sumClosure = SumClosure(a: 60, b: 70)
sumClosure.sum()

//prints 130

```


*Note: As of Xcode 6.1, NSInvocation is disabled in Swift, therefore, NSInvocationOperation is disabled too.*

#### Operation Queue
NSOperationQueue regulates the concurrent execution of operations. It acts as a priority queue, such that operations are executed in a roughly First-In-First-Out manner, with higher-priority (NSOperation.queuePriority) ones getting to jump ahead of lower-priority ones. NSOperationQueue can also limit the maximum number of concurrent operations to be executed at any given moment, using the maxConcurrentOperationCount property.

An operation queue executes its operations either directly, by running them on secondary threads, or indirectly using the lib dispatch library (also known as Grand Central Dispatch).

**To kick off an NSOperation, either call start or add it to an NSOperationQueue, to have it start once it reaches the front of the queue.**

#### State
Operation keeps track of the state of the task. A task at any given time can be in 3 different states.

`Ready -> Executing -> Finished ( Completed/Cancelled)`

Taking of above example, let ask these to **op1**

```swift
op1.isReady  // returns true as initialisation has been done
op1.isExecuting // returns false

opQueue.addOperation(op1)
opQueue.addOperation(op2)

// Adding sleep so that opQueue finishes the task
sleep(2)
op1.isFinished  // returns true

```

#### Queue Priority and Quality of Service
```swift
public enum QueuePriority : Int {
    case veryLow
    case low
    case normal
    case high
    case veryHigh
}
```
Using the above example, Rob set the queue priority of both the operation to see if there is change in order of execution

``` swift
op2.queuePriority = .veryHigh
op1.queuePriority = .low

opQueue.addOperation(op1)
opQueue.addOperation(op2)

Output:
Sum of 20 and 50 is: 70 // op1 got executed first
Sum of 30 and 70 is: 100

```
No change, Rob guessed it and told Bob that it happens because our operation is very small task adding two number. If create a loop of millions of times, then we can see the order difference here.

```swift
public enum QualityOfService: Int {
    case userInteractive // tasks related to UI interaction like drawing, touch
    case userInitiated // task requested by the user like loading email
    case utility // task which doesn't need an immediate response to notification, updates
    case background // It neither visible nor initiated by a user like send crash reports
    case default
}
```
Now when Rob changed the **qualityOfService**, it did change the order.

``` swift
op2.qualityOfService = .userInteractive
op1.qualityOfService = .background

opQueue.addOperation(op1)
opQueue.addOperation(op2)

Output:
Sum of 30 and 70 is: 100 // op2 got executed first
Sum of 20 and 50 is: 70
```
This means that user interaction related tasks get priority on micron level time difference.

#### Operation Dependencies
Dependency helps you serial or synchronous execution of the task. Depending on the complexity of an application, it may make sense to divide up large tasks into a series of composable sub-tasks. This can be done with NSOperation dependencies.

For Example, Many times Rob likes a picture while browsing on his phone and then save it to his personal server. In this cases, until download from the public server has not completed he cannot upload it.

<figure>
  <div class="medium">
    <img src="{{ site.url }}/assets/images/posts/2017-03/dependency_operation.png" alt="Dependency Operation">
    <figcaption> Save to server is dependent on download from URL </figcaption>
  </div>
</figure>

```swift
let saveToServer = Operation()
let DownloadFromURL = Operation()

saveToServer.addDependency(downloadFromURL)
```

#### Synchronous and Asynchronous

If you do not use queues to schedule your operations and decide to execute operations manually (not recommended), in this case, an operation could run:

On the same thread, they are called. (synchronous).
On a different thread. (asynchronous).

Checkout ["Asynchronous Versus Synchronous Operations"](https://developer.apple.com/reference/foundation/operation){:target="_blank"} on the NSOperation docs.

>❗️ When you add an operation to an operation queue, the queue ignores the value of the asynchronous property and always calls the start method from a separate thread. Therefore, if you always run operations by adding them to an operation queue, there is no reason to make them asynchronous.

#### What we have learned?
Let's recap it quickly

* How to create an Operation using subclassing Operation abstract class and also using closures ?
* How to set properties like priority, quality of service etc ?
* If Operation is executed in Operation Queue then they are asynchronous unless by default Operation is a synchronous entity.


### Grand Central Dispatch
GCD is a low-level C-based API that enables the very simple use of a task-based concurrency model. It helps execute code concurrently on multicore hardware by submitting work to dispatch queues managed by the system.

The best place to learn about the all the API it provides is to go visit official Apple [documentation](https://developer.apple.com/reference/dispatch){:target="_blank"}.

Although you may write your code to use concurrent execution under GCD, it’s up to GCD to decide how much parallelism is required. Parallelism requires concurrency, but concurrency does not guarantee parallelism.

Let learn few more things about GCD

#### Queues
GCD provides **dispatch queues** to handle blocks of code; these queues manage the tasks(WorkItem) you provide to GCD and execute those tasks in FIFO order. This guarantees that first task added to the queue is the first task started in the queue, the second task added will be the second to start, and so on down the line.

*All dispatch queues are themselves thread-safe in that you can access them from multiple threads simultaneously.*

#### Serial Queues
As the name suggests, Tasks in **serial queues** execute one at a time, each task starting only after the preceding task has finished. Also, the time consumed by each task is not defined.

#### Concurrent Queues
Here the things get interesting. Tasks in **concurrent queues** are guaranteed to start in the order they were added and that's it and you don't have any knowledge when they are gonna finish. Here one task doesn't wait for the other and this is entirely up to GCD to decide.

#### Main Queue
The system provides you with a special serial queue known as the **main queue**. Like any serial queue, tasks in this queue execute one at a time. However, it’s guaranteed that all tasks will execute on the main thread and that's why use it for updating UI or in the aspect where responsiveness is critical.

In addition to the serial main queue, the system also creates a number of global concurrent dispatch queues.



```swift
// create a new serial dispatch queue
let queue = DispatchQueue(label: "com.rudrakos.concurrency")

// Get the main queue
let mainQueue = DispatchQueue.main

// get the global background queue
let backgroundQueue = DispatchQueue.global(qos: .background)

// Concurrent queue
let concurrentQueue = DispatchQueue(label: "com.rudrakos.concurrency", attributes: .concurrent)
```

#### Synchronous and Asynchronous

Rob said to Bob: You see, it is so simple to create all these queues. Once the queue is created, then we can execute code with it, either synchronously using a method called **sync**, or asynchronously using a method called **async**.

```swift
let queue = DispatchQueue(label: "com.rudrakos.concurrency")

queue.async {
    print("Asynchronous Execution!")
}

queue.sync {
    print("Synchronous Execution!")
}

Output
Asynchronous Execution!
Synchronous Execution!

```

Bob said to take a better example because above doesn't give any clue about sync and async.

```swift
// loop in another thread
queue.sync {
    for i in 1..<10 {
      print("Synchronous Execution!")
    }
}

// loop on main thread
for i in 1..<10 {
  print("Not inside a queue!")
}

Output:
Synchronous Execution!
Synchronous Execution!
Synchronous Execution!
Synchronous Execution!
Synchronous Execution!
Synchronous Execution!
Synchronous Execution!
Synchronous Execution!
Synchronous Execution!
Not inside a queue!
Not inside a queue!
Not inside a queue!
Not inside a queue!
Not inside a queue!
Not inside a queue!
Not inside a queue!
Not inside a queue!
Not inside a queue!
```
Not a surprising output because we have chosen synchronous execution and so the task will be executed as they have been added and another task will wait till the previous one finishes.

```swift
// Asynchronous
queue.async {
    for i in 1..<10 {
        print("Asynchronous Execution!")
    }
}

for i in 1..<10 {
    print("Not inside a queue!")
}

Output:
Asynchronous Execution!
Not inside a queue!
Not inside a queue!
Asynchronous Execution!
Not inside a queue!
Asynchronous Execution!
Not inside a queue!
Asynchronous Execution!
Not inside a queue!
Asynchronous Execution!
Not inside a queue!
Asynchronous Execution!
Not inside a queue!
Asynchronous Execution!
Not inside a queue!
Asynchronous Execution!
Asynchronous Execution!
Not inside a queue!
```
Bob, you guessed it right. you see that the code on the main queue (the second for loop) and the code of our dispatch queue run in parallel. The important thing here is to make clear that our main queue is free to “work” while we have another task running in the background, and this didn’t happen on the synchronous execution of the queue.

#### Queue Priority and Quality of Service

GCD also provide Quality of Service similar to Operations for prioritizing the task.

```swift
public enum QualityOfService: Int {
    case userInteractive // tasks related to UI interaction like drawing, touch
    case userInitiated // task requested by the user like loading email
    case utility // task which doesn't need an immediate response like notification, updates
    case background // It neither visible nor initiated by the user like send crash reports
    case default
}
```
You can create the queue with desired priority by specifying the  QoS value upon the queue initialization.

```swift
let queue1 = DispatchQueue(label: "com.rundrakos.queue1", qos: DispatchQoS.userInitiated)
let queue2 = DispatchQueue(label: "com.rundrakos.queue2", qos: DispatchQoS.utility)
```

#### Delay a Execution
Sometimes it’s required by the workflow of the app to delay the execution of a work item. GCD allows doing that by calling a special method and setting the amount of time after which the defined task will be executed.

```swift
let delayQueue = DispatchQueue(label: "com.rundrakos.delayqueue", qos: .background)
print("Lets delay this execution: \(Date())")
let additionalTime: DispatchTimeInterval = .seconds(2)

delayQueue.asyncAfter(deadline: .now() + additionalTime) {
    print("Calculate delay in execution: \(Date())")
}


Output:
Lets delay this execution: 2017-03-21 19:12:24 +0000
Calculate delay in execution: 2017-03-21 19:12:26 +0000
```

#### DispatchWorkItem
A DispatchWorkItem is a block of code that can be dispatched on any queue and therefore the contained code will be executed on a background or the main thread.

```swift
let workItem = DispatchWorkItem {
    print("Your WorkItem!")
}

// user perfrom method
queue.async {
    workItem.perform()
}

// This will do the same thing as above
queue.async(execute: workItem)

Output
Your WorkItem!

```

#### What we have learned?

* GCD provide both synchronous and asynchronous way of executing of a work item
* Various queues available like global and main
* Creating work item and using it

Wow, Rob, we both learned something great from each other. Both of them left the home at the same time and said "concurrent!".

