---
date: "2025-06-30"
draft: false
title: 'Some notes about Python | King Weekly'
author: 'King Jin'
tags: ["Tech_Weekly","Python"]
showtoc: true
---
## The Global Interpreter Lock (GIL)
At its core, the Global Interpreter Lock, or GIL, is a lock that only allows one thread to execute Python bytecode at a time within a single process. This means that even on a multi-core processor, a standard Python program with multiple threads will only utilize a single core for executing Python code.
It is also for compatibility with large number extension modules written in C. These C extensions may not have built-in thread safety mechanisms, so GIL provides a safety net to ensure that they are executed in a single-threaded environment.
The primary reason for the GIL's existence lies in Python's memory management.

## Python's Memory Management
Python uses a system called automatic memory management. Each object in Python has a reference count, which is a number that keeps track of how many variables or other object refer to it. When you assign a variable to an object, its reference count increases by one. When a reference is removed (for instance, when a variable goes out of scope), the count decreases. Once an object's reference count drops to zero, it means nothing is using it.

This is where GIL becomes important. In a multi-threaded program, multiple threads could try to increase or decrease the same object's reference count simultaneously, which may cause memory leaks.

## Python 3.13
GIL has become a bottleneck for CPU program performance, by reconstruct python, the development team has made a groundbreaking change in Python 3.13: the ability to disable the GIL.

## Why python slow
1. GIL
2. Dynamic Datatype.
3. It's an interpreter language
4. Easy to read makes python very abstract


## Trivias
1. Generating functions are a powerful mathematical tool that transform discrete sequences into algebraic functions, enabling us to solve complex combinatorial counting problems through function operations.
2. GPOS vs RTOS
   1. General purpose operating systems like Windows, macOS, and Linux are designed to provide a versatile, user-friendly computing environment. They prioritize overall system efficiency, with more flexible restrictions on task response times.
   2. Real time operating systems such as VxWorks, focus on strict time limitations for individual tasks, ensuring predictable and deterministic responses. These systems are typically used in environments demanding high reliability and precise time control, featuring a smaller, more streamlined kernel that guarantees real-time performance.
3. In python, Boolean type is essentially a subclass of the integer type, True == 1 and False == 0. This design is mainly due to historical reasons and pragmatic considerations. In early version of Python(before 2.3), there was no dedicated bool type, and people used integers 1 and 0 to represent true and false. When the bool type was introuced, in order to allow old code to continue to run seamlessly, it was the best choice to continue to design it as a subclass of int.
```True + 1 = 2, False * 1 = 0```
1. Huffman coding, an algorithm to compress data losslessly. Huffman coding assigns variable-length binary codes to input symbols.
   - More frequent symbols -> shorter codes
   - Less frequent symbols -> longer codes
2. Windows vs Linux
| Aspect                    | Linux                                     | Windows                                      |
| ------------------------- | ----------------------------------------- | -------------------------------------------- |
|  **System Usage**       | Lightweight, minimal background processes | Heavy, many preloaded services and features  |
|  **Bloatware**          | No pre-installed junk, user chooses all   | Comes with many default apps and features    |
|  **Transparency**       | Fully open, config files are plain text   | Many hidden processes, registry-based config |
|  **Customizability**    | Highly customizable, from kernel to GUI   | Limited customization without hacking        |
|  **Privacy & Security** | User-controlled, minimal telemetry        | Sends telemetry, often needs antivirus       |
|  **Software Support**   | Great for dev tools, less for gaming      | Excellent app/game compatibility             |
|  **System Control**     | Full control over system and services     | Some restrictions, frequent auto-updates     |
|  **Hardware Support**   | Good but sometimes manual setup required  | Plug-and-play for most consumer hardware     |

## Resouces

1. Why the formular of normal distribution has a pi:[explain from 3b1b](https://www.youtube.com/results?search_query=normal+distrubution+in+astronomy)

## Talks
漫士！
<iframe width=100% height=475  src="https://www.youtube.com/embed/nBkr4u_xKms?si=6CY9MwRS2KIN2mzr" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>