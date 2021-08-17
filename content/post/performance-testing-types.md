+++
author = "Kiarash Azarnia"
title = "Types of Performance Testing"
date = "2021-06-04"
description = "Explanation of different types of performance testing."
tags = [
    "performance-testing", 
    "stress-test", 
    "load-test",
]
categories = [
    "software",
]
series = ["performance-testing-types"]
aliases = ["article"]
+++



This article offers a practical explanation of the concepts of the performance testing types.
<!--more-->

## Introduction

Performance testing is one of the most important and common types of non-functional software testing. As you know, performance is a quality attribute and does not have a well-defined scenario and acceptance criteria like the usual functional requirements, and exactly that is the root of the challenge. So it is critical to have a concise understanding of the different performance testing approaches to design and set up a beneficial performance testing solution.

If you google the topic, you will find some articles with the same title, but I could not find one being simple and rigorous at the same time, so I decided to write one. Long story short, among the conventional types of performance testing, the first two are the most common:

1. Load test
2. Stress test
3. Spike test
4. Endurance test

## What is the Designed Load?

To plunge into the differences, it is important to understand the concept of __Load__.

> Load is the number of services that the system under test (SUT) is providing in the unit of time.

The definition of service depends on the system's functionality: 

- For a transactional banking solution: The service is the transaction and the unit of measure for the load of the system will be __transactions per second__ (known as `TPS`).
- For an instant messaging system like telegram, service can be considered as the number of concurrent users having a persistent TLS socket connecting to the server. Another approach is to focus on the number of messages in the unit of time to define the load of the system. Different scenarios require different definitions for the load.

So the designed load is understandable now.

> The load under which the system should work acceptably, in a well-defined environment including network, hardware, and operating system configuration, is called the designed load.

### Load Test

> Load test is testing the system's behavior in the normal situation so that the applied load is under or equal to the designed load.

So if you want to verify the system's performance in the presumed situation, this is the way to go. In load testing, the focus is usually on the performance measures like latency or response time.

The load pattern in a load test is something like the graph below illustrated for a considered system with a designed load of `100 TPS`:
![chart](1.png)
#### What does the load test report contain?
As mentioned before, a load test is performed under the designed load to focus on the requirements the system is designed to provide in the normal situation. In most cases, in performance-critical systems, __latency__ is the main performance measure. For our considered system, the recorded latencies during the load test are like below:
![chart](2.png)
Usually, the latency distribution is like a Gaussian distribution function and we are wary of the last buckets.

It is also convenient to summerize a load testing report to some percentile values.
> #### Note!
> __Percentile__ is a score below which a given percentage of scores in its frequency distribution falls. For example, the 50th percentile (the median) is the score below which 50% of the scores in the distribution may be found. _From Wikipedia_

![chart](3.png)
So according to the above chart, we can simply say that the system’s 99th latency percentile is 300 milliseconds. Be careful about this kind of summarization, it could be confusing and distorting for the performance testing results. Gil Tene has an awesome talk titled _How Not to Measure Latency_ calling it __percent-lie__!

### Stress Test
> Stress test is testing the system beyond the designed load.

Stress testing’s goal is assessing the system’s performance measures beyond the normal situation. Metrics like the capacity load of the system or the system’s crash point could be evaluated in this approach. Utilizing a good stress test plan, the development team could enhance the capacity of the system in each iteration based on the results. The load pattern of a stress test of our considered system is illustrated in the next chart.

![chart](4.png)

#### What does the stress test report contain?
Although we can report the latency distribution in the stress test, if the system is failed or crashed, then the latency results are meaningless. So a good report for a stress test must contain some information about the __reliability__ of the system in the increasing stages of the generated load. For example, we can evaluate the Error Rate of the requests as a reliability indicator. Our considered system’s stress test result is like this chart.

![chart](5.png)

It is beneficial to have a performance acceptance criterion to determine if the system passed a specific stage of stress or not. The considered system's acceptance criterion is `Success Rate = 80%` so it has passed the test until the second stage with `200 TPS` and failed in the next stages.

## Spike Test

A Spike test is testing a system's behavior when it is exposed to a spike of load.

![chart](6.png)

## Endurance Test

The endurance test tests a system’s behavior under a defined load for a long time period.

![chart](7.png)

## Conclusion

It is challenging to evaluate and represent the system's performance requirements, especially while the test plan totally depends on it. But if you involve developing performance-critical software, do not hesitate to set up a performance testing solution. Although there are lots of tools, frameworks, and technical details, it is always inspiring to start with a sketch test plan and a simple tool like k6. Then criticize your solution and debate it with your teammates, you will end up with a powerful and valuable solution by the magic of continuous improvement.

#### Final Note!

There are more performance testing types like Microbenchmarking, Volume Testing, Scalability Testing, Capacity Testing, and so on which some of them are not in the scope of this article focusing on the most common types and some of them are other representations of the explained ones. Like peak testing that is another name for spike testing. I think the most of literature about performance testing is developed in the software industry by developers and not by computer scientists in an academic fashion and that's why there are some inconsistencies in the field.

### References and Beneficial Links

This is not an academic article so excuse me for not respecting conventional referencing formats. Here are some links I have used and found informative.

1. [Gil Tene's awesome talk: How not to measure latency?](https://youtu.be/lJ8ydIuPFeU)
2. [A good book: The art of application performance testing](https://www.oreilly.com/library/view/the-art-of/9781491900536/)
3. [K6: a performance testing tool](https://k6.io/)
4. [Test automation in devops: An informative course](https://testautomationu.applitools.com/test-automation-in-devops/)
5. [A Survey on Load Testing of Large-Scale Software Systems](https://www.researchgate.net/publication/282551435_A_Survey_on_Load_Testing_of_Large-Scale_Software_Systems)
