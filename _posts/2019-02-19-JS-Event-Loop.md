---
layout: default
title: JS learning note
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

### Event loop model
选择当前要执行的任务队列，选择任务队列中最先进入的任务，如果任务队列为空即null，则执行跳转到微任务（MicroTask）的执行步骤。
将事件循环中的任务设置为已选择任务。
执行任务。
将事件循环中当前运行任务设置为null。
将已经运行完成的任务从任务队列中删除。
microtasks步骤：进入microtask检查点。
更新界面渲染。
返回第一步。


执行进入microtask检查点时，用户代理会执行以下步骤：

设置microtask检查点标志为true。
当事件循环microtask执行不为空时：选择一个最先进入的microtask队列的microtask，将事件循环的microtask设置为已选择的microtask，运行microtask，将已经执行完成的microtask为null，移出microtask中的microtask。
清理IndexDB事务
设置进入microtask检查点的标志为false。

[EventLoopModel](https://pic3.zhimg.com/v2-bd2aa27705ca757fc676a37505a4f992_b.gif)