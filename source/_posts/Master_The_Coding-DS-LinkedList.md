---
title: "[Master the Coding Interview]Linked List"
image: /blog/2021/12/12/Master_The_Coding-DS-LinkedList/thumbnail.png
date: 2021-12-12 17:16:14
tags: 
- Data structure
categories: 
- Master the Coding Interview
description: 從字面上的意思翻譯就是一種有連結的列表，列表中的每一個node都有兩項東西，一個是自己本身的值，另一個是pointer指向下一個node，以此方式串聯下去，最後一個node會指向null...
---

**<font color=#FF6600>本篇為Master the Coding Interview教學影片筆記文</font>**

從字面上的意思翻譯就是一種有連結的列表，列表中的每一個node都有兩項東西，一個是自己本身的值，另一個是pointer指向下一個node，以此方式串聯下去，最後一個node會指向null，表示後面沒有東西。LinkedList雖然表面上array很像，但他在最前面和最後面插入的時候，不用去移動整個陣列，時間複雜度會從原本array的O(n)變成O(1)，其他部分的lookup、insert、delete都維持O(n)。

## Implementing an Linked List

```jsx
class Node{
	constructor(v){
		this.value = v;
		this.next = null;
	}	
}

class LinkedList{
	constructor(v){
		this.head = {
			value: v,
			next: null
		}
		this.tail = this.head
		this.length = 1;
	}

	append(v){
		const newNode = new Node(v)
		this.tail.next = newNode;
		this.tail = newNode;
		this.length++;
		return this
	}
	
	prepend(v){
		const newNode = new Node(v)
		newNode.next = this.head
		this.head = newNode
		this.length++;
		return this
	}

	printList(){
		const array = [];
		let currentNode = this.head;
		while(currentNode !== null){
			array.push(currentNode.value);
			currentNode = currentNode.next;
		}
		return array;
	}
	
	insert(index , v){
		if(index >= this.length){
			return this.append(v);
		}else if (index === 0) {
		  return this.prepend(v);
		}

		const newNode = new Node(v)
		const leader = this.traversToIndex(index - 1);
		const holdingPoter = leader.next;
		leader.next = newNode;
		newNode.next = holdingPoter;
		this.length++;
		return this;
	}

	remove(index){
		if(index >= this.length){
			const leader = this.traversToIndex(this.length - 2)
			leader.next = null;
			this.tail = leader;
			this.length--;
			return this
		}
		if(index == 0){
			this.head = this.head.next;
			this.length--;
			return this
		}

		const leader = this.traversToIndex(index - 1)
		const unwantedNode = leader.next
		leader.next = unwantedNode.next
		this.length--;
		return this
	}

	traversToIndex(index){
		let nowNode = this.head;
		let counter = 0;
		while(counter !== index){
			nowNode = nowNode.next
			counter++;
		}
		return nowNode
	}
}

const myLinkedList = new LinkedList(10);
myLinkedList.append(5);
myLinkedList.append(16);
myLinkedList.prepend(1);
myLinkedList.insert(2 , 99);
myLinkedList.printList();
```

## Doubly Linked Lists

一般來說linked list是單向的結構，我們只能從head開始到tail，但如果在每個node上都在多一個資料紀錄上一個node，那這個linked list就會變成雙向，從頭到尾或是從尾到頭都可以查找到所有node，以時間複雜度來說的話，doubly linked lists的查找可以比單向的節省1半的時間，因為可以同時從頭跟尾開始找，但bigO依舊還是O(n)。

## Reverse Linked Lists

反轉單向鏈結串列是一個很常見的面試題，下面的程式碼銜接上面的linked list，是其中的一個方法：

```jsx
reverse(){
	if(!this.head.next) return retrun this.head;
		
	let first = this.head;
	let second = first.next;

	this.tail = this.head;

	while(second){
		const temp = second.next
		second.next = first;
		first = second;
		second = temp;
	} 
	this.head.next = null;
	this.head = first;
	return this;
}
```

## When can use arry?

| 優點 | 缺點 |
| --- | --- |
| Fast Insertion | Slow lookups |
| Fast Deletion | More Memory |
| Ordered |  |
| Flexible Size |  |