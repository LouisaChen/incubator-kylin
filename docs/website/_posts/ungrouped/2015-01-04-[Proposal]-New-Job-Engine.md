---
layout: post
title:  "[Proposal] New Job Engine"
date:   2015-01-04
author: Qianhao Zhou (https://github.com/qhzhou)
categories: ungrouped
---

#Proposal
Currently Kylin has its own job engine in order to build a cube instance, however it is tightly coupled with the Cube Building process, which is difficult to maintain:

1. It cannot support other kinds of job except for Cube Build, such as sync up with data source, async query.

2. It is very difficult to expand, for example using SPARK to accelerate the building process.

3. It depends on [Quartz](http://quartz-scheduler.org/), however it only use very small part of the features of Quartz which can be replaced of the standard java api.

To solve the above problems, we can refactor the job engine in the following ways:

1. split the current job engine into 2 layers, job engine should only worry about the job execution and provide some basic job abstraction(for example map-reduce, shell cmd), on which the Cube Build Process should be based.

2. use the java ExecutorService to replace Quartz to remove this dependency.
