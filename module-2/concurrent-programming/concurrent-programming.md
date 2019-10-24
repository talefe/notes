### **0. Contex**

A _program_ is just a set of instructions (think about Von Neumann machine we did in class).

#### **In order for a program to be executed:**

1. The instructions need to be stored in the system **RAM**.

2. Then sent to the **CPU** through the **Data, Address and Control BUSes**.

3. Once they enter the **CPU**, they go down a queue usually called **Pipeline**.

4. The **CPU** executes these instructions using various components (p.e. Math Processor) (Execution Engine is just a fancy name for many components).

5. For every **CPU** there is a **Clock** that runs at a certain frequency (p.e. 2GHz)

6. Eventually, each instruction will be executed.

   
  
   ![Single Core CPU][single-core-cpu]



We can think of a program as a _Thread_, a unit of execution - a set of instructions that together perform some specific task. On the days of MS-DOS and Command Line based OSes, applications were single threaded, so the set of instructions would just be read into the **CPU**.
We quickly moved to _Multi-Tasking Operating Systems_, where we wanted multiple applications open at once. 
In this example, **Word** and **Excel** are two different programs in execution in memory.

#TODO: summarize this image 

![Pre-emptive Multi-Tasking][pre-emptive-multitasking]

There are various approaches to implementing multi-tasking

![Multi-Tasking Operating Systems Implementations][multi-tasking-os]





#### Resources:

* [How computers work and difference between process and thread][process-vs-threads-video]
* [Introduction to Multitasking][multithreading-video]



### 1. Introduction

Writing correct programs is hard; writing concurrent programs is harder. More things can go wrong in a concurrent program compared to a sequential one.

**Why bother with concurrency?**

Threads are a great and inescapable feature of the Java language. The can _simplify the development of complex systems_ by turning asyncronous code into simpler straight-line code. Threads are the easiest way to tap the computing power of multiprocessor systems. [(processor counts increase)][processor]

![multithreading visual representation][multithreading]



#### 1.1. A Brief History of Concurrency

Before computers had operating systems, they executed a single program from beginning to end, and that program had direct access to all the resources of the machine which is an inefficient use of expensive and scarce computer resources.
Operating systems evolved to allow more than one program to run at once, running individual programs in processes: isolated, independently executing programs to which the operating system allocates resources such as memory, file handles, and security credentials. If they needed to, processes could communicate with one another through a variety of coarse-grained communication mechanisms: sockets, signal handlers, shared memory, semaphores, and files.



[single-core-cpu]: resources/images/single-core-cpu.png
[pre-emptive-multitasking]: resources/images/pre-emptive-multitasking.png
[multi-tasking-os]: resources/images/multi-tasking-os.png
[processor]:http://www.google.com
[multithreading]: https://www.tutorialspoint.com/operating_system/images/thread_processes.jpg
[multithreading-video]: https://www.youtube.com/watch?v=t-zgY7zV9tk
[multithreading-video-frame]: https://i.ibb.co/GR0q6gN/https-i-ytimg-com-vi-t-zg-Y7z-V9tk-hqdefault.jpg
[process-vs-threads-video]: https://www.youtube.com/watch?v=exbKr6fnoUw
[process-vs-threads-video-frame]: https://i.ibb.co/MMVd0mm/https-i-ytimg-com-vi-exb-Kr6fno-Uw-maxresdefault.jpg

