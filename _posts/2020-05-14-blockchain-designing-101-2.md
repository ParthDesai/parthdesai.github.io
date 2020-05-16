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
In Proof of work blockchain, To construct a valid block node need to find an answer to computational puzzle. This puzzle need to be such that finding answer require node to put some effort in terms of resource usage (for example memory, cpu or network) but still feasible enough and verifying if that answer is correct need to be quick and easy. Effort required to calculate the solution can be quantified in terms of some unit of difficulty. 

### Fork selection
A fork having most difficulty as sum of difficulties of all blocks contained can be seen as a fork chosen to extend by a set of nodes with the largest cumulative resources. So, a node is incentivized to select that fork to append new block, due to high probability of said block remaining canonical.

### Block finality
Pure proof of work blockchain offers probabilistic finality, because there is always some probability however small, that current best fork can be overtaken by some other fork by producing more work. This probability is inversely proportional to difference in difficulty between current best fork and that other fork. So, users need to wait for large enough difference in difficulty between block's fork and other forks, before considering said block final for all practical purposes. 
-----
So, if users want to know if for all practical purpose block is finalized, they need to wait for the chain containing that block to extend such that above probability becomes miniscule. So, Users need to wait for the chain containing that block to extend depending upon finality assurance required.

So, Users need to wait for chain to extend by number of blocks proportional to finality assurance required.
-----


## Proof-of-Stake
In proof of stake blockchain, To be able to validate and produce blocks, nodes need to hold some amount of stake in the blockchain. In this blockchain, probability of block production is proportional to amount of stake a node holds.

### Block construction

### Fork selection

### Block finality


## Proof-of-Authority
In Proof of authority blockchain, node operators need to advertise their real world identity which means node operators are incentivized to act honestly since their reputation is at stake.