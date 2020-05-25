---
layout: post
title:  Blockchain Design 101 - Part 2
description: "Describes what goes under the hood of two most popular blockchain designs Proof-of-Work and Proof-of-Stake."
category: articles
tags: [blockchain, block, design, PoA, PoS, DPoS]
image: ""
comments: true
---

This is the second part of blockchain design 101 series. You can read first part [here](/articles/2020/05/08/blockchain-designing-101-1/). In this part, we are going to talk about two of the most popular blockchain designs.

## Proof-of-Work

Proof of work blockchain gets its name from the fact that node requires to do some work, in order to produce a block.

### Block construction

In Proof of Work blockchain, To construct a valid block node need to find an answer to a computational puzzle. This puzzle needs to be such that finding an answer requires a node to put significant but finite and quantifiable effort in terms of resource usage (for example memory, CPU, or network), but verifying correctness of that answer need to be quick and easy. Effort required to calculate the solution can be quantified in terms of amount of resources utilized and can be expressed in units of difficulty. Every node competes in finding a solution and producing a block as quickly as possible. So, a node with more resources has more probability of producing a block in lesser time and consequently more probability of including it in the blockchain.

### Fork selection

A fork having most difficulty as sum of difficulties of all blocks contained can be seen as a fork chosen to extend by a set of nodes with the largest cumulative resources. So, a node is incentivized to select that fork to append new block, due to high probability of said block remaining canonical. Due to amount of effort required to produce a block, nodes are discouraged to extend multiple forks concurrently.

### Block finality

Pure proof of work blockchain offer probabilistic finality. There is always some probability however small, that block can become non-canonical once another fork at less height overtakes that block's fork by increasing its own difficulty quicker. Probability of that happening is inversely proportion to amount of difficulty added on top of said block, as more difficulties added on top less chance for a fork created at height less than block to overtake said block's fork.

### Caveats

In proof of work blockchain every node need to do some effort while competing to produce the block, which is very costly in terms of energy usage. Since solving computational puzzle takes some time, block generation in Proof of work is slow by design.

## Proof-of-Stake

Proof of stake differs with Proof of work by shifting the requirement of block production for node to holding a stake in blockchain as opposed to working on finding solution to puzzle. This speeds up block generation considerably.

### Block construction

In proof of stake blockchain nodes that have locked up some stake in blockchain can only produce block and make an assertion. More stake node has more probability of it to produce the block and more weight to its assertions. In most implementations to make sure nodes act honestly, every node is required to put some portion of its stake as collateral which can be slashed if misbehavior proof is found. Validating a block require nodes with combined majority stake to assert that said block is valid.

### Block finality

Proof of stake blockchain offers either absolute finality or probabilistic finality. Probabilistic finality works same as Proof-of-Work blockchain.

In case of absolute finality support, most common strategies employed by different implementations are as follows:

1. Before finalizing previous block, next block cannot be constructed. In this case forks are not allowed, as it is not possible for any siblings of a block to exists.

2. A distributed algorithm finalizing blocks depending upon certain parameters like block age, combined stake of nodes asserted validity of that block, number of blocks built upon that block etc.

3. A distributed algorithm finalizing a block depending upon finality assertions made by nodes for that block or its descendants.

### Fork selection

Fork selection in Proof of stake system is completely implementation dependent. Protocol level mechanism is required to discourage nodes to extend multiple forks.

### Caveats

Since in proof of stake blockchain there isn't any physical anchoring of blockchain as opposed to proof of work where you have to spend real world energy to produce blocks, So some protocol level attacks are very easy to carry out compared to proof of work.
