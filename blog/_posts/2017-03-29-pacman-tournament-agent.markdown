---
layout: single
title: Deep Q-Learning Pacman Tournament Agent
featured: true
date: '2017-03-29 04:12:00'
tags:
- classes
- machine-learning
- deep-learning
- projects
---

## [Github](https://github.com/jaredjxyz/Pacman-Tournament-Agent)

## Introduction

There is a very popular curriculum for Artificial Intelligence classes that is used at many universities throughout the world, one of those being the one I went to (UC Santa Cruz). This curriculum teaches path finding and decision making in the context of python-based Pacman game. It ends in a large tournament where teams in the class each make their own autonomous Pacman agent and that goes head-to-head in a round-robin style tournament. The trick with this tournament is that the rules of Pacman are changed, and we now have two teams playing against each other on the same playing field.

## Rules

Each team gets 2 agents. Each team gets half of the map as their 'home'. An agent starts at its home as a ghost. If an agent crosses to the other half of the map, it becomes a pacman, where it can both collect pacdots and be killed by any ghosts that may be lurking on that side of the map. An agent can only see enemy agents if they are 5 squares around it, otherwise it can get a rough, noisy distance estimate to its nearest enemy.

## My solution

### Deep Q Learning Offense

I had just learned how to implement Q learning in this class, and had just taught myself how to use Tensorflow, and had heard about Google using something called "Deep Q learning" to make their AlphaGo agent. After trying a basic q-learning approach and finding that it couldn't handle the edge cases that I needed it to, I decided to look up what exactly deep Q learning is and see if I could implement it. I ended up getting a 3-layer Q-learning network working and training relatively consistently on the program. Here's how it works.

input: 4x1 
layer1: tanh(matmul(input, w1) + b1) --> 4x1 
layer2: tanh(matmul(layer1, w2) + b2) --> 4x1 
layer3: relu(matmul(layer2, w2) + b3) --> 1x1 
loss: (layer3 - (reward + discount*V(state')) ^2, where V is the maximum Q value of all possible actions from state'

The features are as follows:
1. \# of food on opponent's side 
2. \# of food on our side 
3. A* distance from nearest edible thing (pacman, scared ghost, or pacdot) 
4. Distance from nearest ghost 

On each move, I ran one iteration of gradient descent. This worked really well for training against itself initially, but I found that it started to freeze up against other agents. I decided to make the baseline agent that was given to us a little dumber and slowly make it smarter so that my agent had some time to figure things out and train before it was defeated by the baseline agent. After being trained on multiple agents, including against a friend's agent that he let me train against, this ended up handling new situations relatively well. If I had more time, I would love to add new features and see how they affect the agent's behavior.

### Max Flow Defense

While debugging I found that my A* path finding algorithm that was looking for the nearest dot was crashing. When looking for where it was crashing I found that it didn't like this situation:

![block_example]({{ '/assets/images/2018/01/block_example.png' | relative_url }})

It turned out that the algorithm saw that there was a pacdot on the other other side of the wall but couldn't find a way to get to the dot without running into the green ghost (which I had told it was essentially a wall). This gave me an idea: If I purposefully put my ghost there, the enemy pacman would never be able to win, becuase my ghost would be blocking the enemy pac man from ever being able to reach the pacdots behind it. As it turned out, these bottlenecks existed in the large majority of the randomly generated maps. I immediately recognized this is a classic example of a Max Flow problem.

Here's the idea behind the solution I came up with. Every position on our side of the field is a vertex in the flow graph. Spots that can be reached from each other are each connected by two directed vertices of capacity 1. We then add a new node that will be our source that has an edge with infinite capacity connecting it and each of the vertices next to the center line.

The algorithm picks a pacdot and finds the maximum flow for that pacdot using the Ford-Fulkerson algorithm and A*. It then saves this flow, essentially "blocking" the pflow from the middle to that pacdot. It then goes along the path of that flow and, for each vertex along the flow's path, tries to find another flow to that vertex. The first vertex which it cannot reach is the bottleneck for that particular pacdot.

It does this for every pacdot on the map, then looks its new list of bottlenecks. It finds the point that appears the most in its list of bottlenecks and designates that the destination point.

This reliably finds the point on each new map with the largest number of pacdots behind it. The night that I finished this and submitted it, my agent went from 13th place to 4th place in the rankings. Unfortunately, big pacdots exist, and so if my pacman was affected by the big pacdot, their pacman could go right through us. This was the biggest weakness of this strategy.

## Results

Our team had been contending for the lead in the nightly test tournaments for a while, but never quite got to first place. On the final run, though, I had fixed some last-minute edge cases by adding some manual fixes to the offense's A* algorithm in order to make it avoid trapping itself in the corner.

We ended up getting the high win/lose ratio in the class, out of 43 teams.