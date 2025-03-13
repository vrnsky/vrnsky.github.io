---
title: Demystifying Java ClassLoaders - A deep dive into the JVM loading mechanism
type: blog
sidebar:
  open: true
date: 2025-03-13
comments: true
---

![Garbage Collector](/images/2025-03-14-classloaders/loading.png "Loading")

Have you ever wondered how your Java application finds all those imported classes?
Or maybe you've faced the dreaded ClassNotFoundException and felt lost in classloader confusion?
Perhaps you've dealt with dependency conflicts or library version issues in large applications.
All these problems come from one key mechanism in Java: classloaders.

In this article, I'll take you into the exciting world of Java's classloading.
We will explore how class loaders operate. We'll talk about their hierarchy. You'll learn how to use
them to solve real-world problems in your apps.

### What are ClassLoaders, anyway?
A classloader is what is sounds like. It's a part of the Java Virtual Machine (JVM) that loads class files.
When you run a Java program, the JVM doesn't load all classes at once. Instead, it loads
them on demand when they're referenced. This lazy - loading strategy is efficient. However, it needs a way to find and load class file when required.

That's where classloaders come in. They're responsible for

Finding class file - wheter they're in your local file system, inside JARs, or even across a network.
Loading the data class - reading the binary from the class file.
Defining the class - turning that binary data into a class object that the JVM can use.

The ClassLoader hierarchy: A three - tier system
Java doesn't use just one classloader; it uses a hierarchy of them. This hierarchy uses a delegation model. When a classloader needs to load class, it first asks its parent classloader. If the parent cant' load it, then the classloader tries to load the class itself.
The standard hierarchy consists of three main classloaders:
#### Bootstrap ClassLoader (Primordial ClassLoader)
The native code (not Java) implements this as the root of the classloader hierarchy.
It loads core Java classes from the rt.jar file and other core libraries in the `$JAVA_HOME/jre/lib directory.`
In Java 9+ with the module system, it loads classes from the modular JDK runtime.

Key classes loaded by the Bootstrap ClassLoader include:
- `java.lang.Object`
- `java.lang.String`
- `java.lang.System`
- And other fundamental classes in the java.* package

#### Extensions ClassLoader (Platform ClassLoader in Java 9+)
This ClassLoader is a child of the Bootstrap ClassLoader. It loads classes from Java extension
directories such as `$JAVA_HOME/jre/lib/ext`. It can also load classes from any directory specified by
the `java.ext.dirs` system property. In Java 9+, it was renamed to the Platform ClassLoader and load platform modules. 
This classloader typically handles:
- Security extension class
- JDBC drivers bundled with JDK
- Other standard extension


#### Application ClassLoader (System ClassLoader)
This classloader loads classes from the classpath. The classpath is set by the `CLASSPATH` environment variable or the `-classpath`
command-line option. It's responsible for loading your application class and third - party libraries.
The application class loader is what you'll interact with most often. It load:
- Your own application classes.
- Third - party libraries.
- Any other classes specified in the classpath.

### Access full article
{{< cards cols="3" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/demysifying-java-classloaders-a-deep-dive-into-the-jvms-loading-mechanism-94883de8819d" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://open.substack.com/pub/vrnsky/p/demysifying-java-classloaders-a-deep?r=3ypfws&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true"  >}}
{{< card icon="paper-airplane" title="Ghost" subtitle="Subscribe & read" link="https://vrnsky.ghost.io/demysifying-java-classloaders-a-deep-dive-into-the-jvms-loading-mechanism/"  >}}
{{< /cards >}}
