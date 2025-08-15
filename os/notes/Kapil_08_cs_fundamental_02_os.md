# 01-os-primer.md

### What is an Operating System (OS)? 
- An operating system (OS) is software that manages computer hardware and software resources while providing essential services for computer programs. It acts as an intermediary between hardware and applications, enabling user interaction with the computer.
  * Linux - different  distribution :- Ubunto, Kali
  * Windows - different  distribution :- - windows 10, 11
  * Unix
  * Android
  * MacOS  
  * iOS


* Functions of an Operating System - 
  * Process Management - Allocating system resources, scheduling processes, and managing process communication.
  * Memory Management - Allocating and managing memory resources, ensuring efficient memory usage and preventing memory leaks.
  * File System Management - Organizing and managing files and directories, providing file access and storage services.
  * Device Management - Managing hardware devices, handling device communication, and providing device drivers.
  * Security - Protecting system resources, controlling user access, and ensuring data privacy and integrity.
  * User Interface - Providing a user-friendly interface for user interaction, enabling users to interact with the system and applications.



However, for developers an operating system is-
* `Low-level APIs` - Developers can the low-level APIs to interact with the various components of a computer. For instance, a developer can use the `read` and `write` system calls to read and write to a file. You can use the `os` module in Python to interact with the operating system.
* `Resource Management` - An operating system manages the resources of a computer. For instance, it manages the memory of a computer. Multiple processes can run on a computer at the same time. However, each process has its own memory space. The operating system manages the memory of a computer and allocates memory to each process. It also manages the CPU of a computer. It schedules the processes to run on the CPU.




* Types of Operating Systems - Uniprogramming vs Multiprogramming/Multi-tasking/Multi-processing 
  *   Uniprogramming is a simple system where only one program can run at a time - e.g. MS-DOS, ATM, washing machine, watch
  *   Multiprogramming/Multi-tasking/Multi-processing - on the other hand, allows multiple programs to run concurrently by sharing the CPU and other resources. Multiprogramming increases system efficiency and throughput by overlapping CPU and I/O operations e.g. Laptop, Mobile, Servers.


Types of Multiprogramming/Multi-tasking/Multi-processing system - 

    * 1. Multi users vs single user -
      * Single-user operating systems are designed for a single user and are used on personal computers. Examples include - personal laptops, windows.
      * Multi-user operating systems are designed to support multiple users simultaneously. Users doesn't Know about each other user presense. Examples include Unix, Linux distributions like Red Hat Enterprise Linux, and Windows Server. AWS EC2.      
          
    * 2. Scheduling - Preemptive vs Non-Preemptive Scheduling - 
        * Preemptive scheduling allows the OS to interrupt a running process and allocate the CPU to another process based on priority or time quantum. 
        * Non-preemptive scheduling, on the other hand, does not interrupt a running process until it completes its execution or voluntarily yields the CPU.

### Process 
- When an application is installed on a system, it is stored as a disk/file. When the application is run, the operating system loads it into memory (RAM) and creates a process, which is an active instance of the application/program. 
    *   Each process has its own memory space and is managed independently. The operating system uses a Process Control Block (PCB) to store essential information about each process, such as its ID, state, priority, program counter, and CPU registers. The PCB acts as an identification card for processes, helping the OS manage them efficiently.
    *   The operating system assigns CPU time to processes as needed, especially for tasks like input/output operations, which only require the CPU at specific times. This ensures efficient multitasking and resource utilization.


    * Types of Processes - 
      * I/O-Bound Process: These processes spend most of their time waiting for input/output operations, like reading data from a disk/file or interacting with external devices.
      * CPU-Bound Process: These processes spend most of their time executing instructions, often involving intensive computations.

#### Burst time -- time taken by process to complete, it's mostly approximation based on previous completion time.

![Process Control Block](https://scaler.com/topics/images/structure-of-process-control-block.webp)

### Scheduling Algorithms - 
* First-Come, First-Served (FCFS): Non-Preemptive Scheduling- see document (01-os-primer.md) for more info if required.
  * Advantages - Simple and easy to implement, suitable for long CPU bursts.
  * Disadvantage - lower CPU utilization, poor response time for short processes.     
* Shortest Remaining Time First (SRTF) - Preemptive scheduling - see document (01-os-primer.md) for more info if required.
    * Advantages - Processes are executed faster than SJF, being the preemptive version of it
    * Disadvantage - Context switching is done a lot more times and adds to the more overhead time. It may still lead to starvation and requires the knowledge of process time beforehand. 
* Round Robin (RR) - Preemptive Scheduling - see document (02-round-robin-threads.md) for more info if required.
    * Advantages - Fair CPU allocation, prevents starvation, and ensures each process gets a chance to execute.
    * Disadvantage - High waiting time for processes with long CPU bursts, inefficient for short processes.Context switching.
    * Load balancer uses this algorithm to distribute the load among the servers.
    * If time quantum (time slices) is more then it will because FCFS.
* Priority Scheduling


* Why do we need Scheduling Algorithms? - A process requires both CPU and I/O time to complete execution. In multiprogramming systems, the CPU stays active by switching between processes, where one uses the CPU while another waits for I/O. In single-programming systems, CPU remains idle during I/O waits, wasting time.

####  The goals of scheduling algorithms are to:

    -Maximize CPU utilization and throughput
    -Ensure fair CPU allocation
    -Minimize turnaround, waiting, and response times


------------------------------------------------------------------------------------------------------------------------


---

--


--------------------------------------------------------------------------------------------------------

# 02-round-robin-threads.md

* Round Robin Scheduling - is a preemptive scheduling algorithm that assigns a fixed time slice (quantum) to each process in a circular queue. The time slice is usually a small value like 10ms. When a process's time slice expires, it is moved to the back of the queue, allowing the next process to run. RR ensures fair CPU allocation and prevents starvation by giving each process a chance to execute.

### Threads (watch **Video Number - 105 "CS Fundamentals: OS - Threads"** (Scaler that very good for Thread and process) ) 
- Each process has at-least one thread that is main thread.Thread is executed by Processor/CPU not Process.Process are like containers.
- A thread is a lightweight process. It is a unit of execution within a process. A process can have multiple threads. Each thread has its own program counter, stack, and registers. Threads share the same address space. This means that all threads in a process can access the same memory. This is different from processes where each process has its own address space (memory and resource).


- Often, a process needs to perform multiple tasks at the same time. For example, a web browser needs to download a file and display a web page at the same time. Creating a new process for each task is expensive. This is because creating a new process requires a lot of resources.
Threads are used to solve this problem. Threads are used to perform multiple tasks within a process. This is done by sharing the same address space. This means that all threads in a process can access the same memory. This is different from processes where each process has its own address space.

![Threads](https://scaler.com/topics/images/what-is-thread-in-os.webp)

### Thread vs Process
| Process                                                                          | Thread                                                                                                     |
| -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Processes use more resources and hence they are termed as heavyweight processes. | Threads share resources and hence they are termed as lightweight processes.                                |
| Creation and termination times of processes are slower.                          | Creation and termination times of threads are faster compared to processes.                                |
| Processes have their own code and data/file.                                     | Threads share code and data/file within a process.                                                         |
| Communication between processes is slower.                                       | Communication between threads is faster.                                                                   |
| Context Switching in processes is slower.                                        | Context switching in threads is faster.                                                                    |
| Processes are independent of each other.                                         | Threads, on the other hand, are interdependent. (i.e they can read, write or change another thread’s data) |
| Eg: Opening two different browsers.                                              | Eg: Opening two tabs in the same browser.                                                                  |

![Threads vs Process](https://scaler.com/topics/images/process-vs-thread.webp)

### Concurrency vs Parallelism

* Concurrent - At the same time, but not necessarily at the same instant. A single core CPU can only execute one thread at a time. But it can switch between threads very quickly. This is called context switching. This is how concurrency is achieved. A single core CPU can have concurrency but not parallelism.
* Parallel - At the same time and at the same instant. A single core CPU cannot achieve parallelism. It can only achieve concurrency. A multi-core CPU can achieve both concurrency and parallelism.
* Unicore vs Multicores - Unicore can have concurrency but not parallelism. Multicore can have both concurrency and parallelism.

### Using threads in Java


In Java, we can create a thread by extending the Thread class or by implementing the Runnable interface. The Thread class is a subclass of the Object class. It implements the Runnable interface. The Runnable interface has a single method called run(). This method is called when the thread is started.

```java
class NewThread implements Runnable {
    @Override
    public void run() {
        // Code to be executed by the thread
    }
}
```

We can create a new thread by creating an object of the NewThread class and passing it to the Thread class constructor. The Thread class constructor takes a Runnable object as an argument. This Runnable object is the thread that we want to create.

```java
NewThread newThread = new NewThread();
Thread thread = new Thread(newThread);
```

To run the thread, we call the start() method on the Thread object. This method calls the run() method of the Runnable object. The run() method is executed by the thread.

```java
thread.start();
```

#### Number printer

**Problem Statement**
* Create a new thread that prints the numbers from 1 to 10.

**Solution**
```java
class NumberPrinter implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i <= 10; i++) {
            System.out.println(i);
        }
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        NumberPrinter numberPrinter = new NumberPrinter();
        Thread thread = new Thread(numberPrinter);
        thread.start();
    }
}
```

**Problem Statement 2**
* Print the numbers from 1 to 10 where each number is printed by a different thread.

***Solution***
```java
class NumberPrinter implements Runnable {
    private int number;

    public NumberPrinter(int number) {
        this.number = number;
    }

    @Override
    public void run() {
        System.out.println(number);
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 1; i <= 10; i++) {
            NumberPrinter numberPrinter = new NumberPrinter(i);
            Thread thread = new Thread(numberPrinter);
            thread.start();
        }
    }
}
```

### Comparing Chrome and Firefox
Chrome and Firefox now both support multithreading, but they do it in different ways. In Chrome, each and every tab you open gets its own content process. Ten tabs, 10 processes. One hundred tabs, 100 processes.  One open tab in Chrome typically consumes hundreds of megabytes of RAM.This approach maximizes perfomance, but you pay a heafty penalty in memory consumption and battery life. Firefox doesn’t take this approach to the problem, but instead spins up to four content process threads by default. In Firefox, the first 4 tabs each use those 4 processes and additional tabs tun using threads within those processes. Multiple tabs within a process share the browser engine that already exists in memory, instead of each creating their own.

### Reading List

* [Web Browser architecture](https://levelup.gitconnected.com/how-web-browsers-use-processes-and-threads-9f8f8fa23371)
------------------------------------------------------------------------------------------------------------------------


--


--------------------------------------------------------------------------------------------------------

# 03-thread-synchronisation.md & 03-threads-synchronisation.md


### Thread Pool - 106 - "CS Fundamentals : Syncronisation and Deadlocks" (Scaler that very good for Thread and process) ) - Very good Merge sort example in Multithreading
- A thread pool is a collection of threads that are used to execute tasks. Instead of creating a new thread for each task, a thread pool reuses the existing threads to execute the tasks. This improves the performance of the application.
- Thread pool e.g --> C3P0, HikariCP, DBCP, Tomcat, Jetty, etc.
- Every application will be running as process which has one main thread.

### Executor

    It is a simple interface with a single method, void execute(Runnable command).

    **Purpose**: It decouples the task define/submission from the details of how each task will be executed (e.g., creating a new thread or reusing existing threads).
    Example:

    Executor executor = command -> new Thread(command).start();
    executor.execute(() -> System.out.println("Task executed"));

### ExecutorService

    A more advanced subinterface of Executor, providing methods to manage and control thread lifecycle.

    Adds functionality for:
        Submitting tasks: Returns a Future to track the result of asynchronous computations.
        Shutting down: Gracefully or forcefully stops the service (shutdown() or shutdownNow()).
        Scheduled tasks: Some implementations, like ScheduledExecutorService, support delayed and periodic execution.

    Key Methods:
        submit(Callable<T> task) or submit(Runnable task)
        invokeAll(Collection<? extends Callable<T>> tasks)
        invokeAny(Collection<? extends Callable<T>> tasks)

    Example:

    ExecutorService executorService = Executors.newFixedThreadPool(2);

    // Submit a task
    Future<String> future = executorService.submit(() -> "Task result");
    try {
        System.out.println(future.get());
    } catch (Exception e) {
        e.printStackTrace();
    }

    // Shutdown
    executorService.shutdown();

### Executers

    A utility class that provides factory methods for creating different types of ExecutorService instances.

    Key Methods:
        newFixedThreadPool(int nThreads)
        newCachedThreadPool()
        newSingleThreadExecutor()
        newScheduledThreadPool(int corePoolSize)

    Example:

    ExecutorService executorService = Executors.newFixedThreadPool(2);
    executorService.submit(() -> System.out.println("Task executed"));

### Callable and Future 

    What it is: A functional interface similar to Runnable, but it can return a result and throw a checked exception.

    Method: It has a single method, V call(), where V is the type of the result.

    Use case: Suitable when you need to perform a task that returns a result or might throw an exception.

      public interface Callable<V> {
      V call() throws Exception;
      }

      ExecutorService executorService = Executors.newCachedThreadPool();
      Future<Integer> future = executorService.submit(() -> 2 + 3);
      Integer result = future.get();


    Futures can be used to cancel tasks. The Future interface has a method called cancel that can be used to cancel a task. The cancel method takes a boolean parameter. If the boolean parameter is true, the task is cancelled even if the task is already running. If the boolean parameter is false, the task is cancelled only if the task is not running.
    
    ExecutorService executorService = Executors.newCachedThreadPool();
    Future<Integer> future = executorService.submit(() -> 2 + 3);
    future.cancel(false);

### CompletableFuture vs ExecutorService

    A powerful class in Java 8 that represents a future result of an asynchronous computation.

    Key Features:
        asynchronous & Non-blocking computation
        Chaining: You can chain multiple computations together using methods like thenApply, thenAccept, and thenCompose.
        Exception handling: Provides methods like exceptionally and handle for error handling.

    * Rule of Thumb
      * Use ExecutorService when you want low-level control over task submission and threads.
      * Use CompletableFuture when you want asynchronous, non-blocking, and chainable operations, especially in modern Java (8+).

### CompletableFuture.runAsync() vs supplyAsync()

Both methods are used to start asynchronous tasks in Java, but they differ in whether they return a result.


| Feature               | `CompletableFuture.runAsync()`                                      | `CompletableFuture.supplyAsync()`          |
|-----------------------|---------------------------------------------------------------------|---------------------------------------------|
| Returns a result?     | ❌ No                                                                | ✅ Yes                                      |
| Input type            | `Runnable` (no return value)                                        | `Supplier<T>` (returns a value of type `T`) |
| Result type           | `CompletableFuture<Void>`                                           | `CompletableFuture<T>`                      |
| Typical use case      | Fire-and-forget background task <br/>like logging, updating a cache | Async computation that returns a result     |
| Custom executor?      | ✅ Optional                                                          | ✅ Optional                                  |


```java
   
    //runAsync --> Use this when the task performs an action but doesn't return a result.
    CompletableFuture.runAsync(() -> {
            System.out.println("Running in background...");
    });

    //supplyAsync --> Use this when the task returns a value that you want to use in further processing.
    CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> 42);    
    future.thenAccept(result -> System.out.println("Result: " + result));

     //Both methods can take a custom executor:
     ExecutorService executor = Executors.newFixedThreadPool(2);
     CompletableFuture.runAsync(() -> doSomething(), executor);
     CompletableFuture.supplyAsync(() -> computeValue(), executor);

    //allOf --> Waits for all provided futures to complete.
    CompletableFuture<Void> all = CompletableFuture.allOf(
            CompletableFuture.runAsync(() -> doTask("A")),
            CompletableFuture.runAsync(() -> doTask("B")),
            CompletableFuture.runAsync(() -> doTask("C"))
    );
     all.join(); // Waits until all tasks are done

    //anyOf --> Waits for any of the provided futures to complete.
    CompletableFuture<Object> fastest = CompletableFuture.anyOf(
            CompletableFuture.supplyAsync(() -> fetchFromDB()),
            CompletableFuture.supplyAsync(() -> fetchFromCache())
    );
    fastest.thenAccept(System.out::println);
    
    //exceptionally --> Handle exceptions in a non-blocking way.
    CompletableFuture.supplyAsync(() -> {
            if (true) throw new RuntimeException("Oops!");
    return "Success";
            }).exceptionally(ex -> "Recovered from error: " + ex.getMessage())
            .thenAccept(System.out::println);

     //Custom Thread Pool
     ExecutorService executor = Executors.newFixedThreadPool(4);
     CompletableFuture.supplyAsync(() -> 42, executor)
            .thenApplyAsync(x -> x * 2, executor)
            .thenAcceptAsync(System.out::println, executor);
     
     
     //Timeout Handling (Java 9+)
     CompletableFuture.supplyAsync(() -> {
            Thread.sleep(5000);
    return "Done";
            }).orTimeout(2, TimeUnit.SECONDS)
          .exceptionally(ex -> "Timeout!");

```

### ForkJoinPool
    - CompletableFuture.supplyAsync() and runAsync() use the common ForkJoinPool by default: you can pass your own thread ppol as well see "Custom Thread Pool" above 
    - A specialized implementation of ExecutorService designed for parallel processing of tasks that can be broken down into smaller subtasks.
    - Think of ForkJoinPool as a smart thread pool that helps you run lots of small tasks concurrently, often using work stealing to keep all threads busy.
    - ForkJoinPool is a powerful concurrency tool in Java designed to execute parallel, divide-and-conquer tasks efficiently.


| Feature           | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| Parallelism       | Designed to maximize CPU usage using multiple threads                       |
| Work stealing     | Idle threads can "steal" tasks from busy threads’ queues                    |
| Default size      | Equal to the number of available CPU cores (unless specified)               |
| Default pool      | Used by `CompletableFuture` if no custom executor is passed                 |
| Recursive support | Supports breaking a task into subtasks using `RecursiveTask` or `RecursiveAction` |

---

### Thread Context Switching - not good as it takes time due to stack re-creation.    

---

### Web Server vs Application Server

| **Aspect**           | **Web Server**                          | **Application Server**                                                              |
|-----------------------|-----------------------------------------|-------------------------------------------------------------------------------------|
| **Primary Role**      | Serves static content (HTML, CSS, JS).  | Handles dynamic content and business logic.                                         |
| **Focus**             | HTTP-based communication.              | Backend services and middleware.                                                    |
| **Complexity**        | Lightweight and simple.                | Feature-rich and more complex.                                                      |
| **Content Served**    | Static files (e.g., images, HTML, JS).  | Dynamic responses from server-side logic.                                           |
| **Supported Protocols** | HTTP/HTTPS.                           | HTTP, HTTPS, RMI, JMS, etc.                                                         |
| **Use Case**          | Hosting static websites or acting as a reverse proxy. | Running enterprise applications, handling transactions, interacting with databases. |
| **Examples**          | Apache HTTP Server, Nginx, IIS.         | Apache Tomcat, JBoss/WildFly, WebLogic, WebSphere, Jetty.                           |
| **Additional Features** | Load balancing, SSL termination, and caching. | Transaction management, security, message queuing, connection pooling.              |
| **Integration**       | Often forwards requests to an application server. | Integrates with databases, APIs, and other backend systems.                         |

------------------------------------------------------------------------------------------------------------------------


--

--


--------------------------------------------------------------------------------------------------------

# 04-synchronisation.md

### Characteristics of synchronisation problems
* `Critical section` - A section of code that is accessed by multiple threads. When multiple threads access the same critical section, the result is a synchronisation problem that might yield wrong or inconsistent results.

```java
    public void run() {
        for (int i = 0; i < 100; i++) {
            count.increment(); // Read/Write/update/Modify shared resource - Critical section 
        }
    }
```
* `Race Conditions` - When more than one thread tries to enter the critical section at the same time.
* `Preemption` - When a thread is interrupted by another thread. It could be possible that the interrupted thread is in the middle of a critical section. This could result in the interrupted thread not being able to finish the critical section and yield inconsistent results.

### Properties of a good solution
* `Mutual Exclusion` - Only one thread can access the critical section at a time. It avoid Race condition.
* `Progress` - If a thread wants to enter the critical section, it will eventually be able to do so. Overall system should be progressing.
* `Bounded Waiting` - If a thread wants to enter the critical section, it will eventually be able to do so, but only after a finite number of other threads have entered the critical section.
* `No busy Waiting` - No pull mechanism to check to enter (pull mechanism is not good it will use CPU cycle). If a thread wants to enter the critical section, it will not be able to do so until the critical section is free. It has to keep checking if the critical section is free. This is called busy waiting.
* `Notification` - Push mechanism (Good way) - If a thread is waiting to enter the critical section, it should be notified when the critical section is free.

### Solutions to synchronisation problems

* `Mutex` - Mutual Exclusion - Locks - In order to solver the concurrency issue, we can use mutexes or locks. In Java this can be achieved by simply wrapping the critical section in a synchronised block.
* `Syncronised keyword`
* `Semaphore`

------------------------------------------------------------------------------------------------------------------------


--



--------------------------------------------------------------------------------------------------------

# 04-memory-management.md

### Producer and consumer problem - check document 03-thread-synchronisation.md to fix the problem & watch video 108 - "CS Fundamental : semaphores and Memory Management"
Overflow and underflow - 

Redis and HashMap/Hashtable  internally uses semaphore for multithreading.
CountdownLatch

### DeadLock and Memory Management -- watch video 109 - "CS Fundamental : Deadlocks and Memory Management"
Timeout vs Heart beat - Timeout is when you wait for a certain amount of time before you give up. Heat-beat is when you keep checking if the other party is alive.


* Process -- stored in main - memory/RAM.
##### Computer storage devices - 
  * Volatile storage - Data is lost when the power is turned off. e.g. Registers, Cache and RAM
    * Registers - CPU uses registers to store data that is currently being processed. Registers are the fastest form of memory.
    * Cache - OS uses cache to store the data that is frequently accessed by the CPU. Cache is faster than main memory.
    * Main Memory/RAM - OS uses main memory to store the data that is currently being used by the CPU. Main memory is slower than cache. Applications and data(including) are stored in main memory.
  * Non-volatile storage - Data is not lost when the power is turned off. e.g. Hard disk, SSD, USB, CD, DVD, etc.
    * Secondary Memory storage - SD card, Hard disk, SSD, USB, CD, DVD, etc.
  
  

CPU doesn't interact with the main memory directly. It interacts with the cache. Cache interacts with the main memory. Main memory interacts with the secondary memory. Secondary memory interacts with the disk.


Disk is slower than RAM. RAM is slower than cache. Cache is slower than CPU registers.

Disk is cheaper than RAM. RAM is cheaper than cache. Cache is cheaper than registers.

Size of storage - Registers(KB) < Cache(MB) < RAM(GB) < Disk (TB)

CPU doesn't directly interact with disk rather data bus interact with disk.

RAM - divided into fixed contiguous blocks called pages. Each page is further divided into fixed-size blocks called frames. The size of a page is equal to the size of a frame.

### Memory Management Unit (MMU) 
- Hardware component that maps virtual addresses to physical addresses. Check watch video 109 - "CS Fundamental : Deadlocks and Memory Management" 

### Java General :- 

* Java statically type language - Memory is allocated at compile time. C and C++ are dynamically typed language - Memory is allocated at runtime.
* Java is pass by value - Java is always pass by value. In Java, when we pass a primitive data type to a method, a copy of the value is passed to the method. When we pass an object to a method, a copy of the reference to the object is passed to the method. The reference is passed by value to the method.
* Java is platform-independent - Java is platform-independent because it uses the Java Virtual Machine (JVM) to run the Java code. The JVM is an abstract machine that provides a runtime environment for Java programs. The JVM converts the Java bytecode into machine code that can be executed by the underlying hardware. This allows Java programs to run on any platform that has a JVM installed.


* String - non primitive data type in Java. String is immutable in Java. String pool is a pool of strings stored in the heap memory. String pool is a part of the heap memory.
* Char is stored as ASCII value in memory. so char ch = 'A' will store 65 in memory. char ch = 'a' will store 97 in memory.
* Ascii table - 256 characters. Unicode - 2^16 characters. Ascii is a subset of Unicode.
* UTF-8 - 1-4 bytes. UTF-16 - 2 bytes. UTF-32 - 4 bytes.
* Implicit type casting - Implicit casting is done by the compiler. Small data type to big data types. e.g. int a = 10; long b = a;
* Explicit type casting - Big data type to small data type. Explicit casting is done by the programmer. e.g. Explicit casting is done by the programmer. e.g. long a = 10; int b = (int) a;
  * byte - 1 byte (8 bits) 
  * short - 2 bytes 
  * int - 4 bytes 
  * long - 8 bytes 
  * float - 4 bytes 
  * double - 8 bytes 
  * char - 2 bytes
  * boolean - 1 byte
* implicit conversion from left to right --> byte -> short -> int -> long -> float -> double.
* explicit conversion from right to left --> double -> float -> long -> int -> short -> byte.
  * loss of information - double -> float -> long -> int -> short -> byte.
  * Overflow - when the value is more than the maximum value that can be stored in a data type. e.g. byte b = 128; //overflow
    * Explicit conversions
      * int x = (int) 3.14f --> 3
      * int y = (int) 0.9 --> 0
      * char ch = (char) 65.5 --> 'A'

* char can't be assigned to byte and short. 
* byte b = 25 --- allowed as byte range is -128 - 127
* byte b = 128 --- not allowed as byte range is -128 - 127


* float f = 2.5 //not allowed - exception
* float store integral and exponential value separately.


* 1 byte = 8 bits
* byte - 1 byte - 8 bits - range -128 to 127
* short - 2 bytes - 16 bits - range -2^15 to 2^15 - 1
* int - 4 bytes - 32 bits - range -2^31 to 2^31 - 1
* long - 8 bytes - 64 bits - range -2^63 to 2^63 - 1
* float - 4 bytes - 32 bits - range -3.4e+38 to 3.4e+38
* double - 8 bytes - 64 bits - range -1.7e+308 to 1.7e+308
* char - 2 bytes - 16 bits - range 0 to 65535


* Heap - objects stored in heap memory. Garbage collection is done in heap memory. 
* Stack - reference variables stored in stack memory
  * Stack memory is used for method calls and local variables. 
  * Stack memory is faster than heap memory. Stack memory is limited. 
  * Stack memory is thread-safe. Stack memory is not shared among threads. Stack memory is automatically managed by the JVM. Stack memory is divided into frames. Each frame is created when a method is called. Each frame is destroyed when the method is returned. Stack memory is used for static

* Heap memory is used for dynamic memory allocation. Heap memory is used to store objects. Heap memory is shared among threads. 
  * Heap memory is not thread-safe. Heap memory is managed by the garbage collector. 
  * Heap memory is divided into two parts - Young Generation and Old Generation. 
    * Young Generation is further divided into 
      * Eden Space, Survivor Space Zero, and Survivor Space One. 
    * Old Generation is used to store long-lived objects. 
  

* String pool - String pool is a pool of string literals stored in the heap memory. String pool is a part of the heap memory. String pool is used to store unique strings. When a string is created, it is stored in the string pool. If another string with the same value is created, it is not stored in the string pool. Instead, a reference to the existing string is returned. This is done to save memory. String pool is used to store unique strings. When a string is created, it is stored in the string pool. If another string with the same value is created, it is not stored in the string pool. Instead, a reference to the existing string is returned. This is done to save memory.



* Immutable classes - Immutable classes are thread-safe
  * String
  * Wrapper classes - Integer, Float, Double, Long, Short, Byte, Character, Boolean, BigDecimal, BigInteger.

```java
String s1 = "abc";
s1 = s1 + "egf"; //IMPORTANT - This concatenation creates a new String object on the heap (not from the pool)
String s2 = "abcegf";
String S3 = new String ("abcegf");

s1 == s2 //false
s2 == s3 //false
s1.equals(s2) // true
s2.equals(s3) //true
```
- Atomicity	- Operation is indivisible (e.g., int x = 5;)
- Visibility - One thread sees changes made by another

- Volatile  - Guarantees visibility but not atomicity
  * Volatile variables are not cached in registers or CPU caches. They are always read from and written to the main memory (Heap - RAM). This ensures that all threads see the most up-to-date value of the variable.
  * Volatile variables are not atomic. This means that if two threads try to update the same volatile variable at the same time, it can lead to inconsistent results.
  * Volatile variables are not thread-safe. This means that if two threads try to update the same volatile variable at the same time, it can lead to inconsistent results.

- Synchronized - Guarantees visibility + mutual exclusion (atomicity)

- Key Areas of Memory in JVM - 
  * Heap - Used for dynamic memory allocation. All objects are stored in heap memory. Heap memory is shared among all threads.
  * Stack - Used for static memory allocation. All local variables are stored in stack memory. Stack memory is not shared among threads.
  * Method Area (aka Metaspace in modern JVMs) - Used to store class-level data. This includes static variables, constants, and method code. Method area is shared among all threads.
  * PC Register - Each thread has its own PC register. It stores the address of the currently executing instruction.
  * Thread Working Memory - Each thread keeps a local copy of variables it’s working with. Synced with main memory (heap) through reads/writes.

Multithreading and the JMM -
When multiple threads are involved:
    Each thread may cache values from main memory in its local working memory.
    One thread’s changes might not be visible to another unless:
        A volatile keyword is used.
        A synchronization mechanism is used (synchronized, Lock, etc.).

```Java
volatile boolean flag = false;

Thread 1: flag = true;
Thread 2: while (!flag) { /* wait */ }
```

* Reference copy vs shallow copy vs deep copy - https://medium.com/swlh/reference-copy-shallow-copy-and-deep-copy-63f9418c9c51
  * Reference copy - Copying the reference of an object. Both the original object and the copied object point to the same memory location. If the original object is modified, the copied object is also modified.
  * Shallow copy - Copying the values of the primitive data types and the references of the non-primitive data types. The copied object has its own memory location. If the original object is modified, the copied object is not modified. However, if the non-primitive data types are modified, the copied object is also modified.
  * Deep copy - Copying the values of the primitive data types and the values of the non-primitive data types. The copied object has its own memory location. If the original object is modified, the copied object is not modified. If the non-primitive data types are modified, the copied object is not modified.


**Java 8 Features:**
1. Some significant features introduced in Java 8 are:
  - **Lambda Expressions:** A concise way to represent anonymous functions, enabling functional programming in Java.
  - **Functional Interfaces:** Interfaces that have only one abstract method, used to enable lambda expressions.
  - **Default Methods:** Methods that have a default implementation in an interface, allowing backward compatibility when adding new methods to interfaces.
  - **Streams API:** A new API for processing collections of data using functional-style operations.

2. Functional interfaces are interfaces that have exactly one abstract method. The "@" symbol is used to indicate that an interface is a functional interface, and it helps in avoiding accidental addition of multiple abstract methods, which would break compatibility with lambda expressions.

3. Example of using lambda expressions in Java 8:

   ```java
   // Before Java 8
   new Thread(new Runnable() {
       public void run() {
           System.out.println("Hello from a thread!");
       }
   }).start();

   // With lambda expression in Java 8
   new Thread(() -> System.out.println("Hello from a thread!")).start();
   ```

2. The Singleton design pattern ensures that a class has only one instance and provides a global point of access to that instance. It is used in scenarios where only one instance is required throughout the application.

3. The Observer design pattern is used to establish a one-to-many dependency between objects, where the subject (observable) notifies its observers (listeners) of any state changes. It is commonly used in event handling and GUI frameworks.

4. The Factory Method pattern is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created. It promotes loose coupling between classes and makes the code more extensible.


* Clone vs copy constructor
---

###  Blocking queue 

* BlockingQueue Comparison - BlockingQueue is a thread-safe queue that supports operations that wait for the queue to become non-empty when retrieving an element and wait for space to become available in the queue when storing an element.
* LinkedList is also queue implementation but it is not thread-safe. BlockingQueue is thread-safe.
* Queue<TreeNode> queue = new LinkedList<>();
```java 

| Queue Type              | Capacity      | Ordering                  | Use Case                                 |
|-------------------------|---------------|------------------         |------------------------------------------|
| LinkedBlockingQueue     | Optional      | FIFO (Linked List based)  | Producer-consumer, large queues,         |
| ArrayBlockingQueue      | Fixed         | FIFO (Array Based)        | High-throughput, memory-tight systems    |
| PriorityBlockingQueue   | Unbounded     | Priority-based            | Task scheduling, priority processing     |
| DelayQueue              | Unbounded     | Time-delayed              | Retry queues, expiring cache entries     |
```

* various - add/remove operations -
* Three categorization of methods:-
  * offer/poll - Non-blocking methods (also tim )
  * add/remove - Exception-throwing methods
  * put/take - Blocking methods

```java
      ## 🟢 Common Methods to Add Elements (BlockingQueue) - 
      
      | Method                                      | Behavior                                                                 |
      |---------------------------------------------|--------------------------------------------------------------------------|
      | `add(E e)`                                  | Adds the element or throws `IllegalStateException` if full (for bounded queues) |
      | `offer(E e)`                                | Adds the element, returns `true` if successful, `false` if full         |
      | `offer(E e, long timeout, TimeUnit unit)`   | Waits up to timeout to insert, returns `false` if timeout expires       |
      | `put(E e)`                                  | Blocks indefinitely until space is available                             |
      
      
      ## 🔴 Common Methods to Remove Elements (BlockingQueue) - 
      
      | Method                                          | Behavior                                                          |
      |-------------------------------------------------|-------------------------------------------------------------------|
      | `take()`                                        | Waits (blocks) until an element is available, then returns it     |
      | `poll()`                                        | Retrieves and removes head, returns `null` if empty               |
      | `poll(long timeout, TimeUnit unit)`             | Waits up to timeout for an element, returns `null` if timeout expires |
      | `remove()`                                      | Removes head element or throws `NoSuchElementException` if empty  |
      | `peek()`                                        | Returns head element without removing, or `null` if empty         |


        ## 💡 Tip: Choosing the Right Method - 

        | Goal                        | Recommended Method(s)                  |
        |-----------------------------|----------------------------------------|
        | Non-blocking insert/remove  | `offer()` / `poll()`                  |
        | Blocking behavior           | `put()` / `take()`                    |
        | Time-bounded behavior       | `offer(e, timeout, unit)` / `poll(timeout, unit)` |

```

###  PriorityBlockingQueue implementation

```java      

public class Task implements Comparable<Task> {
  private static final AtomicInteger COUNTER = new AtomicInteger(0);

  private final int priority; // lower value = higher priority
  private final String name;
  private final int id;

  public Task(int priority, String name) {
    this.priority = priority;
    this.name = name;
    this.id = COUNTER.incrementAndGet(); // unique for logging
  }

  public String getName() {
    return name;
  }

  @Override
  public int compareTo(Task other) {
    return Integer.compare(this.priority, other.priority);
  }

  @Override
  public String toString() {
    return "Task{id=" + id + ", name='" + name + "', priority=" + priority + "}";
  }
}


public class PriorityQueueExample {
  public static void main(String[] args) throws InterruptedException {

    PriorityBlockingQueue<Task> queue = new PriorityBlockingQueue<>();

    // Producer thread - submits tasks with different priorities
    Thread producer = new Thread(() -> {
      queue.add(new Task(3, "Low priority"));
      queue.add(new Task(1, "High priority"));
      queue.add(new Task(2, "Medium priority"));
    });

    // Consumer thread - processes tasks in priority order
    Thread consumer = new Thread(() -> {
      try {
        while (true) {
          Task task = queue.take(); // blocks until a task is available
          System.out.println("Processing: " + task);
          Thread.sleep(500); // simulate task processing
        }
      } catch (InterruptedException e) {
        Thread.currentThread().interrupt();
      }
    });

    producer.start();
    consumer.start();

    producer.join(); // wait for producer to finish, pause the main thread and wait until the producer thread finishes submitting all its tasks before moving on.
    Thread.sleep(3000); // let it process some tasks
    consumer.interrupt(); // stop the consumer
  }
}
```

###  Database connection pool manual creation using singleton pattern
- Creating a connection pool in Java means efficiently managing a set of database connections that can be reused, rather than creating and closing connections each time — which is costly
- use a library like HikariCP, C3P0, or Apache DBCP to manage the connection pool.

- LinkedBlockingQueue is a thread-safe queue implementation,
- It handles all necessary synchronization internally, Methods like poll(), offer(), and clear() are safe to call from multiple threads concurrently.
   ```Java
   
   public class SafeConnectionPool {
    private static volatile SafeConnectionPool instance; // Double-checked locking
    private final BlockingQueue<Connection> pool;
    private final int maxPoolSize;
    private final String jdbcUrl;
    private final String username;
    private final String password;

    private SafeConnectionPool(String jdbcUrl, String username, String password, int maxPoolSize) throws SQLException {
        this.jdbcUrl = jdbcUrl;
        this.username = username;
        this.password = password;
        this.maxPoolSize = maxPoolSize;
        this.pool = new LinkedBlockingQueue<>(maxPoolSize); // LinkedBlockingQueue is a thread-safe queue implementation.

        for (int i = 0; i < maxPoolSize; i++) {
            pool.offer(createConnection());
        }
    }

    public static SafeConnectionPool getInstance(String jdbcUrl, String username, String password, int maxPoolSize) throws SQLException {
        if (instance == null) {
            synchronized (SafeConnectionPool.class) {
                if (instance == null) {
                    instance = new SafeConnectionPool(jdbcUrl, username, password, maxPoolSize);
                }
            }
        }
        return instance;
    }

    private Connection createConnection() throws SQLException {
        return DriverManager.getConnection(jdbcUrl, username, password);
    }

    public Connection getConnection(long timeout, TimeUnit unit) throws SQLException {
        try {
            Connection conn = pool.poll(timeout, unit);
            if (conn == null || conn.isClosed()) {
                throw new SQLException("No available connection from pool");
            }
            return conn;
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            throw new SQLException("Interrupted while waiting for a DB connection", e);
        }
    }

    public void releaseConnection(Connection conn) {
        if (conn != null) {
            try {
                if (!conn.isClosed()) {
                    pool.offer(conn);
                } else {
                    pool.offer(createConnection());
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public void shutdown() {
        for (Connection conn : pool) {
            try {
                if (!conn.isClosed()) {
                    conn.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        pool.clear();
    }
   }
  
   //Usage Example with Singleton :
   public class App {
    public static void main(String[] args) {
        try {
            SafeConnectionPool pool = SafeConnectionPool.getInstance(
                "jdbc:postgresql://localhost:5432/mydb",
                "myuser",
                "mypassword",
                5
            );

           // Simulate multiple threads
            for (int i = 0; i < 10; i++) {
                new Thread(() -> {
                    try {
                        Connection conn = pool.getConnection(5, TimeUnit.SECONDS);
                        System.out.println("Got connection: " + conn);
                        // Do DB work here...
                        Thread.sleep(1000); // Simulate query
                        pool.releaseConnection(conn);
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }).start();
            }

            // Optional shutdown hook
            Runtime.getRuntime().addShutdownHook(new Thread(pool::shutdown));

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
   }
```

```

### Thread pool Manual implementation - 

```Java
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;

public class ManualThreadPool {
    private volatile static ManualThreadPool instance;

    private final BlockingQueue<Runnable> taskQueue;
    private final Thread[] workerThreads;
    private volatile boolean isRunning = true; //ThreadPool is running not shut down

    private ManualThreadPool(int poolSize) {
        taskQueue = new LinkedBlockingQueue<>();
        workerThreads = new Thread[poolSize];

        for (int i = 0; i < poolSize; i++) {
            workerThreads[i] = new Worker("Worker-" + i);
            workerThreads[i].start();
        }
    }

    // Singleton accessor
    public static ManualThreadPool getInstance(int poolSize) {
        if (instance == null) {
            synchronized (ManualThreadPool.class){
               if(instance == null){
                 instance = new ManualThreadPool(poolSize);
               }
            }            
        }
        return instance;
    }

    // Submit a task
    public void submit(Runnable task) {
        if (isRunning) {
            taskQueue.offer(task);
        } else {
            throw new IllegalStateException("ThreadPool is shut down");
        }
    }

    // Shutdown the pool
    public void shutdown() {
        isRunning = false;
        for (Thread worker : workerThreads) {
            worker.interrupt();
        }
    }

    // Worker class
    private class Worker extends Thread {
        public Worker(String name) {
            super(name);
        }

        public void run() {
            while (isRunning || !taskQueue.isEmpty()) {
                try {
                    Runnable task = taskQueue.take(); // blocks until a task is available
                    task.run();
                } catch (InterruptedException e) {
                    // Allow thread to exit if pool is shutting down
                    if (!isRunning) break;
                } catch (Exception e) {
                    System.err.println("Task execution failed: " + e.getMessage());
                }
            }
        }
    }
}

```

### Semaphore vs CountDownLatch

```java

//CountDownLatch - You want one or more threads to wait until a set of operations being performed in other threads 

    CountDownLatch latch = new CountDownLatch(3);
    Runnable worker = () -> {
        System.out.println("Task done");
        latch.countDown(); // decrement the latch
    };
    
    new Thread(worker).start();
    new Thread(worker).start();
    new Thread(worker).start();
    
    latch.await(); // main thread waits until count = 0
    System.out.println("All tasks completed.");


//Semaphore - You want to limit concurrent access to a resource (e.g., max 3 threads accessing a database).

      Semaphore semaphore = new Semaphore(3); // max 3 permits
      Runnable task = () -> {
          try {
              semaphore.acquire(); // acquire permit
              System.out.println("Accessing resource...");
              Thread.sleep(1000);
          } catch (InterruptedException e) {
              e.printStackTrace();
          } finally {
              semaphore.release(); // release permit
          }
      };
      
      for (int i = 0; i < 10; i++) {
          new Thread(task).start();
      }
//Only 3 threads run concurrently; others wait for a permit.

* When to Use What? -
    * Use CountDownLatch when you want one or more threads to wait until a fixed number of events are completed.
    * Use Semaphore when you want to control concurrent access to a shared resource.

```

##### CountDownLatch vs 🚦 Semaphore – Real-World Analogy
| Feature              | CountDownLatch                         | Semaphore                                   |
|----------------------|----------------------------------------|---------------------------------------------|
| Real-world analogy   | 🚀 Rocket launch countdown              | 🅿️ Parking lot with limited spots           |
| Purpose              | Wait for N threads/tasks to complete   | Limit concurrent access to a resource       |
| Resettable           | ❌ No (one-time use)                   | ✅ Yes (permits can be reused)              |
| Counting direction   | Down to zero                           | Up/down (permits increment/decrement)       |
| Wait mechanism       | `await()`                              | `acquire()`                                 |
| Signal mechanism     | `countDown()`                          | `release()`                                 |
| Typical use case     | Task coordination                      | Resource throttling / concurrency control   |

### LRU Cache MRC Cache - implementation 
https://chatgpt.com/c/682b3d45-e668-8005-b306-047b4e9a1fc4


--------------------------------------------------------------------------------------------------------