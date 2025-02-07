#linux #operatingsystems #linuxcommandline #bash 
# Introduction

`cgroups` (control groups): used to keep resource-hungry processes in check, manage containers effectively, and prioritize workloads.
## What are Cgroups?

At their core, `cgroups` are a kernel feature that allows you to partition and limit the system resources (CPU, memory, disk I/O, network, etc.) that a group of processes can use. Think of them as **virtual cages** where your can corral processes and set rules for their behavior. This gives you fine-grained control over how your system's resources are allocated, ensuring that critical processes get the resources they need while preventing others from hogging everything.
## Why use `cgroups`?

1. **Resource Management**: This is the bread and butter of cgroups. You can set hard limits on how much of a particular resource a group of processes can consume, ensuring fairness and *preventing resource exhaustion*.
2. **Prioritization**: Need to make sure your database server gets priority access to the CPU? Cgroups allow you to assign relative weights to different cgroups, giving some processes preferential treatment. 
3. **Accounting**: Cgroups meticulously track the resource usage of each group, giving you valuable insights into how your system is being utilized. This data can be invaluable for performance tuning and capacity planning.
4. 