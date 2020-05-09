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
Generically, Blockchain is a *tree* of block of data linked with each other cryptographically. What this means is every block is built on top of its parent in such a way that changing contents of the parent invalidates child block. This forms core security aspect of blockchain.

Every blockchain implementation is unique, but they share some common concepts.

### State machine
State machine describes how blockchain transition from current state to next state. It requires two inputs: 1) current state 2) state transition operations. For correct operation of blockchain it is essential that state machine is deterministic for every possible input, so that all correct node reaches same state.

### Genesis state
Initial state from which all nodes in the blockchain start is called `Genesis` state. It is typically determined by node operators offline.

### State transition operation
State transition operation is a data blob interpretable by state machine and allows state machine to transition to next state. For blockchain to function correctly, state transition operation needs to be atomic and reversible. 

Two types of state transition operations can exists: 
1) User submitted transition operations: This is typically submitted by user via api exposed by nodes.
2) transition operation generated as part of system operation: Example would be change of validator set in PoS implementation.

### Block
Typically every block except `Genesis` block contains three things: 1) A cryptographic data that links a block to its parent 2) state transition operations 3) Some portion of current state of blockchain.

### Genesis block
Blockchain's tree of block has one root block called `Genesis`, derived from `Genesis` state. `Genesis` block is special in a sense that it does not contain any user submitted state transition operation, but it could still contain operation generated as part of system operation.

### Block construction
Defines which node has right to construct the block, and which state transition operations can be part of that block. In case of some implementation, nodes can produce different blocks from same parent depending upon some conditions. One scenario in which this might happen where due to network partition some nodes on network does not receive the block constructed by current block constructor and are allowed to produce different version of block for same tree height.

### Block finalization Gadget
Refers to how nodes in blockchain determine which block to finalize out of all siblings at particular height of tree. When we say a block is finalized, it means that out of all siblings of blocks, that particular block is considered canonical by majority of nodes and can't be reverted. This is used to assure user that the state transition operation submitted by operation is now final, and won't be reverted in future.

### Fork selection
Refers to how nodes in blockchain determine canonical fork from the tree of blocks. Here fork is defined as path from root node to one of the leaf node. Canonical fork must contain all finalized block.

--------

In next part we will discuss different blockchain design and how they evolved.
