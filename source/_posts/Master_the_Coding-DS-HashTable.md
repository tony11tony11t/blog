---
title: "[Master the Coding Interview]雜湊表"
image: /blog/2021/12/07/Master_the_Coding-DS-HashTable/thumbnail.png
date: 2021-12-07 19:38:08
tags: 
- Data structure
categories: 
- Master the Coding Interview
description: hash table是一個包含key和value的一張表，每個語言都有不同的資料型態來呈現hash table，javaScript一樣還是Object。當我們要存入一筆資料時...
---

**<font color=#FF6600>本篇為Master the Coding Interview教學影片筆記文</font>**

hash table是一個包含key和value的一張表，每個語言都有不同的資料型態來呈現hash table，javaScript一樣還是Object。當我們要存入一筆資料時，值會經過hash function轉換出一個address給memory儲存，所以當我們要讀取、刪除、插入資料時都是O(1)。

hash function是一種加密的函式，最常見的是MD5，還有其他像SHA-1或SHA-256等等，透過function可以把value轉換成一串string，這串string是idempotent的形式，表示每一次相同的字串都會產生相同的結果，不會因為時間還是其他因素而改變。

## Collision

儘管hash table非常快速，他還是有可能會發生衝突，例如當兩個值被計算出來都要放在同一個位置時，有一種方式是直接將每個adress都變成linked-list，雖然可以儲存資料，但時間複雜度就會變成O(n)，另外一種解決方式是Open addressing，如果放入的位置上已經有value，就會再利用hash function(最簡單就是linear的方式解，如果150不行就151以此類推)找出第二個位置，一直找到可以存放的位置即可，這種方法可以有效的運用hash table。

## Implementing an Hash Table

```jsx
class HashTable{
	constructor(size){
		this.data = new Array(size)
	}

	//小小淺規則，如果function前面有underline表示這是一個private function
	_hash(key){
		let hash = 0;
		for(let i = 0; i<key.length;i++){
			hash = (hash + key.charCodeAt(i) * i) % this.data.length
		}
		return hash
	}
	
	set(k , v){
		let address = this._hash(k)
		if(!this.data[address]){
			this.data[address] = []
		}
		this.data[address].push([k,v])
		return this.data
	} //O(1)

	get(k){
		let address = this._hash(k)
		const currentBucket = this.data[address]
		if(currentBucket){
			for(let i = 0 ; i < currentBucket.length ; i++){
				if(currentBucket[i][0] == 'k')
					return currentBucket[i][1]
			}
		}
		return undefined
	} //O(1), somethings use the bad hash function, it's O(n)

	keys(){
		const keysArray = [];
		for(let i = 0 ; i < this.data.length; i++){
			if(this.data[i]){
				this.data[i].forEach(arr => keysArray.push(arr[0]))
			}
		}	
		return keysArray;
	}
}

const myHashTable = new HashTable(50)
myHashTable.set('grapes' , 10000);
myHashTable.set('apple' , 1000);
myHashTable.set('banana' , 100);
myHashTable.get('grapes');
myHashTable.keys();
```

## Exercise：First Recurring Charactor

```jsx
//Google Question
//Given an array = [2,5,1,2,3,5,1,2,4] return 2
//Given an array = [2,1,1,2,3,5,1,2,4] return 1
//Given an array = [2,1,3,4] return undefined

// my answer
function firstRecurringCharactor(arr){
	let hashTable = {}
	for(let i = 0 ; i < arr.length ; i++){
		if(hashTable[arr[i]]) return arr[i]
		hashTable[arr[i]] = true 
	}
	return undefined
}
```

## When can use arry?

| 優點 | 缺點 |
| --- | --- |
| Fast lookups | Unordered |
| Fast inserts | Slow key iteration |
| Flexible Keys |  |