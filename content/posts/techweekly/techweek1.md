---
date: "2025-03-09"
draft: false
title: 'Start | King Weekly'
author: 'King Jin'
tags: ["Tech_Weekly","Algorithm","Email_system"]

showtoc: true
---

## Email sending and receiving system
The main system is build based on three protocols: SMTP, POP3 and IMAP.
![process of email system](/emailsys.png)

SMTP is used for sending emails to the recipient’s email server, but it does not handle receiving emails.
User1 sends an email via an email client, and the email is first sent to User1's email server using SMTP. Then, the email server forwards it to the recipient's email server using SMTP as well.

POP3 downloads emails from the email server to the email client. By default, it removes emails from the server after downloading, but some email clients allow users to keep copies on the server.
IMAP keeps emails on the server and synchronizes them across multiple devices. The email client initially loads only the headers, and the full email content is fetched from the server when the user opens it.

If you want to customize an email domain. You need to have your own SMTP and IMAP/POP3 server and a domain, the other steps are the same as above. 

-------
## PKGBUILD in Arch Linux
PKGBUILD is a bash script contain the build information required by archlinux package
we use makepkg script to build the package, it will search PKGBUILD first in the current folder.
![PKGBUILD process](/Hand_write_note/pkgbuild.jpg)
Benefits:
- using pacman to manage, user can update and uninstall easily
- some pkgbuild file include the commands to generate a binary file and store it in /user/bin

Drawbacks:
- Not friendly to starter

Although we can use yay to help us do all these stuff.

-------

## Trivias
1. Newton's method is quadratic convergence when we want to calculate the root of a number
2. Catalan number is a group of sequence that appear widely in combinatorics. e.g. ways to arrange n brackets, number of triangles in an n+2 convex polygon. The common property of these applications is that they are recursive and have a constrained structure.
3. Toom cook: It divide a d-digit number into n parts and doing arithmatic calculations.
4. Schonhage-strassen scheme: It multiplies two integers of length 𝑛 in O (𝑛 log𝑛 log log𝑛) steps on a multitape Turing machine
5. A Naive algorithm is usually the most obvious solution when one is asked a problem. It may not be a smart algorithm but will probably get the job done 
6. The taste of red wine is determined by acidity, sweetness, alcohol content, tannins, and body. Wines are categorized into New World and Old World. New World wines (from countries like the USA, Chile, Argentina, and China) are named after the grape variety, while Old World wines (mainly from Europe) are named after their place of origin.  
Red wine is made by fermenting red grapes with their skins. White wine is made from either white grapes or red grapes without their skins. Rosé wine is made by soaking the grape skins briefly but fermenting without them. Sparkling wine undergoes a second fermentation to produce bubbles.
7. Gabriel's horn is a type of geometric figure that has infinite surface area but finite volume. 

-------

## Resources
1. Code question(leetcode), system design question(crack the code interview), teamwork, communication are all important in the interview.
2. An old guideline to learn ai: [https://www.captainai.net/itcoke/](https://www.captainai.net/itcoke/)
3. A guideline to learn CS: [https://csdiy.wiki/后记/](https://csdiy.wiki/后记/)
3. Useful tips to integrate by parts, 反对幂指三, to choose u.
4. Customize your zsh: [oh my zsh](https://ohmyz.sh)  
5. Xiaomi releases a concept modular camera, it looks pretty awesome and innovative.
![](/Interesting_thing/Xiaomi_modular_camera.png)
6. 3b1b's taylor series explaination:https://www.youtube.com/watch?v=3d6DsjIBzJ4
7. 3b1b's explaination of why we have exponential e:https://www.youtube.com/watch?v=m2MIpDrF7Es
8. This website is all about competitive writing of source code that is as short as possible: [Codewolf](https://codegolf.stackexchange.com/)
9. Explaination of greedy algorithm: [greedy algorithm](https://houbb.github.io/2020/01/23/data-struct-learn-07-base-greedy)
10. Explaination of dynamic programming: [dynamic programming](https://houbb.github.io/2020/01/23/data-struct-learn-07-base-dp#%E9%A2%98%E7%9B%AE)
11. Deploy perosonal VPN tools: [tailscale](https://tailscale.com/)


## Abstract
If no one is reading blogs anymore, why should we write them?
Let’s make it simple: you write a blog, but nobody cares, nobody reads it.
At least, the number of readers is not as many as you thought.
You put your personal ideas and thoughts into the article, carefully structuring each sentence, and choose a great image—then, no response, no likes, no shares, no activity.
So, what is the meaning of writing a blog?
First, there are two misconceptions about blogging.
One is that if I write a good article, readers will come naturally.
No, they won’t come. There are billions of blogs on the internet, like a massive hurricane, and yours is just a single leaf in the wind. Who would notice?
Another misconception is that if nobody reads it, writing is a waste of time.
Blogs have their own hidden value.
You write blogs not for the applause of others, but for your own needs.
Blogs help clear your mind. They help you organize your thoughts and sharpen your perspective.
When you think better, you will achieve better results.
The target audience of a blog is actually not the people on the internet, but your future self. Your article will help you see the evolution of your own thoughts.
Additionally, one day in the future, someone who truly needs your article will find it.
A deep, thoughtful article has a longer-lasting impact than a viral article.
Writing a blog is quite like street photography. You take your camera and walk through the city.
You see a scene—a moment filled with light, shadow, and humanity—and then you capture it.
Nobody cares about what you actually captured. But that’s not the reason you photograph; you photograph because you see something interesting.
Writing a blog is the same. You write a blog because you are thinking, observing new things, and hope to store them somewhere.
If someone reads it, that's great. If not, you’ve still completed your work