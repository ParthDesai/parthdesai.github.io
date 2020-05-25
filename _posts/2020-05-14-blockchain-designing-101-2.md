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

Proof of work blockchain gets its name on the fact that node requires to do some work, in order to produce a block.

### Block construction

In Proof of work blockchain, To construct a valid block node need to find an answer to a computational puzzle. This puzzle needs to be such that finding answer requires a node to put some finite and quantifiable effort in terms of resource usage (for example memory, cpu or network), but verifying correctness of that answer need to be quick and easy so that other nodes can verify the answer. So, more resources a node has, more probability of its producing the block. Effort required to calculate the solution can be quantified in terms of amount of resources utilized and can be expressed in units of difficulty.

### Fork selection

A fork having most difficulty as sum of difficulties of all blocks contained can be seen as a fork chosen to extend by a set of nodes with the largest cumulative resources. So, a node is incentivized to select that fork to append new block, due to high probability of said block remaining canonical. Node is also discouraged to extend multiple forks due to significant block production cost associated.

### Block finality

Pure proof of work blockchain offer probabilistic finality. There is always some probability however small, that block can become non-canonical once another fork at less height overtakes that block's fork by increasing its own difficulty quicker. Probability of that happening is inversely proportion to amount of difficulty added on top of said block, as more difficulties added on top less chance for a fork created at height less than block to overtake said block's fork.

### Caveats

In proof of work blockchain every node need to do some effort while competing to produce the block, which is very costly in terms of energy usage. Since solving computational puzzle takes some time, block generation in Proof of work is slow by design.

## Proof-of-Stake

Proof of stake differs with Proof of work by shifting the requirement of block production for node to holding a stake in blockchain as opposed to working on finding solution to puzzle. This speeds up block generation considerably.

### Block construction

In proof of stake blockchain nodes which have locked up some stake in blockchain can only produce block and make an assertion. Those nodes are called validators. More stake validator has more chance it has to produce the block and more weight to its assertions. This stake acts as a collateral and incentivize the validator to act non-byzantine. Validating a block require validators with combined majority stake to assert that said block is valid.

### Block finality

Proof of stake blockchain offers either absolute finality or probabilistic finality. Probabilistic finality works same as Proof-of-Work blockchain.

In case of absolute finality support, multiple strategies exists:

1. Before finalizing previous block, next block cannot be constructed. In this case forks are not allowed, as it is not possible for any siblings of block to exists.

2. A distributed algorithm finalizing blocks depending upon certain parameters like block age, combined stake of validators asserted validity of that block, number of blocks built upon that block etc.

### Fork selection

Fork selection in Proof of stake system is completely implementation dependent. Protocol level mechanism is required to discourage validators to produce conflicting blocks.

### Caveats

Since in proof of stake blockchain there isn't any physical anchoring of blockchain as opposed to proof of work where you have to spend real world energy to produce blocks, there need to be protocol level measures to discourage validators to produce multiple conflicting blocks.
