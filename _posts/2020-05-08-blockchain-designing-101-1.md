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
already familiar with basic blockchain concepts and looking to contribute to one or more blockchain platforms out there.

## What is blockchain?
Generically, Blockchain is *tree* of block of data linked with each other cryptographically. What this means is every block is built on top of its parent in such a way that changing contents of the parent invalidates child block. This forms core security aspect of blockchain. We will also expand on why it is *tree* and not *Linked list* as one might think intuitively. 

Every blockchain technology is unique, but they share some common concepts.

## Genesis block
Every blockchain's tree of block has one root block called `Genesis`, typically determined by collaboration between node operators.

## Block production algorithm
Distributed algorithm employed by nodes in blockchain to produce child block from parent block. In case of some block production algorithm, nodes can produce different blocks from same parent depending upon some conditions for example network partition. Which is the reason we described blockchain as *tree* instead of *linked list*.  

## Block finalization algorithm
Algorithm employed by nodes in blockchain to determine which block to finalize out of all siblings at particular height of tree. When we say a block is finalized, it means that out of all siblings of blocks, that particular block is considered canonical by majority of nodes and typically can't be reverted. 

## Fork selection algorithm
Algorithm employed by nodes in blockchain to determine canonical fork from the tree of blocks. Here fork is defined as path from root node to one of the leaf node. Canonical fork must contain all finalized block.




-----

Usually, first block is called `genesis` block, typically determined by collaboration between node operators, and subsequent blocks are built on top of previous block using block production algorithm employed by particular blockchain technology. And depending upon block finalization algorithm employed, a single fork is chosen to be finalized. 




