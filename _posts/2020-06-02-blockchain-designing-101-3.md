---
layout: post
title:  Blockchain Design 101 - Part 3
description: "High level overview of inner working of Cosmos Hub and Ethereum network"
category: articles
tags: [blockchain, block, design, PoW, PoS, ProofOfWork, ProofOfStake, Cosmos, Gaia, Ethereum]
image: "cosmos_hub_ethereum.png"
comments: true
---

This is the third part of blockchain design 101 series. You can read second part [here](/articles/2020/05/23/blockchain-designing-101-2/). In this part we are going to present overview of ethereum and cosmos hub.

---------------------------------

<figure>
  <img src="/public/images/cosmos_hub_ethereum.png" alt="Cosmos hub connected to ethereum via IBC" style="width:100%">
  <figcaption style="text-align: center; font-weight: bold;">Cosmos Hub connecting to Ethereum network via Peg Zone using IBC protocol</figcaption>
</figure> 

## Ethereum Muir Glacier
Ethereum is the second largest Proof-of-Work network behind bitcoin. It’s defining innovation over previous proof-of-work networks is introduction of EVM (Ethereum virtual machine) which runs on every ethereum node deterministically. Combining EVM with proof of work consensus, ethereum network as a whole act as a “World Computer”, where any deterministic immutable computer program compilable to byte code interpretable by EVM can run. Programs can also interact with each other via calling any entrypoint of other programs. Since ethereum byte code is Turing complete, ethereum can run any complex program given enough execution fees. To make state transition operation successful, users need to pay some amount of execution fee in proportion to the complexity of the operation.


Users can submit three types of state transition operations (or in ethereum terminology a transaction) to network:
1. Send some *Ether* to one account to another account or program
2. Call any entrypoint of a program with zero or more parameters
3. Deploy a new program


Ethereum's native currency is called *Ether* and smallest fraction of Ether is called *Wei*. One Ether equals to 10<sup>19</sup> Wei.

### Block construction
In ethereum, algorithm to compute computational puzzle used is *Ethash*. Ethash uses a large dataset that is periodically regenerated, and slowly grows over time, which makes it fairly ASIC resistant. To mine a block, node need to find an eight byte *nonce* which satisfies Ethash's verification conditions, which can be tuned to increase/decrease difficulty. Ethereum tries to keep time required to solve the puzzle in range of 10 to 19 second regardless of continuos change in total resources of the network by adjusting difficulty depending upon time taken to solve the puzzle for previous block. Once node finds solution to the Ethash puzzle, it will prepare a block and broadcast it into the network.

Block contains a set of state transition operations and block header containing nonce, reference to parent block, and optionally reference to siblings of its parent.

Whenever a node constructs a valid block and it becomes part of the canonical fork, node is rewarded:
1. Fixed fee of 2 *Ether* as a reward for constructing a valid block
2. Execution Fee (Or in ethereum terminology Gas) for every state transition operations included in the block

### Fork selection
Ethereum node selects a fork that has maximum Ethash difficulty calculated as a sum of difficulties of all blocks contained. Since Ethash difficulty is dynamically adjusted, it is not always a case that the longest fork is the one with the most difficulties.

### Block Finality
Ethereum offers probabilistic finality as we discussed in the previous part. For almost all use-cases, if seven new blocks are built upon the target block, it is enough to consider that block final.

---------------------------------

## Cosmos Hub v2.0
Cosmos Hub is one of the famous proof of stake network and is called an "Internet of Blockchain". Its strength lies in facilitating interoperability between fully sovereign blockchain by acting as a hub using a protocol called *IBC*. For now, only the top 100 candidates with most stake can become a validator. 

Users can interact with cosmos hub by sending a state transition operation, which will be routed internally to a specific module that handles that operation.

Cosmos Hub's native currency is called *Atom*.

### Block construction
Since cosmos hub is proof of stake blockchain, every validator which has stake in form of *ATOM* is eligible to produce a block. Every consensus round, a validator is chosen as a block proposer based on a weighted round-robin algorithm, where weight is in proportion to that validator's stake. If either proposer is offline or due to any other reason isn't able to broadcast the block in stipulated time, next validator as per round-robin algorithm is chosen as proposer. 

Block contains a set of state transition operations (or in cosmos terminology a transaction) and block header containing reference to parent block and optionally future change to current set of validators.

### Staking
Cosmos Hub requires validator to stake some amount of ATOM as collateral and in return, validator gains the chance to be elected as a proposer as well as have voting power in proportion to ATOM staked. In addition to this, it supports delegated proof of stake which allows users who can not or do not want to run the validator to delegate their funds to one or more validators of their choice and will be compensated with some portion of the revenue of those validators. These users are called delegators.

Validators and delegators earn rewards in two ways:
1. Atom Inflation: New atoms are created every block and distributed to validators and delegators participating in the consensus process. This mechanism exists to incentivize Atom holders to stake them, as non-staked atom will be diluted over time.
2. Execution fees: Every state transition operation submitted to cosmos hub need to include some amount of fee in proportion to complexity of the execution.

Above mentioned rewards are first distributed to individual validators in proportion to their stake in the network. Then for every validator, rewards will be further distributed among delegators of said validators in proportion to their contribution in the validator's total stake.

### Fork Selection
In cosmos hub, only one validator can propose block at a given height and until that proposed block is either finalized or rejected network cannot make further progress. Due to this, there cannot be any fork as long as less than 1/3rd of nodes are faulty.

### Block Finality
To finalize a block, validators with a combined voting power of >66% need to vote for that block. Once a block is finalized, it cannot be reverted unless majority of validators in the blockchain agree to roll back their local states.

---------------------------------

This is final part of the Blockchain Design 101 series. In next series, we will look at advanced blockchain design concepts.
