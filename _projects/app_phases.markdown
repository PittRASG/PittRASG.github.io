---
layout: page
title: Detection and Scheduling of Application Phases
description: Intelligent Characterization and Scheduling of Application Phases for Energy Efficiency in Heterogeneous Processors
---

<!-- List of collaborators -->
<h4>Collaborators</h4>
<ul>
    <li><a href="https://people.cs.pitt.edu/~mosse/">Daniel Mossé</a></li>
    <li>Vasco Xu</li>
    <li>Nathan Ackerman</li>
</ul>

<!-- Overview of the project -->
<h4>Overview</h4>
<p>
In recent years, energy consumption has become one of the most important issues in computer systems due to its increasing power demands. As computing devices become indispensable parts of people’s daily lives, efficient energy management is crucial in reducing carbon emissions and promoting a sustainable world. 
<br><br>
A principal limiting factor to improvements in computing performance is power. Therefore, chip manufacturers have moved towards building heterogeneous processors that balance performance and power efficiency. ARM’s big.LITTLE is an example of a heterogeneous processor; it uses two types of processors, “big” and “LITTLE”, with the same instruction set architecture (ISA), running on a single SoC (system on chip). “LITTLE” processors are designed to maximize energy efficiency while “big” processors are designed to provide maximum compute power. Energy efficiency can be achieved in heterogeneous processors by assigning tasks to the core that it is best suited for, which is not a trivial task. 
<br><br>
A common approach to energy management in modern computing systems is Dynamic Voltage/Frequency scaling (DVFS), which dynamically adjusts voltage and frequency levels according to different workloads. DVFS is performed on a per-core basis, which is optimal for achieving energy efficiency on a single core. However, in heterogeneous multi-core systems we must also consider thread-to-core assignment, under the assumption that big cores are best suited for computationally-heavy tasks and small cores are best suited for I/O-bound tasks.
<br><br>
This research project aims to characterize application phases and use machine learning to appropriately schedule phases to the cores they are best suited for to achieve a balance between energy-efficiency and performance. 
</p>

<!-- Project Objectives -->
<h4>Project Objectives</h4>
<p>
The objectives of the proposed project are (1) to efficiently track Linux HPCs (hardware performance counters), (2) characterize application phases through clustering, (3) build a machine learning model that accepts as input a set of the current HPCs along with a list of previous HPCs to predict performance speedup, and (4) migrate the current task to a different core if the predicted performance speedup is above a certain threshold.
</p>

<!-- References -->
<h4>References</h4>
<ol>
    <li><a href="https://dl.acm.org/doi/abs/10.1145/3139645.3139664">Exploring Machine Learning for Thread Characterization on Heterogeneous Multiprocessors</a></li>
</ol>