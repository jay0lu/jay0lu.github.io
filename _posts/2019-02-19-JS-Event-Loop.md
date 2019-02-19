---
layout: default
title: Docker learning note
comments: true
---

### Heap
Data structure stored in binary-tree.

### Stack
Data sturcture stored in liner. LIFO.

### Queue
Data sturcture stored in liner. FIFO

***

## Event Loop
There are two types of task in JS, MacroTask(Task) and (MicroTask)

### MacroTask
Script, setTimeout, setInterval, I/O, UI Rendering.

### MicroTask
Process.nextTick, Promise, Object.observe, MutationOvserver

***

## Event Loop in browser
JS has a `main thread` and `call-stack`. All task will be put in `call-stack` waiting for `main thread` to call.

### Call-stack
LIFO

![Task Queue](https://pic3.zhimg.com/80/v2-971a09fea16fff72db03d498245bc892_hd.jpg)
