# 01-os-primer.md

### What is an Operating System (OS)? 
- An operating system (OS) is software that manages computer hardware and software resources while providing essential services for computer programs. It acts as an intermediary between hardware and applications, enabling user interaction with the computer.
  * Linux - different  distribution :- Ubunto, Kali
  * Windows - different  distribution :- - windows 10, 11
  * MacOS
  * Unix
  * Android
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
    * If time quantam (time slices) iks more then it will because FCFS.
* Priority Scheduling


* Why do we need Scheduling Algorithms? - A process requires both CPU and I/O time to complete execution. In multiprogramming systems, the CPU stays active by switching between processes, where one uses the CPU while another waits for I/O. In single-programming systems, CPU remains idle during I/O waits, wasting time.

####  The goals of scheduling algorithms are to:

    -Maximize CPU utilization and throughput
    -Ensure fair CPU allocation
    -Minimize turnaround, waiting, and response times


------------------------------------------------------------------------------------------------------------------------

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

### Thread Context Switching - not good as it takes time due to stack re-creation.


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
* `No busy Waiting` - No poll mechanism to check to enter (pull mechanism is not good it will use CPU cycle). If a thread wants to enter the critical section, it will not be able to do so until the critical section is free. It has to keep checking if the critical section is free. This is called busy waiting.
* `Notification` - Push mechanism (Good way) - If a thread is waiting to enter the critical section, it should be notified when the critical section is free.


### Solutions to synchronisation problems

* `Mutex` - Mutual Exclusion - Locks - In order to solver the concurrency issue, we can use mutexes or locks. In Java this can be achieved by simply wrapping the critical section in a synchronised block.
* `Syncronised keyword`
* `Semaphore`

------------------------------------------------------------------------------------------------------------------------


# 04-memory-management.md

### Producer and consumer problem - check document 03-thread-synchronisation.md for to fix the problem & watch video 108 - "CS Fundamental : semaphores and Memory Management"
Overflow and underflow - 

Redis and HashMap/Hashtable  internally uses semaphore for multithreading.
CountdownLatch

### DeadLock and Memory Management -- watch video 109 - "CS Fundamental : Deadlocks and Memory Management"
Timeout vs Heat beat - Timeout is when you wait for a certain amount of time before you give up. Heat-beat is when you keep checking if the other party is alive.


* Process -- stored in main - memory/RAM.
* Computer storage devices - 
  * Registers - CPU uses registers to store data that is currently being processed. Registers are the fastest form of memory.
  * Cache - OS uses cache to store the data that is frequently accessed by the CPU. Cache is faster than main memory.
  * Main Memory/RAM - OS uses main memory to store the data that is currently being used by the CPU. Main memory is slower than cache. Applications and data(including) are stored in main memory.
  * Secondary Memory storage - SD card, Hard disk, SSD, USB, CD, DVD, etc.

CPU doesn't interact with the main memory directly. It interacts with the cache. Cache interacts with the main memory. Main memory interacts with the secondary memory. Secondary memory interacts with the disk.

* Volatile storage - Data is lost when the power is turned off. e.g. Registers, Cache and RAM
* Non-volatile storage - Data is not lost when the power is turned off. e.g. Hard disk, SSD, USB, CD, DVD, etc.

Disk is slower than RAM. RAM is slower than cache. Cache is slower than CPU registers.

Disk is cheaper than RAM. RAM is cheaper than cache. Cache is cheaper than registers.

Size of storage - Registers(KB) < Cache(MB) < RAM(GB) < Disk (TB)

CPU doesn't directly interact with disk rather data bus interact with disk.

RAM - divided into fixed contiguous blocks called pages. Each page is further divided into fixed-size blocks called frames. The size of a page is equal to the size of a frame.


### Memory Management Unit (MMU) - Hardware component that maps virtual addresses to physical addresses. Check watch video 109 - "CS Fundamental : Deadlocks and Memory Management" 

### Java General :- 

* Java statically type language - Memory is allocated at compile time. C and C++ are dynamically typed language - Memory is allocated at runtime.
* Java is pass by value - Java is always pass by value. In Java, when we pass a primitive data type to a method, a copy of the value is passed to the method. When we pass an object to a method, a copy of the reference to the object is passed to the method. The reference is passed by value to the method.
* Java is platform-independent - Java is platform-independent because it uses the Java Virtual Machine (JVM) to run the Java code. The JVM is an abstract machine that provides a runtime environment for Java programs. The JVM converts the Java bytecode into machine code that can be executed by the underlying hardware. This allows Java programs to run on any platform that has a JVM installed.


* String - non primitive data type in Java. String is immutable in Java. String pool is a pool of strings stored in the heap memory. String pool is a part of the heap memory.
* Char is stored as ASCII value in memory. so int a = 'A' will store 65 in memory. int a = 'a' will store 97 in memory.
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
      * Eden Space, Survivor Space, and Old Generation. 
    * Old Generation is used to store long-lived objects. 
    
  * Heap memory is used for dynamic memory allocation. Heap memory is used to store objects. Heap memory is shared among threads. Heap memory is not thread-safe. Heap memory is managed by the garbage collector. Heap memory is divided into two parts - Young Generation and Old Generation. Young Generation is further divided into Eden Space, Survivor Space, and Old Generation. Old Generation is used to store long-lived objects.


* String pool - String pool is a pool of strings stored in the heap memory. String pool is a part of the heap memory. String pool is used to store unique strings. When a string is created, it is stored in the string pool. If another string with the same value is created, it is not stored in the string pool. Instead, a reference to the existing string is returned. This is done to save memory. String pool is used to store unique strings. When a string is created, it is stored in the string pool. If another string with the same value is created, it is not stored in the string pool. Instead, a reference to the existing string is returned. This is done to save memory.



* Immutable classes - Immutable classes are thread-safe
  * String
  * Wrapper classes - Integer, Float, Double, Long, Short, Byte, Character, Boolean, BigDecimal, BigInteger.

```java
String s1 = "abc";
s1 = s1 + "egf"; //IMPORTANT - 
String s2 = "abcegf";

s1 == s2 //false
s2 == s3 //true
```

PECS - Producer extends Consumer super -


* Reference copy vs shallow copy vs deep copy - https://medium.com/swlh/reference-copy-shallow-copy-and-deep-copy-63f9418c9c51
  * Reference copy - Copying the reference of an object. Both the original object and the copied object point to the same memory location. If the original object is modified, the copied object is also modified. 
  * Shallow copy - Copying the values of the primitive data types and the references of the non-primitive data types. The copied object has its own memory location. If the original object is modified, the copied object is not modified. However, if the non-primitive data types are modified, the copied object is also modified. 
  * Deep copy - Copying the values of the primitive data types and the values of the non-primitive data types. The copied object has its own memory location. If the original object is modified, the copied object is not modified. If the non-primitive data types are modified, the copied object is not modified.

* Clone vs copy constructor  