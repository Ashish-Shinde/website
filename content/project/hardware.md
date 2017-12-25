+++
# Date this page was created.
date = "2016-04-27"

# Project title.
title = "RTL Design, Verification, ASIC Design Projects"

# Project summary to display on homepage.
summary = ""

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "hardware.png"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
#tags = ["deep-learning"]
tags = ["hardware"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
#[header]
#image = "headers/bubbles.jpg"
#image = "bubbles.jpg"
image = ""
#caption = "My caption :smile:"
#url_video = "https://www.youtube.com/watch?v=9dF-Sq_3M-El"
+++

### Sorting Accelerator
![alternative text for search engines](/img/accel5.PNG)
Designed a sorting accelerator to sort an array of integers of unknown lenght. The baseline design consisted a quick-sort benchmark running on a CPU. The alternative design consisted a processor and an accelerator sharing a data cache through an arbiter while the processor also has a private instruction cache. The accelerator can have up to 32 special resisters to implement the Proc-Accel protocol. These registers are manily used to store the information such as source and destination array pointers, their sizes and some FSM control bits. The accelerator was implemented using a 8-element/4-element bitonic sorting network to sort two/one cache-lines at a time and these sorted elements were later merged on the CPU.

The ASIC toolflow was implemeted using Synopsy DC, ICC and PT to compare the area, energy and cycle time of the baseline and alternative accelerator design. The diagram above shows the amoeba plot of the accelerator. The results are summarized in the table below:  

|                    | Baseline | 4-Element Sorter | 8-Element Sorter |
|--------------------|----------|------------------|------------------|
|`Area(um^2)`        | 964372   |  965894          |1118146           |  
|`Constraint(ns)`    | 2        |    2             |   2              |
|`Slack(ns)`         | -0.14    |  -0.20           | -0.34            |
|`Exec. Time(cycles)`| 16853    |  18682           | 13299            |
|`Power(mW)`         | 82.2     |  77.4            | 85.8             |
|`Energy(nJ)`        | 3446.56  |  3543.62         | 3627.87          |
### SV Test Bench
![alternative text for search engines](/img/bus1.PNG)
Designed a layered system verilog test bench for the 4x4 on-chip bus network shown in the figure above. Implemented the environment, driver, receiver, coverage and scoreboard classes. The scoreboard receives and compares the transaction from driver and receiver using the mailboxes. The scoreboard class also instantiates the coverage class which implements cover points and cover groups to check the functional coverage. More test cases (direct and random) can be added to the testcase class to achieve high functional coverage. 

### Pipelined Processor
![alternative text for search engines](/img/proc1.PNG)
The baseline design consisted a five stage pipelined processor for TinyRV2 ISA as shown in the figure above. To resolve the data dependencies such as read-after-write (RAW), the processor implements stalling in decode (D) stage of the pipeline. For control hazards, we use simple branch prediction scheme where we assume the branch is not taken and squash the pipeline when the branch is actually taken. The alternative design implements hardware bypassing instead of stalling to improve the CPI.

The CPI results for various benchmarks are summarized below:

| Benchmark     | Baseline | Alternative |
|---------------|----------|-------------|
|`vvadd-unpot`  | 2.22     |  1.32       |  
|`vvadd-opt`    | 1.11     |  1.11       |
|`cmult`        | 2.65     |  2.53       |
|`bsearch`      | 2.97     |  1.39       |
|`cmult`        | 3.99     |  2.15       |

### Superscalar Processor
![alternative text for search engines](/img/super3.PNG)
We attempted to design a dual-issue, in-order, stalling pipelined superscalar processor. The ASIC toolflow was used to compare the area, energy and cycle time of the superscalar processor with the single-issue, stalling pipelined processor. The superscalar processor can fetch, decode and execute two independent instructions at a time. The instructions such as ADD, ADDI can be issued in both the pipes, while the instructions such as LW, MUL can be issued only in the second pipe. Therefore, the instructions are swizzeled in the decode (D) stage before issuing them to the appropriate pipe. The processor uses stalling for inter and intra fetch-block data dependencies.

The superscalar processor improves the CPI for various benchmarks by 12% to 48%. The power, energy, execution time comparision for one of the benchmarks is as follows:
 
|                    | Single-issue | Dual-issue       |
|--------------------|--------------|------------------|
|`Area(um^2)`        | 93531        |  157805          |  
|`Constraint(ns)`    | 2            |    2             |
|`Slack(ns)`         | -0.01        |  -0.06           |
|`Exec. Time(cycles)`| 558          |  327             |
|`Power(mW)`         | 7.8          |  12.6            |
|`Energy(nJ)`        | 8.8          |  8.5             |
  
### Blocking Cache
![alternative text for search engines](/img/cache1.PNG)
The baseline design consisted a direct-mapped, write-back cache. The datapath of this baseline design is shown above while the control path included a FSM. The cache has 16 four-word (16 bytes) cache lines with a total capacity of 256 bytes. Each cache line also has a corresponding valid bit and dirty bit (for write-back cache) in the control unit. The alternative design attempts to reduce the miss rate (specificaaly conflit misses) by implementing a 2-way set associative cache. The alternative design has same capacity and uses LRU replacement policy for cache line eviction.

We wrote various benchmarks to compare the performance of both the deisgns for addresses with different spatial and temporal locality. Generally, the miss rate is comparable for benchmarks with high temporal and spatial locality. But for the benchmark such as pointer-chase or non-unit strides which has low temporal and spatail locality, the alternative design has lower miss rate due to reduced conflict misses. In some cases due to higher capacity misses, the baseline has lower miss rate than the alternative design.  
