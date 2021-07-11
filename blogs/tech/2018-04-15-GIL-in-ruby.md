---
title:  "Digest: GIL in Ruby"
description: "Digest about GIL in Ruby"
date: 2018-04-15 18:00:00
categories: [Tech]
tags: [Digest]
---

# Digest: GIL in Ruby

> * Original Article：[Parallelism is a Myth in Ruby](https://www.igvita.com/2008/11/13/concurrency-is-a-myth-in-ruby/)
> * Original Article：[Nobody understands the GIL](https://www.jstorimer.com/blogs/workingwithcode/8085491-nobody-understands-the-gil)
> * Original Article：[Actor-based Concurrency](http://berb.github.io/diploma-thesis/original/054_actors.html#02)
> * Original Article：[Concurrency Models](http://tutorials.jenkov.com/java-concurrency/concurrency-models.html#functional-parallelism)
> * Original Article：[non-blocking algorithms](http://tutorials.jenkov.com/java-concurrency/non-blocking-algorithms.html)
> * Author: [Damon Yuan](https://www.damonyuan.com)
> * Date: 2018-04-15

## 1. Parallel Workers

  * ### Advantages

  * ### Disadvantages

    -  shared states

       * Problems

         - race conditions
         - deadlock

       * Solutions:

         - non-blocking concurrency algorithm
         - persistent data structure
         - stateless

    - job order is non-deterministic

## 2. Assembly line

  Non-blocking IO operation

  - Actors: mailbox and addresses
  - Channels: subscriptions

## 3. Functional Parallelism

  When each function call can be executed independently, each function call can be executed on separate CPUs. That means, that an algorithm implemented functionally can be executed in parallel, on multiple CPUs.
