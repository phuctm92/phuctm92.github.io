---
title: "Docker vs Virtual Machine"
date: 2022-09-12 15:00:00 +0700
categories: [Programming]
tags: [Devops]

---
A virtual machine and Docker container differences.
<!--more-->

|**Virtual Machine** | **Docker Container** |
|--|--|
Hardware-level process isolation | OS level process isolation
Each VM has a separate OS | Each container can share OS
Boots in minutes|Boots in seconds
VMs are of few GBs|Containers are lightweight (KBs/MBs)
Ready-made VMs are difficult to find|Pre-built docker containers are easily available
VMs can move to new host easily|Containers are destroyed and re-created rather than moving
Creating VM takes a relatively longer time|Containers can be created in seconds
More resource usage|Less resource usage


## 5. Reference
[https://geekflare.com/docker-vs-virtual-machine/](https://geekflare.com/docker-vs-virtual-machine/){:target="_blank"}

___
*“Learn as if you will live forever, live like you will die tomorrow.” — Mahatma Gandhi*{: .text-center.text-success}
