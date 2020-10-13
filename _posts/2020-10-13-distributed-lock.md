---
layout: post
title: Distributed Lock
subtitle: A simple best-effort distributed lock using "fence token" and leasing expiration
bigimg: /img/fence.jpg
share-img: /img/fence.jpg
tags: [architecture, distributedsystem, dotnet, redis, mongodb]
---

A common issue in distributed system is having multiple consumers hosted in different nodes competing for the same resources. In the example bellow a producer creates files in a file share and multiple consumers compete to for those files to parse and persist the data.

![](/img/distributed-lock-redis.svg.png)

## 🔒 Best-effort

A simple approach to implement a reliable lock is by best-effort, **set-if-not-exists**. By best-effort it means that the lock has no guarantee that it will always work, mainly because of network issues or in cases the node that requested the lock crashes without finishing it work and releasing it.

>The locks are approximate and may fail occasionally

## 🔑 Fence Token

The implementation of a fence token by correctness would involve using a consensus system with an incremental key. For this implementation, the fence token is not as reliable as what a good consesus system implements, it is a unique token to prevent a node releasing a resource locked by another node. Basically, **delete-if-exists-and-token-matches**.

## ⏲️ Leasing Expiration

For the reasons I pointed before, the implementation by best-effort can't guarantee that the lock will be released by a node if it suddenly crashes or a network problem happens when the node tries to unlock, resulting in a deadlock. Putting an expiration will allow the lock release automatically by redis cleaning up the string after certain time.

## 👉 Conclusion

Use it carefully, keep in mind that this is a best-effort implementation. I recomend reading Martin Kleppmann's blog below, also his book, mainly chapter 8 and 9, which cover in depth distributed concerns. Another thing, don't use Red-Lock :P, It may fail you badly.

I've implemented an example in C# with .Net and Docker, you can scale the consumers and play with the code to make it fail, it will 😁. The producer do not require locks in the sample code, only consumers.

The source code is hosted on GitHub: <a href="https://github.com/fals/distributed-lock" target="_blank">https://github.com/fals/distributed-lock</a>

## 📖 Reference

* <a href="https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321/ref=sr_1_1?ie=UTF8&qid=1537824366&sr=8-1&keywords=designing+data-intensive+applications" target="_blank">Designing Data Intensive Applications</a>

* <a href="http://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html" target="_blank">How to do distributed locking
</a>