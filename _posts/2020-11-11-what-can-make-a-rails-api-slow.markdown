---
layout: post
title:  "What can make an Rails API slow"
date:   2020-11-11 07:24:24 +0700
tag: [Ruby, System Performance]
---

If you have been a web developer for more than two or three years, you may experience several performance issues in your web applications. Specifically, users complain that a page takes ages to show up or some features suddenly stop working because the infrastructure runs out of resources. Some fun facts I find regarding performance issues as follows:
- Some existing performance issues suddenly become urgent because of who reports the issues
- Performance issues can originate from anywhere, usually the areas of the system which can be considered as the unknown unknowns to us. We tend to blame unrelated things and follow the wrong directions
- Performance issues may be caused by complex user behavior in production environment combined with several issues which we think minor when analyzed in isolation
- Some performance issues cannot be fixed other than rewriting a certain module, due to architectural decisions made earlier
I am going to summarize several common causes of performance issues I encounter over the course working as a Ruby on Rails developer for five years.

## I/O activities
<img src="/assets/images/io-speed.png" alt="io-speed" width="600">

[Jeffrey Dean](https://research.google/people/jeff/), a Google researcher, showed the above slide in a lecture, [Software Engineering Advice from Building Large-Scale Distributed Systems](https://research.google.com/people/jeff/stanford-295-talk.pdf). In comparison with main memory reference, disk seeking and network communication (I/O activities) are much slower. Some I/O activities a RoR developer usually encounters:
- SQL queries
- HTTP or GRPC calls to external services
- Reading and writing files

## Database sequential scans

<img src="/assets/images/customer-table.png" alt="customer-table" width="850">
```SQL
SELECT FROM WHERE
CUS_NAME, CUS_STATE CUSTOMER
CUS_STATE = 'FL';
```
(Source: [Database Systems: Design, Implementation, and Management](https://www.amazon.com/Database-Systems-Implementation-Management-Information/dp/0538469684))

With no advance preparation, the system would have to scan the entire table, row by row, to find all matching entries. Use index for query optimization as follows:

<img src="/assets/images/customer-table-with-index.png" alt="customer-table-with-index" width="1000">

(Source: [Database Systems: Design, Implementation, and Management](https://www.amazon.com/Database-Systems-Implementation-Management-Information/dp/0538469684))

Some knowledge regarding database index I think a RoR developer should know:
- B-Tree index
- Unique index
- GIN index
- Multicolumn index
- [Unused indexes](https://www.cybertec-postgresql.com/en/get-rid-of-your-unused-indexes/)
- [Using EXPLAIN](https://www.postgresql.org/docs/9.6/using-explain.html)

I assume that you are using Postgres. You can find alternatives in other database systems, I believe.

## Database Locks
Database systems provide a technique called transactions, to prevent data integrity problems. We usually use transactions when we want all independent updates to databases caused by a unit of work either all successful or not affecting the database at all. However, transactions are double-edged swords. Managing concurrent transactions requires locks, affecting database performance. Even worse, locks can become deadlocks, causing application bugs.

## Pause times caused by Garbage Collection (GC)
If you used to develop applications using C or C++, you absolutely understand why GC was born. C/C++ requires developers to manage memory by themselves. That means each time you create an object, you have to free its memory explicitly once the object is done with. To make application development less complicated, some languages like Ruby use automatic memory management where an asynchronous garbage collection process free objects if eligible.

Ruby applications are paused while GC executes causing occasional application responses with high latency. The more memory your code consumes, the more GC works, and the slower your applications will be. I borrow a figure from a Heroku blog to show you how GC affects Ruby application performance.

<img src="/assets/images/ruby-gc.png" alt="ruby-gc" width="1000">

(Source: [Incremental Garbage Collection in Ruby 2.2](https://blog.heroku.com/incremental-gc))

Mark and Sweep is where GC works, pausing Ruby apps.

## Application server performance
In order to deploy a Rails app, we need an application server which is usually Unicorn or Puma. Understanding the application server architecture is important when it comes to optimize the performance of the Rails app. Let’s take a look at [Puma](https://github.com/puma/puma)

<img src="/assets/images/puma.png" alt="puma" width="500">

Each request is served in a separate thread. In other words, if we have five threads, we can serve five requests concurrently. However, concurrent is not necessarily parallel. If you are using MRI Ruby, there is a Global VM Lock (GVL) that ensures only one thread can run Ruby code at a time. While one thread holds the lock, other threads need to wait for their turn to acquire the lock. Read [Built For Speed & Concurrency](https://github.com/puma/puma#built-for-speed--concurrency) and [Thread Pool](https://github.com/puma/puma#thread-pool) for more details.

What is more, threads in the same process share memory address space and garbage collection. That means if one uses up memory, other requests suffer from slow performance.

# References

- [Systems Performance: Enterprise and the Cloud](https://www.amazon.com/Systems-Performance-Enterprise-Brendan-Gregg/dp/0133390098)
- [Ruby Performance Optimization](https://pragprog.com/titles/adrpo/ruby-performance-optimization/)
- [Working with Ruby Threads](https://www.goodreads.com/book/show/17826435-working-with-ruby-threads)
