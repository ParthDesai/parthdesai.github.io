---
layout: post
title:  Blockchain Design 101 - Part 1
description: "Describes some common blockchain concepts like state machine, state transition operators, block construction and block finalization."
category: articles
tags: [blockchain, block, design, BFT, consensus]
image: "blockchain-example.png"
comments: true
---

This is the first part of blockchain design 101 series. Aim of this blog series is to describe in detail what goes under the hood of blockchain. In this part, We are going to talk about some common blockchain concepts.

-------

## What is blockchain?
Generically, Blockchain is a *tree* of block of data linked with each other cryptographically. What this means is every block is built on top of its parent in such a way that changing contents of the parent invalidates child block. This forms core security aspect of blockchain.

<img src="/public/images/blockchain-example.png" alt="Sample blockchain" style="width:800px;"/>

Every blockchain implementation is unique, but they share some common concepts.

### State machine
State machine describes how blockchain transitions from current state to next state. It requires two inputs:
1. Current state 
2. State transition operation

For correct operation of blockchain, state machine must be deterministic for every possible input. So that all correct node reaches same state, upon consuming same input.

### Genesis state
Initial state from which all nodes in the blockchain start is called genesis state. It is typically determined by node operators offline.

### State transition operation
State transition operation is a data blob interpretable by state machine. Given current state, successful interpretation produces a changeset, which is then applied by state machine to current state to produce next state. For blockchain to function correctly, state transition operation needs to be atomic and reversible. 

Two types of state transition operations exists: 
1. User submitted: Typically submitted by user via api exposed by nodes.
2. System generated: Generated as part of system operation. One example would be enacting a new validator set in Proof-of-Stake blockchain.

### Block
Every block except genesis block contains three things: 
1. A cryptographic data that links a block to its parent 
2. Zero or more state transition operations 
3. Some portion of current state of blockchain.

### Genesis block
Blockchain's tree of block has one root block called genesis block, derived from genesis state. In most blockchain implementations, Genesis block is not allowed to contain any user submitted state transition operation, but system generated state transition operation can still be part of it.

### Block construction
Defines which node has the right to construct the block, and which state transition operations can be part of that block. In case of some implementation, nodes can produce different blocks from same parent depending upon some conditions. One scenario in which this might happen where due to network partition some nodes on network does not receive the block constructed by current block constructor and are allowed to produce a different version of block for same tree height.

### Block finalization
Refers to how nodes in blockchain determine which block to finalize out of all siblings at a particular height of tree. When we say a block is finalized, it means that out of all siblings of blocks, that particular block is considered as confirmed and depending upon actual implementation it is either impossible or only possible with significant effort to revert changeset produced by interpretation of said block.

### Fork selection
Refers to how nodes in blockchain determine canonical fork from the tree of blocks. Here fork is defined as a path from root node to one of the leaf node. Canonical fork must contain all finalized block.

--------

In the next part we will discuss different blockchain designs and how they evolved.
