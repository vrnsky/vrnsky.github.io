---
title: Understanding Java Memory Model and Thread Safety
type: blog
sidebar:
  open: true
date: 2025-03-20
comments: true
---
![Headline image](/images/2025-03-20-jmm/headline.png)
In today's world of multiple-core processors, it is vital to know how Java manages memory and threads. This understanding helps in creating strong, high - performance applications. We often overlook basic understanding threading mechanisms as developers. But when issues arise - and they will knowing the core concepts can save your hours of debugging.

### Java Memory Model: More than heap and stack
The Java Memory Model (JMM) defines how threads interact through memory. It's not just about how we organize memory. It's also about the rules that control visibility, atomicity, and the order of memory operations.
When Java code runs, each thread gets its own stack, storing local variables and method call information. But all threads share the heap, which contains all objects your program allocates. This shared nature is strong but risky. It lets threads communicate, but it can lead to race conditions.
The JMM, introduced in Java 5 (JSR - 133), provides guarantees about when changes made by one thread become visible to other. Before we dive into the details, let's understand why this matters.
Consider this code that appears to be harmless:
```java {filename="SharedData.java"}
class SharedData {
  private boolean ready = false;
  private int value = 0;

  //Thread A
  public void producer() {
    value = 42;
    ready = true;
  }

  // Thread B
  public void consumer() {
    while(!ready) {
      //wait
    }
    assert value == 42; //This might fail!
  }
}
```
This should work base on common understanding. Thread A set value to 42, then signals ready . Thread B waits until ready is true, then reads value . But in reality, this code is flawed for several reasons:
Reordering: The JVM or processor might reordered instructions, setting ready = true , before value = 42 .
Visibility: Even if instructions execute in order, Thread B might not see the updated value.
Infinite loop: Thread B might nnever see the update to ready and loop forever.

### Memory visibility and the "happens-before" relationship
The Java Memory Model introduces concept of "happens - before" relationships. If operation A happens before operation B, then B can see A's effect. Without this connection we can't be sure about visibility.
Some ways to establish a happens - before relation include:
Program order: Operations in the same thread follows happens - before ordering.
Monitor locks: Using a monitor happens - before acquiring the same monitor.
Volatile variables: Writing to a volatile variables happens - before reading it.
Thread operations: Starting a thread happens - before any actions in that thread.

Let's fix our previous example using volatile variable
```java {filename="SharedData.java"}
class SharedData {
  private volatile boolean ready = false;
  private int value = 0;

  //Thread A
  public void producer() {
    value = 42;
    ready = true;
  }

  // Thread B
  public void consumer() {
    while(!ready) {
      //wait
    }
    assert value == 42; //This might fail!
  }
}
```
The `volatile` keyword does two things:
It prevents instruction reordering around the volatile access.
It ensures memory visibility of variables modified before a volatile write.

Atomic operations and race conditions
One common misconception is that all basic operations in Java are atomic. They're not. For example, the operations `count++` , which appears innocent, consist of three distinct operations.
- Read the current value.
- Increment it.
- Write it back.

This creates a window for race conditions. If two threads execute count++ concurrently:
```
Thread A: Read count (value: 5)
Therad B: Read count (value: 5)
Thread A: Increment to 6
Thread B: Increment to 6
Thread A: Write 6
Thread B: Write 6
```
The final value is 6, not 7 as expected. To fix this, we need atomic operations or synchronization. Java provides several ways to handle atomic operations:
Synchronization: Using synchronized blocks or methods.
Atomic classes: Using classes like AtomicInteger or AtomicReference .
Lock interfaces: Using ReentrantLock , ReadWriteLock , etc.

Here's an example with AtomicInteger :
```java {filename="Counter.java"}
import java.util.concurrent.atomic.AtomicInteger;

class Counter {
  private AtomicInteger count = new AtomicInteger(0);

  public void increment() {
    count.incrementAndGet();
  }

  public int getCount() {
    return count.get();
  }
}
```

### Access full article
{{< cards cols="3" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/understanding-java-memory-model-and-thread-safety-f7eed4c08509" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://open.substack.com/pub/vrnsky/p/understanding-java-memory-model-and?r=3ypfws&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true"  >}}
{{< card icon="paper-airplane" title="Ghost" subtitle="Subscribe & read" link="https://vrnsky.ghost.io/understanding-java-memory-model-and-thread-safety/"  >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)
