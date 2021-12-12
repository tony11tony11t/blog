---
title: "[Master the Coding Interview]Stacks+Queues"
image: /blog/2021/12/12/Master_The_Coding-DS-Stacks+Queues/thumbnail.png
date: 2021-12-12 17:21:14
tags: 
- Data structure
categories: 
- Master the Coding Interview
description: LIFO(last in first out)的一種資料結構，可以把他想像成疊盤子，一直往上疊，最先疊的最後才能拿到，最後疊的最先可以拿到，push跟pop都是O(n)，lookup則是要O(n)...
---

**<font color=#FF6600>本篇為Master the Coding Interview教學影片筆記文</font>**

## Stack

LIFO(last in first out)的一種資料結構，可以把他想像成疊盤子，一直往上疊，最先疊的最後才能拿到，最後疊的最先可以拿到，push跟pop都是O(n)，lookup則是要O(n)。

## Queues

FIFO(first in first out)的一種資料結構， 可以把他想像成排隊，第一個排的人會先出去，以此類推到最後一位，對queues來說enqueue跟push一樣，只是他是從最後面進去，是O(n)的動作，pop就是dequeue，會先把第一個進來的丟出去，一樣也是O(n)，lookup則跟stack一樣O(n)，不一樣的是我們不會用array來做queue，如果用array的話我們每dequeue一個node就要shift所有的node，非常糟糕。

## JavaScript Engine

JS可以在chrome上解析主要是依靠V8，透過他來轉換js code，變成可以給瀏覽器執行的語法。V8 engine裡面有Memory Heap和Call Stack， 當我們創建一個變數的時候，會在memory Heap裡面產生一個位置來存放他，當我們超出可以存放的位置時，瀏覽器就會有memory leak的情況發生，由此可知全域變數並不好，因為她會一直存在於memory Heap不會自己清除，導致memory leak的產生。當我們在執行code的時候，每一行code都會被加入call stack，透過call stack來決定執行的順序。

```jsx
const one = () =>{
	const two = () =>{
		console.log('4')
	}
}

//call stack
//console.log('4')
//two
//one
```

## Implement an stack(Linked list)

```jsx
class Node{
	constructor(value){
		this.value = value;
		this.next = null
	}
}

class Stack{
	constructor(){
		this.top = null;
		this.bottom = null;
		this.length = 0;
	}

	peek(){
		return this.top;
	}

	push(value){
		const newNode = new Node(value);
		const OriginTop = this.top;
		this.top = newNode
		newNode.next = OriginTop
		if(this._isEmpty()) this.bottom = newNode
		this.length++;
		return this
	}

	pop(){
		if(this._isEmpty()) return null;
		if(this.top === this.bottom) this.bottom = null
		this.top = this.top.next;
		this.length--;
		return this
	}
	
	_isEmpty(){
		return this.length === 0
	}
}

const myStack = new Stack();
myStack.push("Tony");
myStack.push("John");
myStack.peek();
myStack.push("Eagle");
myStack.pop();
```

## Implement an stack(Array)

```jsx
class Stack{
	constructor(){
		this.arr = []
	}

	peek(){
		return this.arr[this.arr.length - 1];
	}

	push(value){
		this.arr.push(value)
		return this.arr
	}

	pop(){
		this.arr.pop()
		return this.arr
	}
	
	_isEmpty(){
		return this.arr.length === 0 
	}
}

const myStack = new Stack();
myStack.push("Tony");
myStack.push("John");
myStack.peek();
myStack.push("Eagle");
myStack.pop();
```

## Implement an queue(Linked list)

```jsx
class Node{
	constructor(value){
		this.value = value;
		this.next = null
	}
}

class Queue{
	constructor(){
		this.first = null;
		this.last = null;
		this.length = 0;
	}

	peek(){
		return this.first;
	}

	enqueue(value){
		const newNode = new Node(value);
		if(this._isEmpty()){
			this.first = newNode;
			this.last = newNode;
		}else{
			this.last.next = newNode;
			this.last = newNode;
		}
		this.length++;
		return this
	}

	dequeue(){
		if(this._isEmpty()) return null
		if(this.first === this.last) this.last = null
		this.first = this.first.next;
		this.length--;
		return this
	}
	
	_isEmpty(){
		return this.length === 0
	}
}

const myQueue = new Queue();
myQueue.enqueue("Tony");
myQueue.enqueue("John");
myQueue.peek();
myQueue.enqueue("Eagle");
myQueue.dequeue();
```

## When can use arry?

| 優點 | 缺點 |
| --- | --- |
| Fast Peek | Slow lookup |
| Fast Operations |  |
| Ordered |  |

補充：[LeetCode 232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)