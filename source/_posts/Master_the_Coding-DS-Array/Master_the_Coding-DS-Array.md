---
title: "[Master the Coding Interview]陣列"
image: /blog/2021/12/07/Master_the_Coding-DS-Array/thumbnail.jpeg
date: 2021-12-07 19:38:08
tags: 
- Data structure
categories: 
- Master the Coding Interview
description: 在javaScript的世界裡，array並不是一個固定的資料結構，他本身算是dynamic array，會自動的伸縮長度，所以我們不用擔心記憶體分配不足的問題，但在較低階的語言...
---
```jsx
const strings = ['a' , 'b' , 'c' , 'd']

string[2] //O(1)

//push
strings.push('e'); //O(1)

//pop
strings.pop(); //O(1)

//unshift
strings.unshift('x'); //O(n)

//splice
strings.splice(2,0,'alien') //O(n)
```

在javaScript的世界裡，array並不是一個固定的資料結構，他本身算是dynamic array，會自動的伸縮長度，所以我們不用擔心記憶體分配不足的問題，但在較低階的語言，例如C、C++，這種在宣告階段就要將陣列記憶體配置好，當我們要使用的範圍超出記憶體配置的時候，會進行擴增，通常會是增加2倍，例如原本有8個位置就新增到16個等等。所以當這種語言在進行陣列的append的時候，會先把原陣列複製到另外一塊記憶體並且擴充，時間複雜度會是O(n)，但javaScript裡面就只有單純的append，時間複雜度是O(n)。

## Implementing an array

JavaScript的Array其實是一種Object，所以我們要利用class的方式來自創一個array

```jsx
class MyArray{
	constructor(){
		this.length = 0;
		this.data = {};
	}

	get(index){
		return this.data[index]
	}

	push(item){
		this.data[this.length] = item;
		this.length++;
		return this.length
	}

	pop(){
		const lastItem = this.data[this.length - 1]
		delete this.data[this.length - 1];
		this.length--;
		return lastItem;
	}
	
	delete(index){
		const item = this.data[index];
		this.shiftItems(index)
		return item
	}

	shiftItem(index){
		for(let i = index ; i < this.length - 1; i++){
			this.data[i] = this.data[i + 1]
		}
		delete this.data[this.length - 1]
		this.length--;
	}
}

const newArray = new MyArray()
```

## Exercise：Reverse a string

```jsx
//my answer
function reverse1(str){
	return str.split("").map((_ , i) => str[str.length - i - 1]).join('')
}

//video answer
function reverse2(str){
	//check input
	if(!str || str.length < 2 || typeof str !== 'string') return false

	const backwards = [];
	const totalItems = str.length - 1;
	for(let i = totalItems ; i >= 0 ; i--){
		backwards.push(str[i]);
	}
	return backwards.join('')
}

//video better answer
const reverse3 = str => [...str].reverse().join('');
```

## Exercise：Merge Sorted Array

```jsx
//my answer
function mergeSortedArrays1(arr1,arr2){
	let ans = [];
	let arr1Index = 0 , arr2Index = 0
	while(arr1Index < arr1.length || arr2Index < arr2.length){
		if(arr1Index >= arr1.length) ans.push(arr2[arr2Index++])
		else if(arr2Index >= arr2.length) ans.push(arr1[arr1Index++])
		else{
				if(arr1[arr1Index] > arr2[arr2Index]) ans.push(arr2[arr2Index++])
				else ans.push(arr1[arr1Index++])
		}
	}
	return ans
}

//video answer
function mergeSortedArrays2(arr1,arr2){
	const mergedArray = [];
	let array1Item = array1[0];
	let array2Item = array2[0];
	let i = 1 , j = 1;

	//Check unput
	if(arr1.length == 0) return array2;
	if(arr2.length == 0) return array1;

	while(array1Item || array2Item){
		if(!array2Item || array1Item < array2Item){
			mergedArray.push(array1Item);
			array1Item = array1[i]
			i++
		}else{
			mergedArray.push(array2Item);
			array2Item = array2[j]
			j++
		}
	}

	return mergedArray;

}
```

## When can use arry?

| 優點 | 缺點 |
| --- | --- |
| Fast lookups | slow inderts |
| Fast push/pop | slow delete |
| ordered | Fixed size(static array) |