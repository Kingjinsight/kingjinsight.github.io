---
date:  "2025-02-13"
draft: false
title: "Ambitious Cross-Platform Dream: JVM\'s Achievements and Limitations"
author: 'King Jin'
tags: ["JVM","Java","Programming"]
showtoc: true
---
This semester, I learned OOP from Inf1B, which using java as the official teaching language. What fascinates me the most is why Java has the JVM. I learned Python, C++, js and Haskell before, but all of them doesn't have a jargon for virtual machine. And then I went to wikipeidia to find out why.

> In 1995, Sun Microsystems introduced Java and the JVM to the world with an ambitious dream: "Write Once, Run Anywhere." This WORA philosophy became a reality through the JVM, enabling Java applications to run on any operating system with a compatible JVM. Before talking about the archivements and limitations, Let's have a look about how JVM works.

## How the JVM works
The JVM executes er programs in several stages:

1. Compilation: Java source code (.java) is compiled into bytecode (.class) by the Java Compiler (javac).

2. Class Loading: The JVM loads compiled bytecode when required.

3. Bytecode Verification: Ensures security and correctness before execution.

4. Execution: The JVM interprets or compiles bytecode using Just-In-Time (JIT) compilation.

5. Garbage Collection: The JVM automatically manages memory, reclaiming unused objects.

## Class loader
One of the organizational units of JVM byte code is a class. A class loader implementation must be able to recognize and load anything that conforms to the Java class file format. Any implementation is free to recognize other binary forms besides class files, but it must recognize class files.   

Let's explore this concept with an example:      
Imagine you're watching a movie on a streaming service.   
- Loading:   
    The service first finds and imports the movie data you want to watch. Similarly, the class loader locates the binary data for a Java class.   
- Linking:   
    - Verification: Before you watch the movie, the service checks that the file isn't corrupted. In Java, the class loader verifies the correctness of the class.   
    - Preparation: The service sets up the necessary space in memory to buffer the movie. Java allocates memory for variables and sets default values.   
    - Resolution: The service ensures all necessary subtitles or audio tracks are ready to play. Java resolves references to make them direct.   
- Initialization:   
    As you start watching, the service begins playing the movie. Similarly, Java runs code to set up variables with their starting values.   

Class Loader Types:   
- Bootstrap Class Loader: Like the service's core library of well-known movies, it loads fundamental, trusted classes.   
- Extension Class Loader: Similar to special add-on features, it loads additional classes outside the core library.   
- System/Application Class Loader: Like searching for new releases or user-uploaded content, it loads classes specific to the application you’re using.   
 
## Virtual machine architecture
![](/JvmSpec7.png)


## Cross-Platform Compatibility and Limitations
The JVM abstracts away the underlying hardware and operating system specifics, allowing Java bytecode to run on any device equipped with a compatible JVM. This cross-platform capability greatly simplified software distribution and development, as developers could write code once and deploy it across various platforms without modification.

Despite its strong cross-platform capabilities, the JVM faced significant challenges due to competitive corporate strategies, particularly the "Embrace, Extend, and Extinguish" (EEE) approach adopted by some companies like Microsoft in the late 1990s. This strategy involved embracing a technology, extending it with proprietary features, and eventually using those extensions to undermine the original technology.

Microsoft initially embraced Java by integrating it into their Internet Explorer browser and Windows platforms. However, they extended Java with proprietary features that were specific to Windows, creating a version of Java that was incompatible with the standard JVM specifications set by Sun Microsystems. This move fragmented the Java platform and undermined the "Write Once, Run Anywhere" philosophy.

With the development and rise of programming languages like Swift, Kotlin, and JavaScript, the JVM faced significant challenges in maintaining its performance edge. Swift, designed by Apple for iOS and macOS platforms, offers high performance and safety due to its compiled nature and modern language features. Kotlin, although initially running on the JVM, introduced concise syntax and advanced features that surpassed Java in many ways, leading it to become the preferred language for Android development. JavaScript's performance greatly improved with engines like V8, and its versatility expanded through technologies like Node.js for server-side development. These languages not only matched but often exceeded the JVM's performance and adaptability in their respective domains, leading to a shift in developer preferences and a relative decline in the JVM's dominance.

## Overall
Nowadays, Java has become to a normal programming lauguage. And the question is obvious solved. Python has its own interpreter to transfer the source code into machine code. Haskell has its own compiler, C++/C are compiled directly into machine code. However,they can't generate a compiled file that enable to run in every operating system. If there is no EEE strategy, Linux may have a stronger effects in today's world.