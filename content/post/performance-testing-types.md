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

Performance testing is one of the most important and common types of quality testing because performance is not a well-defined functional requirement, and exactly where is the beginning of the debate. So it is crucial to have a concise testing plan to design and set up a beneficial performance testing solution.

#### What type of performance testing do I need?
It depends on your performance requirement.

If you google the topic you will find some articles with the exact title, but I could not find a clear and practical one so decided to write one! Long story short, among the conventional types of performance testing, the first two items are the most common:

1. Load test
2. Stress test
3. Spike test
4. Volume test
5. Scalability test

## What is the Designed Load?

To plunge into the differences, it is important to be aware of the concept of __Load__.

#### Load is the number of __services__ that the system under test is providing in the unit of time. 

The definition of service depends on your system functionality: 

- For a transactional banking solution: The service is the transaction and the unit of measure for the load of the system will be __transaction per second__ (known as _TPS_).
- For an instant messaging system like telegram, service can be considered as the number of concurrent users having a persistent TLS socket connecting to the server.

So the __designed load__ is understandable now.

#### The load that is applicable for the system working acceptable, with a well-defined environment including network, hardware, and operating system configuration, is called the __designed load__.

### Load Test

#### Load test is testing the system under the designed load.

So if you want to verify the system's performance in the presumed situation, this is the road to go. In load testing, the focus is usually on the performance measures like latency or response time.

The load pattern in a load test is something like the graph below illustrated for a considered system with a designed load of `100 TPS`:
![chart](1.png)
#### What does the load test report contain?
As mentioned before, a load test is performed under the designed load to focus on the requirements the system is designed to provide in the normal situation. In most cases, in performance-critical systems, __latency__ is the main performance measure. For our considered system, the recorded latencies during the load test are like below:
![chart](2.png)
Usually, the latency distribution is like a Gaussian distribution function and we are wary of the last buckets.

It is also convenient to summerize a load testing report to some percentile values.
> #### Note!
> In statistics, a __percentile__ is a score below which a given percentage of scores in its frequency distribution falls. For example, the 50th percentile (the median) is the score below which 50% of the scores in the distribution may be found. `From Wikipedia`

![chart](3.png)
So according to the chart, we can simply say the system's 99th latency percentile is 300 milliseconds. Be careful about this kind of summarization, it could be confusing and distorting the performance testing results. Gil Tene has an awesome talk calling it __percent-lie__! Highly recommended.

### Stress Test
#### Stress test is testing the system beyond the designed load.

Stress testing's goal is assessing the system's performance measures beyond the normal situation, especially the capacity load of the system or the system's crash point. With a functioning stress test plan, the development team could enhance the capacity of the system on each iteration based on the results. The load pattern of a stress test of the considered system is illustrated in the next chart.

![chart](4.png)

#### What does the stress test report contain?
Although we can report the latency distribution in stress test but note that if the system is failed or crashed, then the latency results are pointless. So a good report of a stress test must contain some information about the __reliability and availability__ of the system in the increasing stages of the generated load. Our considered system's stress test result is like this chart.

![chart](5.png)

It is beneficial to have a performance acceptance criterion to determine if the system passed a specific stage of stress or not. The considered systems acceptance criterion is `Success Rate = 80%` so it has passed the test until the second stage with `200 TPS` and failed in the next stages.

## Spike Test

A Spike test is testing a system's behavior when it is exposed to a spike of load.

I am not so much experienced in this type of performance testing but it seems that the main challenge in this type of test is defining the load pattern and the behavior measurement to be concise and repeatable.
![chart](6.png)

## Endurance Test

The endurance test is testing a system's behavior under a defined load for a long period of time.

![chart](7.png)

## Conclusion

It is challenging to design and represent the performance requirements of the system, especially while the test plan totally depends on it. But if you involve developing a performance-critical solution, do not hesitate to set up a performance testing solution. Although there are lots of tools, frameworks, and technical details, it is always inspiring to start with a sketch test plan and a simple tool like k6. Then criticize your solution and debate it with your teammates, you will end up with a precise, powerful, and valuable solution by the magic of continuous improvement.

#### Final Note!

There are more performance testing types like Microbenchmark that are not in the scope of this article focusing on the most common types. I hope I could study, learn, and share more.

### References and Beneficial Links

It is not a scientific article so excuse me for not respecting conventional referencing formats. Here are some links I have used and I recommend you to check them out:

1. [Gil Tene's awesome talk: How not to measure latency?](https://youtu.be/lJ8ydIuPFeU)
2. [A good book: The art of application performance testing](https://www.oreilly.com/library/view/the-art-of/9781491900536/)
3. [K6: a performance testing tool](https://k6.io/)