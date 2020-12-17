---
layout: page
title: Performance Counter Enhanced User-Centric Scheduling for Heterogeneous Cores
description: Using CPU performance counters to make intelligent scheduling decisions for asymetric cores, optimizing for multiple utility-based (user-centric) models
---

<!-- List of collaborators -->
<h4>Collaborators</h4>
<ul>
    <li><a href="https://people.cs.pitt.edu/~mosse/">Daniel Mossé</a></li>
    <li>Nathan Ackerman</li>
</ul>

<!-- Overview of the project -->
<h4>Overview</h4>
<p>
This work combines research in two disciplines, namely heterogeneous core scheduling and user-centric scheduling, both for the sake of energy reduction. The project is a modified version of the Linux kernel with changes made to the CFS scheduler and frequency governing. It is well known that certain tasks have varying performance across asymetric cores. This project seeks to use CPU performance counters to enhance the scheduling decisions using models that are optimized for a user-centric view of the computation needed. The user-centric spin is that background applications are optimized for EDP, while foreground applications are optimized for ED<sup>2</sup>P.
<br><br>
</p>


<!-- asym core sched -->
<h4>Asymetric Core Scheduling</h4>
<p>
The board this project is built for is an Odroid XU4. The board is an ARM big.LITTLE system with two types of core clusters. The small cluster cores are Cortex A7 and the big cluster cores are Cortex A15. To address why these must be treated differently, we must address the differences between them. The small cores are in order execution. They are designed to run at a lower range of frequencies in a more energy-efficient manner, but not for very high throughput performance. The big cores are out-of-order execution and are designed for throuput performance, but not to be very energy-efficient.
<br>
</p>

<p>
There are certain aspects of tasks that make them more efficient to run on one core or another. For example, an IO or Memory-bound task will not benefit from a big core as it spends most of its time in stalled cycles anyways, so it would not benefit form a faster core. On the other hand, CPU-bound tasks can benefit from the big core as it allows the work to be finished sooner, allowing other parts of the system to be turned off or moved into low-power states. Many of these behaviors are recognizable from CPU performance counters (IPC, Cache Misses, Bus Communications). 
<br>
</p>

<p>
The kernel has been modified to track CPU performance counters and use them in models that predict the best core to run on. These counters are tracked for each process seperately at the granularity of each context switch. The scheduler mappings have been created via empirical data collected from many different types of application behavior. Microbenchmarks were run offline with their performance counter and power information collected. This was done in user space using the perf tool and measuring the power from Smartpower 2 device with firmware modified to give power readings at a 1ms granularity.
<br>
</p>


<p>
These microbenchmarks were run on every core at every possible frequency for each cluster. Offline, this data was analyzed and a decision tree model was built to map counter values being seen to the best core to run on (depending on different metrics). The EDP and ED<sup>2</sup>P was calculated for each benchmark and the runs with optimal EDP or ED<sup>2</sup>P were added to lists of mappings that map counter values to a cluster/frequency pair. It is important to note that the CPU Scheduler in this project also takes the responsibility of the CPU Frequency Governor.
<br>
</p>


<p>
Decision trees were chosen because they offer good prediction (~97%) and are very quick models. Any model used in scheduling decisions must be able to run in the order of microseconds. They also have a small memory footprint. To put these into the model, a code generation routine is run in the sci-kit learn objects to create the if/elses and ranges of values that make the decisions. This code is then added into the kernel and run when a program comes off of the CPU (but not if it was just relocated recently). Below is the workflow diagram for more details on how the scheduler mappings are created. Click to view in another page.
<br><br>
</p>



<div class="img_row">
    <img class="col one left" src="/assets/img/sched_map_diagram.jpg" alt="" title="Derivation of Scheduler Mappings" onclick="window.open('/assets/img/sched_map_diagram.jpg', '_blank');"/>
</div>


<p>
You may notice in this diagram a path labeled B. This is for an alternate model that instead predicts the power at which a core would run given performance counter information. This is meant for a future iteration of this type of scheduler that does prediction of application phases.
<br><br>
</p>



<!-- user-centric -->
<h4>The User-Centric Nature</h4>
<p>
There are two models used in the scheduling, optimizing for different metrics. The first one is EDP. This is used for background tasks where we want to run them in an energy-efficient manner. In this case, we do not care to much about the delay, other than the fact that that means keeping system components on longer. On the other hand, foreground tasks have more immediate needs for computation as these give direct utility to the user and increase interactivity. For these tasks, we use the ED<sup>2</sup>P model as it increases the weight of the delay, meaning we only make a tradeoff that increases delay by a small amount if we receive a much larger energy gain.
<br><br>
</p>


<h4>The Kernel Architecture</h4>
<p>Click to view in another page.</p>
<div class="img_row">
    <img class="col one left" src="/assets/img/kernel_diagram.jpg" alt="" title="Kernel Architecture" onclick="window.open('/assets/img/kernel_diagram.jpg', '_blank');"/>
</div>

<!-- Where is it currently? -->
<h4>Current State</h4>
<p>
Currently, the scheduler was trained and tested with microbenchmarks written to stress particular behaviors in the system. The next step is to try scheduling real applications.
</p>
