Authors:

[Christina Hinchin](mailto:christina.hinchin@academiadecodigo.org)  
[Sara Talefe](mailto:sara.talefe@academiadecodigo.org)
[Diogo Rolo](mailto:diogo.rolo@academiadecodigo.org)

&nbsp;

## 2.1. Introduction to Concurrency

Back in the dark ages, when programs were fed to a computer on a punched paper card, or on magnetic tape, these **computers could only execute one program at a time**. The program would be run **sequentially** and would access any resources it might need directly from the machine.

&nbsp;

*Program In Execution In Memory in a Single-Core CPU*![Single Core CPU][single-core-cpu]

&nbsp;

In order for a program to be executed:

1. The instructions need to be stored in the system **RAM**  
2. To be then sent to the **CPU** through the **Data, Address and Control BUSes**  
3. Once they enter the **CPU**, they go down a queue usually called **Pipeline**
4. Every **CPU** has a **Clock** that runs at a certain frequency _(p.e. 2GHz)_
5. Eventually, the **CPU** executes each instruction with the help of various components *(p.e. Math Processor)*  
**Execution Engine* is just a fancy name for many components
	
&nbsp;

**Operating systems** evolved to allow more than one program to run at once, running individual programs in *processes*.

This is analogous to the real life. When you're at home making dinner and finishing the summarizer for the next day *at the same time*, what you are really doing is cutting up some onions and adding them to the pan, then finding that funny meme for the presentation, then quickly stirring the onions so they don’t burn, then switching back to your laptop - otherwise known as *multi-tasking*.

You can surf the web on a browser and listen to music on Spotify *at the same time*. You can edit a document on word processor, while other applications can download files from the internet, *at the same time*.

So, **concurrency** can be thought of as `the ability to do more than one thing at the same time`. But how is that possible? How can multiple tasks execute at the same time even on a single CPU?
Well, in truth, they don’t execute at the same exact time.

When we say “multiple tasks are executing at the same time”, what we *actually* mean is that “multiple tasks are making progress during the same period of time.” The tasks are executed in an interleaved manner. And the way this happens is through the Operating System. It switches between the tasks so frequently that it appears like they are being executed at the same instant when in fact, they aren’t.

&nbsp;

If they needed to, processes could communicate with one another through a variety of **Inter-Process Communication** (**IPC**) mechanisms: sockets, signal handlers, shared memory, semaphores, and files.

> **Sockets**, you guys are already pretty familiar with. How many processes are running in our Chat program? The Server and the Client. In order to send information between these two processes, we used sockets to send and recieve data.

An example of a **signal** that you’ve used before is the ctrl-C to kill a program.

`$ ^C`

It is not actually you shutting down the program - you are just sending a signal via the operating system that you wish to terminate the program. The OS passes on this signal to the process and it shuts itself down.

# ------------ TODO ------------
**Semaphores** are classified into two types:

* *Binary Semaphores* − Only two states 0 & 1, i.e., locked/unlocked or available/unavailable, Mutex implementation.
* *Counting Semaphores* − Semaphores which allow arbitrary resource count are called counting semaphores.

Assume that we have 5 printers (to understand assume that 1 printer only accepts 1 job) and we got 3 jobs to print. Now 3 jobs would be given for 3 printers (1 each). Again 4 jobs came while this is in progress. Now, out of 2 printers available, 2 jobs have been scheduled and we are left with 2 more jobs, which would be completed only after one of the resource/printer is available. This kind of scheduling as per resource availability can be viewed as counting semaphores.
&nbsp;

## 2.2. Threads

Concurrency doesn’t necessarily involve multiple applications. Running multiple parts of a single application simultaneously is also termed as concurrency.

* A Word Processor formats the text AND responds to keyboard events *at the same time*. 
* Spotify reads the audio from the network, decompresses it and updates the display *at the same time*.
* A Web Server serves thousands of requests from all over the world *at the same time*.

These smaller parts of a **Process** that can run concurrently are known as **Threads**. The act of multiple threads running concurrently is known as *Multi-Threading*.

A thread is a *unit of execution within a process*. Every process has at least one thread - called the **main** thread. This main thread can create additional threads within the process. 

All of the threads within a process share the same resources such as memory and file handles. However, every thread has its own call stack and local variables.


In real life, you execute tasks **asynchronously**. If you're cooking some pasta with , you'd start by warming the water, then peeling and cutting the veggies, when the water is boiling, adding the spaghetti, .... At each step of the process, you'd start a task, and switch to the tasks that are ready for your attention.

&nbsp;

## 2.3. Processes vs Threads

![multithreading visual representation][multithreading]

Since threads share the same address space of the process, creating new threads and 
having them communicate is a lot more efficient.

Concurrency overall greatly improves the capacity of a computer - with it we simply can get a lot more done. But with great performance, comes a few issues.

If multiple threads have access to the same data within a process, then they can all modify that data - even if that data is currently being used by another thread in question. This can end up causing some very unpredictable results, which are extremely hard to detect.

Writing correct programs is hard; writing concurrent programs is harder. More things can go wrong in a concurrent program compared to a sequential one.

&nbsp;

But the biggest question is:

&nbsp;

## 2.4. Why Should I Care?

Threads are everywhere. Even if your program never explicitly creates a thread, frameworks you use may create threads on your behalf and we need to be sure the code called from these threads is *safe* and the only way to do that is to be aware of what a safe multi-threaded environment *is*.

Every Java application uses threads. When the JVM starts, it creates threads for things like garbage collection and there is a main thread for running the `main` method. It would be nice to tell ourselves that concurrency is an **advanced** feature of Java and we need not concern ourselves with it… but that simply is not the case.

Besides, used right, threads can greatly improve the performance of complex applications and make it easier to model how humans work and interact, turning asynchronous workflows into mostly sequential ones.

Imagine if instead of being able to “multi-task” we could only ever do anything once at a time. We would never get anything worthwhile done!

&nbsp;

## 2.5. {Hands-On} Implicit Thread Creation and Timers

Java class from the `utils` package, used to schedule tasks for future execution in a background thread that corresponds to each `Timer` object. The `scheduleAtFixedRate()` recieves a `TimerTask` object and schedules this object for repeated fixed-rate execution, beginning either at a specified time or after a specified delay.

[docs](https://gitlab.com/ac-bootcamp-materials/bootcamp/blob/master/docs/exercises/module_2_concurrency.adoc#user-content-hands-on-timers-and-implicit-thread-creation)

&nbsp;

### Why not use _Thread.sleep()_ ?

For precision timing, Thread.sleep() is absolutely *useless* and a big fat lie. You think that it blocks a thread for a given number of milliseconds, but what it actually does is block the current thread for a given number of *timeslices* that can occur within a set number of milliseconds. The length of a timeslice depends on the version of the Operating System and processor, generally ranging from 15 to 30 milliseconds. So basically you are almost guaranteed to block your thread for more than `n` milliseconds. .


&nbsp;

## 2.6. Thread Creation

There are objects in Java that create threads implicitly, but how do we go about making threads of our own? There are two ways we can explicitly create Threads.

- Extending the Thread class.
- Implementing the Runnable interface.

We can extend the Thread class, but this is very limited because once you extend your class from Thread, you cannot extend from any other class since Java doesn’t allow multiple inheritance. Also, as we know from Inheritance - it is meant to extend the functionality of the parent class, which is not what we are really trying to achieve here.

We can implement the Runnable interface, which is the primary template for any object that is intended to be executed by a thread. It defines a single method - run() - which is meant to contain the code that we want to be executed by the thread.

When creating a new Thread, we invoke the method start() which in turn, calls the run() method in whatever way we chose to implement it.

&nbsp;

## 2.7 {Hands-On} Explicit Thread Creation 

[docs](https://gitlab.com/ac-bootcamp-materials/bootcamp/blob/master/docs/exercises/module_2_concurrency.adoc#user-content-hands-on-explicit-thread-creation)

&nbsp;

## 2.8. Thread Synchronization

Under normal circumstances where we have more than one thread, there is zero guarantee of the order of execution of threads. We might create three threads in sequential order, but the order in which they start and end is not specified. We could run the same block of code multiple times and obtain different results. This is quite unpredictable.

This is because, just like how processes make progress at the same time by switching back and forth between each-other, threads switch context (governed by a scheduler) which introduces the biggest challenge that multi-threading presents to us. It takes us from a sequential thought process to a new unpredictable state.

There are times when we might want one thread to wait for another thread to finish execution before running, to guarantee the next block of code runs *sequentially* in relation to the previous block of code.

We could use the sleep() method, which allows us to pause the execution of one thread for a specified number of milliseconds. There are two issues with this attempt. The first is that Thread.sleep() is unreliable as it relies on the underlying OS, so the time it waits is not always precise and also that it is impossible for us to know how long a thread might take to complete a task.

The **join()** method allows one thread to wait for the completion of the other. It will hold the execution of the currently running thread until the thread upon which the method has been invoked has finished its execution.

&nbsp;

## 2.9. {Hands-On} Thread-Sync using Join 

[docs](https://gitlab.com/ac-bootcamp-materials/bootcamp/blob/master/docs/exercises/module_2_concurrency.adoc#user-content-hands-on-thread-sync-using-join)

&nbsp;

## 2.10. {Exercise} Concurrent WebServer

[docs](https://gitlab.com/ac-bootcamp-materials/bootcamp/blob/master/docs/exercises/module_2_concurrency.adoc#user-content-exercise-concurrent-web-server)

&nbsp;

## 2.11. Thread Safety

> Concurrent programming isn’t so much about **_threads_** or **_locks_**, any more than civil engineering is about rivets and I-beams. Of course, building bridges that don’t fall down requires the correct use of these things, just as concurrent programs require the correct use of threads and locks. But these are just *mechanisms* - means to an end. **Writing thread-safe code is, at its core, about managing access to state, and in particular to shared, mutable state.**.  
> — Java Concurrency in Practice

Multithreading is a very powerful tool which enables us to better utilize the system's resources, but we need to take special care while reading and writing data that is *shared* by multiple threads.

Concurrent programming errors fall into one of these three categories:

1. Visibility
2. Atomicity
3. Ordering

&nbsp;

## 2.12. Visibility

Firstly, **what is visibility**? The name says it all. **That the actions of one thread may be *visible* to another**. The problem is this isn’t always the case.

In order to understand this issue, we need to learn a bit more about how a modern-day CPU works.

Retrieving and writing data to the Memory has always been a slow process. Before, processors were equally slow so this wasn’t such a great issue, but as processors became a lot faster, the gap between the two in terms of performance widened and became far more noticeable.

With the introduction of caches things became a whole lot faster. Caches are another form of memory which is incredibly fast. When the CPU accesses something from your main memory, it stores this data in its CPU cache. The next time it needs that same data, rather than grabbing it from the main memory, which is slow, it first checks its cache and takes it from there.

**L1, L2 and L3 caches** are different memory pools similar to the RAM in a computer. **They were built in to decrease the time taken to access data by the processor.** This time taken is called **_latency_**. The architecture they are built with also differs considerably. 
>The L1 cache is built using larger transistors and wider metal tracks, trading off space and power for speed. The higher level caches are more tightly packed and use smaller transistors. [Read More][l1-l2-l3-cache-article]

So, L1 cache is a smaller and much faster cache, whereas L2 and even L3 are subsequently larger and slower layers of cache. If there isn’t something stored in the L1 cache, the CPU checks its L2, then L3 and so forth.

&nbsp;

![L1, L2 & L3 Cache][l1-l2-l3-cache]

&nbsp;

Okay, so we get why caches help speed up processing, but what does that have to do with our threads?

Well, rather than read from and writing directly to the main memory, each thread may also copy variables from the main memory into a CPU cache while working on them. The JVM makes no guarantee about when it reads data from main memory into CPU caches or when it takes data from caches and writes to the main memory - which in a multithreaded environment could cause problems.

&nbsp;

```java
public class FieldVisibility {
  
  private int x = 0;

  public void writerThread(){
    x = 1;
  }

  public void readerThread(){
    int r1 = x;
  }

}
```

&nbsp;

| writer-thread | reader-thread |
| ------------- | ------------- |
| core-1        | core-2        |
| local cache   | local cache   |
| x = 1;        | x = 0;        |
|               | r1 = x;       |

| shared cache |
| :----------: |
|    x = 0;    |

&nbsp;

This problem of not seeing the latest value of a variable because it has not yet been written back to main memory by another thread is called a “visibility” problem. The updates of one thread are not *visible* to other threads.

&nbsp;

## 2.13. Volatile

The `volatile` keyword intends to address visibility problems. By declaring a variable `volatile` all writes will be written back to main memory immediately. Also, all reads will be read directly from main memory.

Volatile also defines a **happens-before** relationship.

Meaning, that whatever happens *before* a volatile write should be visible *after* a volatile read.

&nbsp;

```java
private int a = 0;
private int b = 0;
private volatile int = x;

// Thread-1
public void write(){
  
  a = 1;
  b = 1;
  x = 1;   // volatile write
}

// Thread-2
public void read(){
  
  System.out.println(x);  // volatile read
  System.out.println(a);
  System.out.println(b)
}
```

&nbsp;

When the Thread-1 changes **_x_**, it will not only flush this change to main memory, but **it will also cause the previous two writes** (and any other previous writes) **to be flushed into the main memory as well!** As a result, when the second thread accesses these three variables it will see all the writes made by thread 1, even if they were all cached before (and these cached copies will be updated as well)! 

But, volatile is not always enough.

&nbsp;

## 2.14. Atomicity

In the previous example where one thread performs a write and write whilst the other simply performs a read, by declaring a variable is volatile we ensured that the second thread will always see the changes the first thread is making.

In fact, *multiple* threads could write to a shared volatile variable, and still have the correct value stored in main memory, as long as the new value written to the variable **does not depend on its previous value.**

However, as soon as a thread needs to first *read* the value, and *based* on that value generate a new value, then `volatile` is no longer enough to guarantee correct visibility. This is because an increment operation such as:

```java
counter++
```

is in reality 


```java
counter = counter + 1;
```

two separate operations: a read and then a write. 

In order to make this operation **thread safe**, we need it to act as if it was one operation. We need it to be *atomic*.

&nbsp;

## 2.15. Atomicity

> Atom - derived from the Greek word *atomos* which means “Indivisible”

If an action is (or a set of actions are) atomic, its result must be seen to happen “all at once”, or indivisibly.

&nbsp;

```java
private volatile long balance = 10;

public void deposit(long x){
  
  long b = getBalance();
  setbalance(b + x);
}

public void withdraw(long x){
  
  long b = getBalance();
  setbalance(b - x);
}

// Thread-2
withdraw(5);

// Thread-1
deposit(5);
```

&nbsp;

If this was single-threaded, we would expect to see the output 10, no matter which order these two methods are called. But in a multi-threaded environment, this result isn’t guaranteed.

- Thread-1 reads the `balance` and sees a value of 10, then
- Thread-2 reads the `balance` and sees a value of 10 for the balance *and* withdraws 5, writing the value 5 in `balance`, finally
- Thread-1 uses the value it originally saw (10) and writes the value 15 in `balance`.

Because these methods are not atomic, the result is not what we expected. We need to find a way to say that this set of instructions is to be executed *as one unit.*

There is another issue.

&nbsp;

### Java Primitives Are NOT Thread Safe

Long and double require two memory operations because they are stored as two 32-bit values. So a 64-bit write operation is performed as **two** separate 32-bit operations. We must explicitly state that this variable is `volatile` to make it an atomic variable.

But still, as we saw before - declaring a variable as being volatile isn’t enough to ensure thread-safety - we need to make sure the operations we are performing on it are also atomic.

&nbsp;

## 2.17. Atomic Variables

In Java we have classes which work a lot like our wrapper of primitive types, with the added guarantee that they can be used safely in a multi-threaded context.

They provide operations that cannot be interfered by multiple threads, such as increment and decrement. They are guaranteed to execute atomically using machine-level instructions on modern processors.

&nbsp;

## 2.18. Check-Then-Act

Whilst we now guarantee atomicity upon primitive values, we still need to watch out for issues such as the deposit and withdraw problem we discussed earlier.

&nbsp;

```java
public void withdrawMoney(long money){
  //check
  if(balance >= money){
      //act
      balance -= money;
  }
}
```

&nbsp;

Whilst the decrement value will be done atomically, anytime we have separate lines of code, we have an atomicity problem.

First, we perform a *check* and then we *act* upon this check. As we saw earlier, anything can happen between the check and the act - so methods that contain a check-then-act logic **NEED** to be atomic!

There is yet another problem working against us when we have multi-threading…

&nbsp;

## 2.19. Ordering

> The Java compiler can change the order of execution if it believes the outcome will not change…

Wait, what?

Java is an imperative language. You tell Java *how* to do something for you. If Java executed your instructions not in the order you write, it would obviously not work. 

&nbsp;

```
1. Take eggs out of the freezer
2. Take lid off
3. Take milk out of the freezer
4. Pour egg and milk in
5. Cook for 3 hours
```

&nbsp;

If Java worked the way we thought it did, it would run this code in the same order as we wrote it. However Java is clever enough to understand that it’s more efficient AND that the end result would be the same should it do 1 > 3 > 2 > 4 > 5.

&nbsp;

```
1. Take eggs out of the freezer
2. Take milk out of the freezer
3. Take lid off
4. Pour egg and milk in
5. Cook for 3 hours
```

&nbsp;

One less operation (moving to the freezer again) and it makes no changes to the outcome of the recipe.

So, in a single thread, your program will run **as if** it was executed in the exact order you wrote it. The ordering might change behind the scene, but it makes sure that none of that will change the output.

In a single thread environment this works without a problem. In a multi-threaded environment however this simply is not possible, with the unpredictable context-switching between threads occurring, it is no longer possible to guarantee this reordering won’t affect the outcome anymore.

So, we need to explicitly tell it to **not** do reordering that would change the program outcome.

The keyword `volatile` aside from making sure changes to a variable is *visible*, also tells the compiler that the read and write operations made upon it *cannot be reordered*.

But, yet again, it is not enough…

&nbsp;

## 2.20. So Many Issues! What Is The Right Answer??



[REVISE ISSUES THAN CAN ARISE IN CONCURRENCY AND THE SOLUTIONS WE HAVE DISCUSSED THUS FAR]

&nbsp;

## 2.21. Make Everything Immutable.

What is an immutable object?

An object is considered *immutable* if its state cannot change after it is constructed.

Since the issue we have in multithreading is the manipulation of shared state - then the obvious answer is to make that state unchangeable! What is a keyword that we know in Java that means ‘cannot be changed’ ?

The `final` keyword!

- a final variable can only be initialized once
- a final method cannot be overriden or hidden by subclasses
- a final class cannot be subclassed

If immutability makes our code thread-safe, then why don’t we just make everything in our program an immutable object?

Well, both mutable and immutable objects have their own uses, pros and cons.

Immutable objects do indeed make life simpler in many cases. They are especially applicable for value types that don’t have an identity and can easily be replaced. And they can make concurrent programming way safer and cleaner (as most concurrent bugs are caused by mutable state shared between threads) However, for large and/or complex objects, creating a new copy of the object for every single change can be very costly and tedious. And for objects with a distinct identity, changing an existing object is much more simple and intuitive than creating a new modified copy of it.

Think about a game character. In games, speed is top priority, so representing your game characters with mutable objects will most likely make your game run significantly faster than an alternative implementation where a new copy of the game character is spawned for every little change.

So yes, an immutable object is thread-safe - but we might not want to apply this solution to every situation.

…so *what* is the answer here?

&nbsp;

## 2.22. Intrinsic Locks - NEEDS REVIEW

![img](https://deviniti.com/wp-content/uploads/2019/09/460E9D08-1BED-4634-9F39-09025B867985-1.png)

Imagine, if you will, a program that will add all the numbers from 1 to 10.  
We could write this in a for loop.

&nbsp;

```java
int num = 0;

for(int i = 1; i <= 10; i++){
  num += i;
}
```

&nbsp;

Printing the result of this will give me 55, always.

Now what if I were to split this up into two threads - one that will count all the numbers from 1 to 5 and another from 6 to 10.  
We should still expect the output to be 55, but in reality it’s not always the case.

(Well, actually in reality it would be, just because threads can interleave doesn’t mean they always do. In order to actually see a difference we’d need to increase the number of iterations by *a lot* - so let’s do that!)

&nbsp;

```java
private static long num = 0;

public static void main(String[] args) {
 
  Thread t1 = new Thread(threadFunc());
  Thread t2 = new Thread(threadFunc2());
  t1.start();
  t2.start();
  
  // add in a Thread.sleep(1000) to give time for the two threads to finish.
  System.out.println(num);
}

public static Runnable threadFunc(){
  
  return new Runnable() {
   
    @Override
    public void run(){
      for (int i = 1; i < 100000; i++) {
        num = num + i;
      }
    }
  
  };
}

public static Runnable threadFunc2(){

  return new Runnable() {

    @Override
    public void run(){
      for (int i = 100000; i <= 200000; i++) {
        num = num + i;
      }
    }
  
  };
}
```

&nbsp;  
The result we expect to see is 20000100000.

But if we run the code several times, the outcome is always different. Why?

Well, as you can imagine - with two threads running concurrently, there is quite a bit of data interference. Both threads are causing consecutive overwrites, manipulating data “out of turn” so to speak. Whilst we don’t want one thread to wait for the other to finish adding his 100,000 before it can start - we want them to take turns incrementing data so it is always in a fresh, updated state.

![img](https://imgur.com/YbrR5GS.png)

And yes, with numbers and incrementation we can certainly optimize this with `volatile` and atomic wrappers, but if we increased the complexity of these operations a little bit more, we’d be at a loss. 

*Unless*...

*Unless* we add a token of sorts. A thread **must** be holding the token in order to perform an operation and when it has finished, the token is freed to be used by any thread. 

The token here is called an **Intrinsic Lock**. All Objects in Java have an intrinsic lock. A thread must have a hold of the lock in order to enter a block of code. Any thread that needs to run this code will be *blocked* from doing so until the previous thread has finished.

&nbsp;

## 2.23. Synchronized Blocks

Let’s use a different analogy other than numbers. Let’s imagine we have a Cadet class and a Bathroom class.

&nbsp;

```java
public class Cadet implements Runnable {
  
  private String name;
  private Bathroom wc;

  public Cadet(String name, Bathroom wc) {
    this.name = name;
    this.wc = wc;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  @Override
  public void run() {
    Thread.currentThread().setName(name);
    wc.useToilet();
  }

}
```

```java
public class Bathroom {
  
  public void useToilet() {
    
    System.out.println(Thread.currentThread().getName() + " entering toilet");
    System.out.println("*unzips*");

    try {
      Thread.sleep(1000);
    } catch (InterruptedException e) {
       e.printStackTrace();
    }

    System.out.println(Thread.currentThread().getName() + " leaving toilet");
  }
  
}
```

&nbsp;

If we instantiate a few Cadets and run their threads, it appears they all go into the bathroom at the same time! This is very undesirable behaviour. I want to make this method atomic and ensure that no other thread can perform these actions until the previous is finished. I need to *lock* the bathroom.

&nbsp;

```java
public class Bathroom {

  public void useToilet() {
    
    synchronized (this) {
      // do stuff
    }
    
  }
  
}
```

&nbsp;

Now, each thread blocks, waiting for the lock to free up so they can then use the bathroom.

&nbsp;

## 2.24. Method Synchronization *vs* Statement Synchronization

What is the difference between synchronizing a method *vs* a block of code?

&nbsp;

```java
public synchronized void useToilet(){
  // do stuff
}

public void useToilet() {

  synchronized (this) {
    // do stuff
  }
  
}
```

&nbsp;

With a synchronized method the lock is obtained for the duration of the entire method. With synchronized blocks you can specify exactly when the lock is needed.

This is helpful if the useToilet method had parts that didn’t need to be synchronized. You only really need to guarantee synchronization when dealing with mutable and shared state. With **block synchronization** you limit the scope of synchronization.

Another difference is the lock itself. A synchronized method always refers to `this` - the object instance. If we have several synchronized methods in a class, one thread obtains the lock for the instance and other threads can’t use *any* of the other synchronized methods of that instance until the lock is released.

A synchronized block can refer to different objects as the lock.

&nbsp;

```java
public class Bathroom {

  private Toilet t1;
  private Toilet t2;
  
  public void useToilet1() {
    synchronized(t1) {
      // do a peepee
    }
  }
    
  public void useToilet2() {
    synchronized(t2) {
      // a different peepee
    }
  }
  
}
```

&nbsp;

One toilet being occupied is not reason for our Bathroom instance to be off-limits to other threads. Whilst thread-1 obtains the lock for **t1**, other threads can try to obtain the lock for **t2**.

&nbsp;

## 2.25. Thread Synchronization with Guarded Blocks

Sometimes you only want a thread to execute a block of code when a certain event is true. One way we can achieve this is with a while loop.

&nbsp;

```java
private boolean happy = false;

public void guardedHappiness() {

  while(!happy) {
    // do nothing.
  }

  System.out.println("Happiness achieved!");
}

public void beHappy() {
  happy = true;
}
```

&nbsp;

We could have one thread which invokes the guardedHappiness method and another which runs the beHappy method. The first enters guardedHappiness and loops indefinitely until the other thread invokes the beHappy method.

The problem is, our boolean `happy` is *shared and mutable* state, which is something we need to worry about in a mutli-threaded environment. If we use the `synchronized` keyword, we can protect our state by allowing **only one thread at a time** into a particular section of code thus allowing us to protect, for example, variables or data from being corrupted by simultaneous modifications from different threads.

&nbsp;

```java
private boolean happy = false;

public synchronized void guardedHappiness() {...}

public synchronized void beHappy() {...}
```

&nbsp;

But now we have introduced a problem. What do we know about synchronized and locks? Since both of our methods are synchronized and the lock is the instance, after the first thread has obtained the lock - *no other synchronized methods can be invoked on this instance until the lock is released*. If the thread holding the lock is trapped in a while loop, when does the lock get released?

**Never**. This is known as a *dead-lock*.

What we actually want to happen is, in the eventuality that our thread reaches a moment where it must *wait* for a condition to be true, that our thread both stops running *and* releases the lock. This way, it is now possible for other threads to invoke the `beHappy()` method.

We can do this with **guarded blocks.**

&nbsp;

```java
public synchronized void guardedHappiness() {

  while(!happy) {
  	 wait();
    // thread will wait here forever.
  }

  notifyAll();
  System.out.println("Happiness achieved!");
}
```

&nbsp;

The first thread enters the method when `happy` is false and *waits*. It will wait here, releasing it’s lock and only resume execution - not when the happy boolean is true - when another thread invokes *notifyAll*. What this does is wake all the threads who are currently waiting on the same lock.

It is important to have the `wait()` inside a while loop and not an if.

[Discuss what could happen if we used an if and not a while]

&nbsp;

## 2.26. Thread LifeCycle and Wait/Notify

![img](https://imgur.com/StIIOC7.png)

`wait`, `notify` and `notifyAll` are methods inherited from `Object`.

By invoking the method wait() inside of a synchronized block - we send the Thread currently using the object into a **non runnable** state. The scheduler will no longer allocate time for the Thread to run and it will essentially ‘sleep’ *forever* unless it is woken up.

When another thread invokes notify or notifyAll within the same object, then the *non-runnable* threads become *runnable* again.

&nbsp;

## 2.27. Producer/Consumer Problem

A classic example of a multi-process synchronization problem. Two entities, the producer and the consumer, who share a common fixed-size buffer which they use as a qeue. The producer generates data, tries to put it into the buffer and repeat. At the same time, the consumer is attempting to consume data one piece at a time.  
The goal is to make sure the producer cannot attempt to put data on the queue when it is full and the consumer cannot remove data from the queue when it is empty.



&nbsp;

## 2.28. {Exercise} - Producer-consumer using a (created) BlockingQeue
#### Objective  

The goal is to have the cadets consolidate the knowledge of both the Java Collections and multi-threading by implementing their own version of a BlockingQeue, and have them understand what a `thread safe` program is and what do we have to worry about in order to make it so.  
I like the idea of having a pizzeria and making and consuming pizzas, but you guys can use whatever as the data, Strings, numbers, whatever.

#### Flow  
1. The general concepts for the exercise are:
  * We will build our implementation of a producer/consumer using a blocking queue of a fixed size created by us
  * Producers will attempt to add products to the queue (Integers in AC's example)
  * Consumers will attempt to get products from the queue
  * The idea is that if a producer attempts to place something in the queue and finds it full, he will wait until a consumer frees up space on the queue
  * The opposite is expected of the consumer if he attempts to get anything from the queue and finds it empty
2. The producers should have a limit to how many items they produce and the same goes for the consumers.
3. If you introduce random `threadSleep()` times in both the producer and the consumer, the concurrent behaviour might become more obvious
4. Show the cadets the skeleton for the exercise and match each class with the previous points, then have them go at it

_**Do not forget to make it really obvious that cadets should not use Java's already existing BlockingQueue!!**_

##### Possible issues  
* cadets will not understand that the lock they are using on the producer and consumer is not the same as the queue
* cadets might notifyAll() before adding or removing elements, making the program not actually thread safe (remember them of the "check-then-act" situation)
 

&nbsp;

## 2.29. Synchronised collections
A set of Java collections in which the state is encapsulated and all the public methods are synchronised. This makes sure that all operations on these classes are atomic and thus thread-safe, but concurrency is sacrificed.
Java's synchronised classes are:

* [HashTable][java.util.Hashtable-docs]
* [Vector][java.util.Vector-docs]
* [synchronised wrapper classes][java.util.Collections-synchronizedCollection-docs]

Despite being thread-safe, these classes are not the most interesting to use in a high-concurrency environment.
The reason for that is due to the fact that they implement single collection-wide locks, and it is often necessary to lock a collection for a considerable period during iterations in order to prevent a `ConcurrentModificationException` from occurring.


&nbsp;

## 2.30. Concurrent collections
Java's [java.util.concurrent][java.util.concurrent-docs] package provides you with several concurrent implementations of containers, some of them being:

 * [ConcurrentHashMap][java.util.concurrent.ConcurrentHashMap-docs]
 * [CopyOnWriteArrayList][java.util.concurrent.CopyOnWriteArrayList-docs]

There are several others, finding out which is a matter of looking in the java.util.concurrent package for them.
Those somewhat "improved" containers are actually designed with concurrent access by several threads in mind and can offer interesting scalability improvements. This is possible due to how locking is actually implemented within the containers. In the example of the [ConcurrentHashMap][java.util.concurrent.ConcurrentHashMap-docs], this is achieved by introducing the concept of segmentation, allowing only smaller parts of the collection to be locked at a single time, allowing free access to the rest, meaning that a thread does not block access to all other threads trying to interact with the map, just those trying to access the same specific segment that it has locked for itself.


&nbsp;

## 2.31. Damn this is hard.
Why can't I just make everything volatile and synchronised?
You actually can, but that will actually end up performing worse than having a single thread, because not only you will basically end up not allowing threads to do much work in between each other, having an execution that will almost feel sequential, you will now also have your program busy switching between those threads.  
Also you can easily create a deadlock by forgetting to release a lock somewhere...

&nbsp;

## 2.32. Thread pools and executors
Let's switch subjeects a tiny bit and go back to our web server, which is currently creating a new thread for each request that comes in.

&nbsp;

## 2.33. Creating a Thread per request
So, right now our web-servers are actually taking advantage of concurrency in order to be able to handle requests simultaneously, not leaving our users "hanging". That's pretty good, it has allowed us to fire a thread handling each request that arrived while our main thread goes back to actually waiting for more requests to arrive.

But is it safe?

&nbsp;

## 2.34. {Hands-On} - How my web-server blew up

#### Objectives
![dream-crushing][dreamcrush-link]

The goal is to show the cadets how expensive threads are and that even if they are idling they are consuming resources from the machine.

#### Flow
1. Prepare to use the script by running `npm i` on the `bootcamp/exercises/module-2/concurrency/1000requests` folder (beware, you must be in the `10000requests` branch of the repo, that is the branch with the currently working script) --> move script to master branch??
2. Ask a cadet to run his server and for his ip and port
3. Run the script aiming at his server `node 10000requests <IP>:<PORT> <AMOUNT_OF_REQUESTS>`
4. You should achieve an `OutOfMemoryError` on the cadet's machine. (In case you run it against our solution, you will have to turn off our `Logger` or look back up in the console for the Error, because we are gracefully closing and logging all executing threads, so you will still get several logs after the main thread has blown up.)
  
  * If you have it installed, you can open the [visualvm][visualvm-site] tool to show the cadets what is happening to their server when handling the requests. Take a glance at how it works by following the link, and you can install it as a brew cask by running `brew cask install visualvm` if you want. It's a cool detail to just allow you to show some performance statistics to the cadets, including amount of threads and HEAP usage and size in a graphical way.
 
&nbsp;

## 2.35. What just happened?
As the last hands-on tried to exemplify, creating threads and maintaining them is actually an expensive process that can consume significant resources from your machine.  
There's actually a limit that will be imposed by both the JVM and the OS on how many threads your program can create, but you should also keep in mind that if you achieve a number of threads that is disproportionally gigantic, you will in fact end up loosing performance as you will spend too much time just jumping from thread to thread.  
Thankfully in the environment that we are currently in we are unable to actually crash our system in a way that imposes grave consequences other than simply closing our program, thanks to those limits from the OS/JVM. 

But even if so, we don't really want our server to go down that easily, do we?

&nbsp;

## 2.36. So yea, that wasn't really that safe...
The problem with our server implementation as it is is that we are not in any way limiting the amount of threads that our program tries to create. This means that if either a malicious user, or simply a huge bunch of ordinary ones can cause our program to crash, intentionally or not.

&nbsp;

## 2.37. _**The EXECUTOR**_ ... framework.
Besides the [java.util.concurrent][java.util.concurrent-docs]'s containers that we have spoken about a bit before, this package provides you with some more very interesting and useful stuff.  
Some of which are the [java.util.concurrent.Executor][java.util.concurrent.Executor-docs] and [java.util.concurrent.ThreadPoolExecutor][java.util.concurrent.ThreadPoolExecutor-docs].

The image in the slides aims to illustrate the structure behind all the involved entities, let's try to understand at least some of all that's mentioned. The first three rectangles on the left are interfaces:

* [Executor][java.util.concurrent.Executor-docs] interface that defines the basic API for an object that is able to execute submitted `Runnable` tasks. (you will talk more about this in the next slide)
* [ExecutorService][java.util.concurrent.ExecutorService-docs] provides methods to manage termination and methods that are able to produce a [Future][java.util.concurrent.Future] for tracking progress of asynchronous tasks (Don't get _too_ scared about the `Future`. It's actually a concept similar to JavaScript's `Promise`)
* [ScheduledExecutorService][java.util.concurrent.ScheduledExecutorService-docs] is similar to the previous but allows scheduling of when to execute given tasks, either at a delay or an interval

The rest are Classes:

* [Executors][java.util.concurrent.Executors-docs] is this framework's equivalent of the Collections to the Collection framework, providing a lot of factory and utility methods for the classes in this package
* [AbstractExecutorService][java.util.concurrent.AbstractExecutorService-docs] is an abstract class that provides default implementation for [ExecutorService][java.util.concurrent.ExecutorService-docs] execution methods
* [ForkJoinPool][java.util.concurrent.ForkJoinPool-docs] is an [ExecutorService][java.util.concurrent.ExecutorService-docs] for running [ForkJoinTask][java.util.concurrent.ForkJoinTask-docs] (damn this language has some obscure cool shit. Read into this at your own leisure, but the general idea is that these are thread-like but light-weight objects intended to perform very small async tasks and the ForkJoinPool is the Executor meant to run them)
* [ThreadPoolExecutor][java.util.concurrent.ThreadPoolExecutor-docs] provides an [ExecutorService][java.util.concurrent.ExecutorService-docs] that executes each submitted task using one of possibly several pooled threads
* [ScheduledThreadPoolExecutor][java.util.concurrent.ScheduledThreadPoolExecutor-docs] is a [ThreadPoolExecutor][java.util.concurrent.ThreadPoolExecutor-docs] that can additionally schedule commands to run after a given delay, or to execute periodically.

&nbsp;

## 2.38. Executor interface
(although mentioned in the previous slide's notes I feel it makes more sense to bring the following up as you open this slide - Rolo)
Thanks to this new very powerful framework, we can further abstract the way we look at our application's operations, and we can instead of abstracting towards the concept of a `Thread` (which was at the same time the unit of work and the mechanism that was used to actually perform it), abstract towards the concept of a "task" (which would represent only a unit of work).  
Ideally those tasks should be independent activities, that don't depend on the state, result, or possible side-effects of other tasks, and the main mechanism that will be responsible for executing these tasks will be an `ExecutorService`.

The Executor interface in specific allows you to decouple a task's submission from its execution as long as they implement `Runnable`.  
(This slide's notes do not seem accurate as well, they are most likely meant for a concrete implementation of an executor instead, since the interface only really forces you to have a `void execute(Runnable)` method - Rolo)

&nbsp;

## 2.39. Why use these Executors?
The way we have been working directly with threads forces the creation of a new one each time we have a new task that we wish to set off. By making use of Executor entities we can reduce the amount of new threads created, since they will try to reutilise previously created worker threads in order to increase performance.

(The following would as well apply to a specific implementation such as the ThreadPoolExecutor, not exactly to the Executor interface...? - Rolo)  
Those executors also give you access to some more actions such as tuning, management, monitoring, logging or reporting errors.

&nbsp;

## 2.40. ExecutorService
This is a sub-interface of [Executor][java.util.concurrent.Executor-docs], and it provides some methods to allow you the managing of the [Executor][java.util.concurrent.Executor-docs]'s lifetime and the the submission of tasks.
This entity can be shut down, in which case it will stop accepting the submission of any new tasks.
You should not forget to shut down an ExecutorService when you are done using it, otherwise it will probably keep at least some of the threads it is managing running.  
This means for instance that your `main()` may actually finish its execution and the application might keep running since an ExecutorService is still active.

You can order this shut down to be done either graciously (`shutdown()`), in which current tasks are allowed to terminate but new ones are rejected, or abruptly (`shutdownNow()`), which will attempt to stop all actively executing tasks _and_ reject new ones.

&nbsp;

## 2.41. Creating new thread pools
There are several ways to create thread pools that you can read about in the documentation, but unless you want to specifically define any of the several possible settings the best way to create those is vie using one of the several static factory methods from the [Executors][java.util.concurrent.Executors-docs] class. (If you want to read up on these settings you know just the place, right?... )

&nbsp;

## 2.42. newFixedThreadPool(int nThreads)
Creates a thread pool that reuses a fixed number of threads operating off a shared unbounded queue. (in case you're not familiar with the concept, an unboundded queue is simply a queue that is not bound to a fixed size)  
This type of pool will create threads as tasks are submitted, up to the maximum specified size, and will attempt to keep the pool size constant by creating new threads in case one dies due to for example an unexpected Exception)

&nbsp;

## 2.43. newCachedThreadPool()
Creates a thread pool that creates new threads as needed, but will reuse previously constructed threads when they are available.  
A bit more flexible than a `FixedThreadPool`, as it will terminate idle threads when the current pool size is greater than currently demanded and will create new ones if the demand increases. This, however, does not impose a maximum size on the pool (for real? beware...)

&nbsp;

## 2.44. NewSingleThreadExecutor()
Creates an Executor that uses a single worker thread operating off of an unbounded queue.
The Executor will replace the thread in case it unexpectedly dies, and tasks submitted to this type of executor are guaranteed to be processed sequentially.  
(Found no reference in documentation as to the possibility of choosing what queue is used within the Executor, which leads me to believe that what is meant by this slide's last sentence refers to having the tasks come from a queue, and that being the one who determines the order, by submitting them to the executor by its standards -- must confirm - Rolo)

&nbsp;

## 2.45. {Exercise} How my web-server _held the door_
#### Objective

* Have the cadets understand how actually managing the number of threads we allow our implementation to have is a great perk, and make them do so in their web-servers.

#### Flow

* Ask the cadets to make their servers bullet proof by making use of their newly acquired knowledge of thread pools
* Proceed to test the strength of their servers once more by using the previous script again and see if they now hold up.

&nbsp;

## 2.46. {Exercise} Make that chat behave better than whatsapp!


&nbsp;

&nbsp;

#### Resources:

* [\[Video\] How computers work and difference between process and thread][process-vs-threads-video]

* [\[Video\] Introduction to Operating System Multitasking][multithreading-video]

* [\[Video\] Inter Process Communication][inter-process-communication-video]



[//]: # (THIS IS A WAY OF COMMENTING IN MARKDOWN! here as an example)

[//]: # (LINKS TO VARIOUS EXTERNAL RESOURCES)
[multithreading]: https://www.tutorialspoint.com/operating_system/images/thread_processes.jpg

[multithreading-video]: https://www.youtube.com/watch?v=t-zgY7zV9tk
[process-vs-threads-video]: https://www.youtube.com/watch?v=exbKr6fnoUw
[inter-process-communication-video]: <https://www.youtube.com/watch?v=W0BX6geRCDQ>
[basic-thread-mechanisms-video]: <https://www.youtube.com/watch?v=Hdd1BlnI4GQ>
[kernel-vs-user-level-threads-video]: <https://www.youtube.com/watch?v=_5q8ZK6hwzM>
[process-context-switch-video]: <https://www.youtube.com/watch?v=lS1GOdXFLJo>
[basic-thread-management-interactions-video]: <https://www.youtube.com/watch?v=oKJqqvnjl_s>

[thread-sleep-bad-post]: <https://blogs.msmvps.com/peterritchie/2007/04/26/thread-sleep-is-a-sign-of-a-poorly-designed-program/>
[asynchronous-programming-with-async-await-post]: <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/async/>
[semaphore-and-mutex-post]: <https://crunchify.com/what-is-java-semaphore-and-mutex-java-concurrency-multithread-explained-with-example/>
[thread-vs-runnable-post]:<https://www.callicoder.com/java-multithreading-thread-and-runnable-tutorial/>
[volatile-memory-consistency-post]: <https://dzone.com/articles/java-multi-threading-volatile-variables-happens-be-1>
[l1-l2-l3-cache-post]: <https://specialties.bayt.com/en/specialties/q/305444/what-is-the-difference-between-l1-l2-and-l3-cache-memory/>

[visualvm-site]:https://visualvm.github.io/documentation.html


[//]: # (LINKS TO IMAGES AND SIMILAR RESOURCES)
[single-core-cpu]: <resources/images/single-core-cpu.png>
[pre-emptive-multitasking]: <resources/images/pre-emptive-multitasking.png>
[multi-tasking-os]: <resources/images/multi-tasking-os.png>
[l1-l2-l3-cache]: <resources/images/l1-l2-l3-cache.png>
[dreamcrush-link]: <resources/images/crushdreams.png>


[//]: # (LINKS TO JAVA DOCUMENTATION)
[java.util.Hashtable-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/Hashtable
[java.util.Vector-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/Vector.html
[java.util.Collections-synchronizedCollection-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#synchronizedCollection(java.util.Collection)
[java.util.concurrent-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/package-summary.html
[java.util.concurrent.ConcurrentHashMap-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ConcurrentHashMap.html
[java.util.concurrent.CopyOnWriteArrayList-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/CopyOnWriteArrayList.html
[java.util.concurrent.Executor-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/Executor.html
[java.util.concurrent.ThreadPoolExecutor-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ThreadPoolExecutor.html
[java.util.concurrent.ExecutorService-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ExecutorService.html
[java.util.concurrent.Future]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/Future.html
[java.util.concurrent.ScheduledExecutorService-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ScheduledExecutorService.html
[java.util.concurrent.Executors-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/Executors.html
[java.util.concurrent.AbstractExecutorService-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/AbstractExecutorService.html
[java.util.concurrent.ForkJoinPool-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ForkJoinPool.html
[java.util.concurrent.ForkJoinTask-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ForkJoinTask.html
[java.util.concurrent.ThreadPoolExecutor-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ThreadPoolExecutor.html
[java.util.concurrent.ScheduledThreadPoolExecutor-docs]: https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ScheduledThreadPoolExecutor.html 
