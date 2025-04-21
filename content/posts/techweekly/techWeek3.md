---
date: "2025-04-21"
draft: false
title: 'For UNIX Week | King Weekly'
author: 'King Jin'
tags: ["Tech_Weekly","Unix"]
showtoc: true
---
## Book - Unix: A History and a Memoir
Recently, I read this fantastic book. It bring me back to that 1960s - a period without modern computer and how the most clever minds in this world changed the world.
During the reading, I found many answers to the "why" questions I had when I learning linux system.
1. AT&T built Bell Labs and invited some of the most brilliant people in the world to do the most advanced scientific work. There was no limit on funding and no fixed goals for individuals.
2. The system developed before Unix was called Multics.
3. Since “Multics” already used “multi,” the early name of Unix was “Unics.”
4. Unix was first written on the PDP-7. The next version, written in C, was developed on the PDP-11. Fortunately, it wasn’t written for the PDP-10.
5. Tools like the shell, grep, regular expressions, the C language, the C compiler, yacc, lex, make, sed, awk, and troff were all invented at Bell Labs.
6. Unix eventually declined due to copyright issues. AT&T sold it as a product and made it proprietary, which gave rise to open-source Unix-like systems.
7. GNU is a Unix-like project that provides free and open-source alternatives. Under the GNU license, if you modify the source code of a project, the modified version must also remain open-source.
8. MacOS is based on BSD, which is a Unix-like system. The Linux kernel combined with GNU forms GNU/Linux. They both follow POSIX.
9. In the early days, operating systems were not portable. This changed with the invention of the C language and its compiler.
10. MINIX was widely used because it was embedded in Intel chips.
11. The working environment at Bell Labs in the 1970s are of hard problems, brilliant colleagues with shared dreams, and a unique management style that encouraged innovation.
12. Microsoft once had its 3own Unix-like system.
13. Another completely different path from Unix was MS-DOS, which eventually evolved into today’s Windows.
14. You can also get to know the geniuses of that era, like Ken Thompson, Richard Stallman, and Brian Kernighan.
15. “Everything is a file” is one of the core principles of Unix.
16. The KISS principle (“Keep It Simple, Stupid”) is a fundamental part of Unix philosophy.

The UNIX philosophy is very similar to some programming concepts I've recently learned at university. That's why, Its impact not only on system desisgn but also software deveopemnt and beyond.
1. Keep it simple stupid
2. Do one thing, and do it well
3. Everything is a file
4. Make each program a filter
5. Fail loudly
6. Modularity
7. Prototyping early

In today, many barriers had already been removed.  
And I realise.  
The revolution of AI is just like the reenactment of Unix's development.  
So.  
KISS.


## Trivias
1. tty - TeleTYpewriter, terminal in the old time, before lcd screen been invented.<img src="/TechStuff/Teletype_model_33.jpg" alt="teletype model 33" width="500" height="600">
2. UNIX was developed on the PDP-7, a computer with no screen, no mouse and only 8KB of RAM. It weighted nearly 500kg. ![pdp7](/TechStuff/Pdp7.jpeg)
3. UNIX and UNIX-like system use abbreviated commands because typing on TTY terminals in the 1960s was slow and insufficient.
4. Second-system effect: It believes that after completing a small, elegant, and successful system, people tend to have overly high expectations for the next projects, which may lead to the creation of a huge, feature-rich but monstrous system.The "second-system effect" can result in software project plans being overdesigned, with too many variables and excessive complexity, ultimately falling short of expectations and leading to failure. such as PL/I in Multics
5. Fortran(formular translation): The purpose of this lagnauge is to proceed mathematics formular and float number in an efficient way, like integration, linear algebra. That's why fortran is still popular in some supercomputer and scientific calculation.
6. B lagnauge is designed in a bit-unit computer PCP-7, where C langauge is designed in a byte-unit computer. Therefore the main difference between B and C is B langauge doesn't support types and C does.
7. Development of Clang: PL/I -> BCPL -> B -> New B(C)
8. If computers using the same cpu architecture, they will using the same assembly language.![assembly_langauge_with_architecture](/TechStuff/assembly_langauge_diff.png)
9. The grep command is used to find lines that match a specific pattern in a file while the sed command is used to insert, replace and delete text from a file. Finally, the awk command supports programming logic and is often used for advanced data processing tasks.
10. The development of UNIX from 1970 until now. ![road of unix](/TechStuff/roadOfUNIX.png)

## Talks
1. "A new technological discovery is often discredited by older generations of professionals - especially those with high authority and prestige in the existing field - in order to protect their own status"
