---
layout: single
title:  "System Design and Scalability"
date:   2017-10-27 08:10:06 -0500
categories: Tech
toc: true
toc_label: "On this page"
toc_icon: "list"
---

> The idea of these questions is to have a discussion about the problem at hand. What’s important for the interviewer is the process, which you use to tackle the problem.

**Remember that there is no one right answer. A system can be built in different ways. The important thing is to be able to justify your ideas.**

System design questions require a combination of the right strategy and knowledge. By strategy we mean a way to approach the problem at an interview.

{:toc}

# Important Links

1. [Harvard Video](https://www.youtube.com/watch?v=-W9F__D3oY4)

2. [Extensive Prep](https://github.com/checkcheckzz/system-design-interview)

3. [Differential Synchronization]( https://neil.fraser.name/writing/sync/)

4. [Scalability for Dummies](http://www.lecloud.net/tagged/scalability)

5. [REST principles](https://ninenines.eu/docs/en/cowboy/2.0/guide/rest_principles/)

6. [HiredInTech](https://www.hiredintech.com/classrooms/system-design/lesson/60)

7. [Database sharding](http://www.25hoursaday.com/weblog/2009/01/16/BuildingScalableDatabasesProsAndConsOfVariousDatabaseShardingSchemes.aspx)

8. [Database Indexing](https://stackoverflow.com/questions/1108/how-does-database-indexing-work)

   ​

# System Design Process
### Constraints and Use Cases

- The very first thing you should do with any system design question is to clarify the system's constraints and to identify what use cases the system needs to satisfy. 
- Usually, part of what the interviewer wants to see is if you can gather the requirements about the problem at hand, and design a solution that covers them well. Never assume things that were not explicitly stated.
- **Constraints consist of either the amount of traffic or the amount of data that our system needs to handle**
- Find the data per second(read and written), and memory required

  > Imagine this is your startup idea and you are designing your system. This way, you would eliminate many assumptions that you would normally make when you try and replicate a well-established system like bit.ly or Google.

### Abstract Design

- Once you've scoped the system you're about to design, you should continue by outlining a high-level abstract design. The goal of this is to outline all the important components that your architecture will need.
- Sketch your main components and the connections between them. If you do this, very quickly you will be able to get feedback if you are moving in the right direction. Of course, you must be able to justify the high-level design that you just drew.
- Don’t get lured to dive deep into some particular aspect of the abstract design. Not yet. Rather, make sure you sketch the important components and the connections between them. Justify your ideas in front of the interviewer and try to address every constraint and use case.
- Usually, this sort of high-level design is a combination of well-known techniques, which people have developed. You have to make sure you are familiar with what's out there and feel comfortable using this knowledge.

### Understanding Bottlenecks

- Most likely your high-level design will have one or more bottlenecks given the constraints of the problem. This is perfectly ok. You are not expected to design a system from the ground up, which immediately handles all the load in the world. It just needs to be scalable, in order for you to be able to improve it using some standard tools and techniques.
- Now that you have your high-level design, start thinking about what bottlenecks it has. Perhaps your system needs a load balancer and many machines behind it to handle the user requests. Or maybe the data is so huge that you need to distribute your database on multiple machines. What are some of the downsides that occur from doing that? Is the database too slow and does it need some in-memory caching?
 - It may be the case that the interviewer wants to direct the discussion in one particular direction. Then, maybe you won’t need to address all the bottlenecks but rather talk in more depth about one particular area. In any case, you need to be able to identify the weak spots in a system and be able to resolve them.
- Remember, usually each solution is a trade-off of some kind. Changing something will worsen something else. However, the important thing is to be able to talk about these trade-offs, and to measure their impact on the system given the constraints and use cases defined.

### Scaling the Abstract Design

- There is a common set of scalability principles that you need to know. Knowing what they are, understanding how they are used, and being able to discuss their pros and cons is what scalability at interviews is all about.







