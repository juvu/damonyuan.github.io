---
title:  "Shards, Replicas and Nodes"
description: "How to ensure the availability"
date: 2020-07-21 15:04:23
hidden: false
categories: [Tech]
tags: [Shards, Replicas, Nodes]
---

# Shards, Replicas and Nodes

> * Author: [Damon Yuan](https://www.damonyuan.com)
> * Date: 2020-07-21

Say you have a elasticsearch cluster and you want to ensure the highest availability with minimum replicas and shards with fixed node number, how is the relationship between them?

  - nodes -> x
  - replicas -> y
  - shards -> z
  
If we want to ensure the availability when one of the nodes is down, where min(x) = 2 , then min(y) = 2 and min(z) = 1.

    |--- node 1 ---|--- node 2 ---|
    |--------------|--------------|
    |-- replica 1--|-- replica 2--|
    
If we want to ensure the availability when two of the nodes are down, where min(x) = 3, then min(y) = 3 and min(z) = 1. 
    