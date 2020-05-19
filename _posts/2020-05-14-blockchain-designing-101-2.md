---
layout: post
title:  Blockchain Design 101 - Part 2
description: "Describes different blockchain designs like Proof-of-Work, Proof-of-Stake, Delegated-Proof-of-Stake and how they evolved."
category: articles
tags: [blockchain, block, design, PoA, PoS, DPoS]
image: ""
comments: true
---

This is the second part of blockchain design 101 series. You can read first part [here](/articles/2020/05/08/blockchain-designing-101-1/). In this part, we are going to talk about some different blockchain designs and how they evolved.

## Proof-of-Work

Proof of work blockchains gets their name on the fact node requires to do some work, in order to produce a block. So, more capable the node is more its probability to produce blocks. 

### Block construction

In Proof of work blockchain, To construct a valid block node need to find an answer to a computational puzzle. This puzzle need to be such that finding answer require node to put some effort in terms of resource usage (for example memory, cpu or network) but still feasible enough and verifying if that answer is correct need to be quick and easy. Effort required to calculate the solution can be quantified in terms of some unit of difficulty.

### Fork selection

A fork having most difficulty as sum of difficulties of all blocks contained can be seen as a fork chosen to extend by a set of nodes with the largest cumulative resources. So, a node is incentivized to select that fork to append new block, due to high probability of said block remaining canonical.

### Block finality

Pure proof of work blockchain offer probabilistic finality, because there is always some probability however small, that block can become non-canonical once another fork overtakes fork containing that block. Probability of that happening is inversely proportion to amount of difficulty added on top of said block by building more blocks on top of that block, as more difficulties added on top less chance for a fork created at height less than block to overtake said block's fork.

### Caveats

In proof of work blockchain every node need to do some effort while competing to produce the block, which is very costly in terms of energy usage. Since solving computational puzzle takes some time, block generation in Proof of work is slow by design.

## Proof-of-Stake

Proof of stake improves on Proof of work by shifting the requirement of block production for node to holding a stake in blockchain as opposed to working on finding solution to puzzle. This speeds up block production considerably. 

### Block construction

In proof of stake blockchain nodes who have locked up some stake in blockchain can only produce block and cast vote. Those nodes are called validators. More stake validator has more chance it has to produce the block. This stake acts as a collateral and incentivize the validator to act non-byzantine. 

### Block finality

Proof of stake blockchain offers either absolute finality or probabilistic finality. Probabilistic finality works same as Proof-of-Work blockchain.

In case of absolute finality support, multiple strategies exists:

1. Before finalizing previous block, next block cannot be constructed. In this case forks are not allowed, as it is not possible for any siblings of block to exists.

2. A distributed algorithm finalizing previous blocks depending upon certain parameters like votes casted on blocks,  

### Fork selection

Fork selection in Proof of stake system is completely implementation dependent.

### Caveats
