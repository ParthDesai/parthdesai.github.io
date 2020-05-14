---
layout: post
title:  Blockchain Design 101 - Part 2
description: "Describes different blockchain designs like Proof-of-Work, Proof-of-Stake, Delegated-Proof-of-Stake and how they evolved."
category: articles
tags: [blockchain, block, design, PoA, PoS, DPoS]
image: ""
comments: true
---

This is the first part of blockchain design 101 series. You can read first part [here](/articles/2020/05/08/blockchain-designing-101-1/). In this part, we are going to talk about some different blockchain designs and how they evolved.

## Proof-of-Work

### Block construction
In Proof of work blockchain, To construct a valid block node need to find an answer to computational puzzle. This puzzle need to be such that finding answer need to be moderately expensive in terms of resource usage (for example memory, cpu or network) but still feasible enough and verifying if that answer is correct need to be quick and easy.

### Fork selection
To produce a valid block node require to put some effort. A fork having most effort as sum of effort of all blocks contained represents that set of nodes with combined largest resources have chosen that fork as best fork. 

### Block finality
Pure proof of work blockchain offers probabilistic finality, because there is always some probability however small, that current longest fork can be overtaken by some other fork. This probability depends upon computational puzzle chosen and is inversely proportional to difference in length between longest fork and that other fork. So, Users need to wait for chain to extend by number of blocks proportional to finality assurance required.
-----
So, if users want to know if for all practical purpose block is finalized, they need to wait for the chain containing that block to extend such that above probability becomes miniscule. So, Users need to wait for the chain containing that block to extend depending upon finality assurance required.
-----


## Proof-of-Authority

## Proof-of-Stake

## Delegated-Proof-of-Stake