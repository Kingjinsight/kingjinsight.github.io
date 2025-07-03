---
date: "2025-04-26"
draft: false
title: 'Hopfield Network'
author: 'King Jin'
tags: ["AI","Algorithm"]
showtoc: true
---
2024 Nobel Physics prize was earned by Professor John Hopfield and Professor Geoffrey Hinton, to thanks their distribution on machine learning.
However, I felt very suprised that why it gives to machine learning? Anyway, I hadn't deeply find the answer in that time.

Recently, Professor Geoffrey Hinton gived us a short lecture about Boltzmann machine virtually.
And before the lecture, I learned Hopfield Network(the predecessor of Boltzimann machine) at my accommodation.
So today I will record this moment.

Hopfield Network was invented at 1982. Processor John Hopfield designed it based on ideas from statistical mechanics.

![metaphor](/Hand_write_note/hopfield_network_metaphor.png)
The graph above shows two states of a ball
From the left part, we can see the energy system of the ball is at the highest, which means the ball is very unstable
From the right part, we can see the ball had already fall into the bottom, which means the ball is very stable.
Although it is a classical physics model, but it definitly explain the main idea of hopfield network.

So now we can say hopfield network is just make a system move from an unstable state to stable state.

If you interested how exactly hopfield network work. See the video below, it's pretty nice.
<iframe width=100% height=475 
src="https://www.youtube.com/embed/1WPJdAW-sFo?start=505" 
title="YouTube video player" 
frameborder="0" 
allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
allowfullscreen>
</iframe>

This idea is also useful in today. 
In LLM, we can say the user's prompt and question is the most unstable states while the answer is the stable state.

Based on the concept of Hopfield networks, many different architectures had been invented, which makes Connectionism and Deep Learning great again.

After all, I catch the reason why nobel prize gives to physics.