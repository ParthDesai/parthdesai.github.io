---
layout: post
title:  Blockchain designing 101 for developers - Part 1
description: ""
category: articles
tags: [blockchain, tendermint, ethereum, BFT]
comments: true
---

It is the first part of blockchain designing 101 for developers. We will talk about what you need to 
consider when designing your blockchain and trade-offs for certain decisions. I am assuming that readers are 
already familiar with basic blockchain concepts and looking to gain more knowledge on how does inside of blockchain work.

-------

## What is blockchain?
Generically, Blockchain is *tree* of block of data linked with each other cryptographically. What this means is every block is built on top of its parent in such a way that changing contents of the parent invalidates child block. This forms core security aspect of blockchain.

Every blockchain technology is unique, but they share some common concepts.

### Genesis block
Every blockchain's tree of block has one root block called `Genesis`, typically determined by collaboration between node operators.

### Consensus algorithm
Consensus algorithm is heart of blockchain. It's responsibility is to make sure network can continuously make progress and majority of nodes are in agreement regarding state of the blockchain. At higher level, it is responsible for below three tasks.

#### Block production
Refers to how nodes in blockchain produce child block from parent block. In case of some consensus algorithm, nodes can produce different blocks from same parent depending upon some conditions for example network partition. Which is the reason we described blockchain as *tree* instead of *linked list*.  

#### Block finalization
Refers to how nodes in blockchain determine which block to finalize out of all siblings at particular height of tree. When we say a block is finalized, it means that out of all siblings of blocks, that particular block is considered canonical by majority of nodes and typically can't be reverted. 

#### Fork selection
Refers to how nodes in blockchain determine canonical fork from the tree of blocks. Here fork is defined as path from root node to one of the leaf node. Canonical fork must contain all finalized block.

Depending upon consensus algorithm, either above three task are handled separately or handled in tightly coupled manner.

### Local state
In some blockchain design, Every node in network needs to maintain some data about current state of blockchain, for example auxiliary state of data contained in blocks, consensus algorithm configuration etc. This state is used by block production algorithm along side parent block to derive child block.

## Notable consensus algorithms:

### Proof of Work

### Proof of Stake

### Delegated Proof of Stake

--------

In next part we will discuss how above consensus algorithms work and why they were invented.
