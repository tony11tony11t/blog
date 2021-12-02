---
title: "[Master the Coding Interview] BigO介紹"
date: 2021-12-02 10:09:40
tags: 
- BigO 
categories: 
- Master the Coding Interview
description: 什麼是好的程式碼，好的程式碼是Readable和Scalable的，BigO可以拿來測量程式的執行速度，所以這章會著重在Scalable的部分。...
image: /blog/2021/12/02/Master_The_Coding-BigO/thumbnail.png
---

**<font color=#FF6600>本篇為Master the Coding Interview教學影片筆記文</font>**

### What is good code?

什麼是好的程式碼，好的程式碼是Readable和Scalable的，BigO可以拿來測量程式的執行速度，所以這章會著重在Scalable的部分。

### BigO

BigO為什麼會存在，因為當我們要判斷一個code好或不好的時候，如果用執行的時間來看的話，因為每個電腦CPU的不同，會有執行速度上的差異，同樣的code不同的設備會有不同的速度，所以不能以時間來做為依據，這時候我們就會用BigO來判斷code執行速度。

BigO主要是利用程式執行多少步驟來做計算，拿以下的程式碼來說：

```jsx
function printHappy(n){
	for(let i = 0 ; i < n ; i++){
		console.log("Happy")
	}
}

printHappy(n);  //O(n) -->linear time
```

假設今天n是1，那這個for迴圈就會執行1次，n=2就會執行兩次，n=100就會執行100次，以此類推，我們可以發現n跟執行的次數呈現一個正比，並且是線性的增加，透過這個方式我們可以說這個printHappy的函式時間複雜度是O(n)。

O(1)表示constant time，表示不管甚麼input進去，這個function都會執行一樣數量的步驟，是時間複雜部裡面最好的一種。

**BigO Challenge**

```jsx
function funChallenge(input) {
  let a = 10;  //O(1)
  a = 50 + 3;  //O(1)

  for (let i = 0; i < input.length; i++) { //O(n)
    anotherFunction(); //O(n)
    let stranger = true; //O(n)
    a++; //O(n)
  }
  return a; //O(1)
}
```

首先，有些人說賦值不能算是一個步驟，但這邊先不討論這部分，所以賦值就給他O(1)，for迴圈的東西就是執行n次，接著將所有的BigO加起來，我們會得到O(3 + 4n)的時間複雜度的，接著我們就會簡化她，把常數消掉後，取最複雜的那個就好，所以這題的答案是O(n)。

當然我們在面試的時候，不會一行一行的算出來，我們必須一眼就看出時間複雜度為何，以下有四個遵循的規則：

1. Worst Case
永遠要設定成最糟的情況，因為BigO只會看最壞情況。
    
2. Remove Constants
因為input要假設成一個很大很大的數字，所以常數對他們來說不重要。
    
3. Different terms for inputs
不同的input要用不同的代數去寫，假設function裡面有兩個迴圈一個有m個element一個n個element的話，會把結果寫成O(m + n)，因為不會知道到你m多還是n多，所以都要寫上去。
    
> 如果兩個迴圈都同樣有n個element，並且又是一個巢狀的話，我們就可以把結果寫成O(n^2)，這是一個不好的時間複雜度，很多面試就是要請你把O(^2)變成較好的時間複雜度。
    
```jsx
for (let i = 0; i < n; i++) { //O(n)
    for (let j = 0; j < n; j++) { //O(n)
    console.log(i,j)
    }
}
```
    
4. Drop Non Dominants
丟掉不重要的部分，假設function裡面有一個時間複雜度是O(n)，一個是O(n^2)，我們會取最複雜的，也就是O(n^2)。
    
O(n!)這是最糟糕的時間複雜度，等於說每次執行loop都要加一個element，絕對要避免。

到這邊已經介紹了3種時間複雜度，接著要回到Scalable這個點上，時間複雜度表示的是他的run time，但除了時間，memory也是注重的一個環節，要符合Scalable，必須考慮時間跟空間，雖然現在的memory越來越大，但她不是無限的，我們仍然要注意使用的大小。

```jsx
function boo(n){
	for (let i = 0; i < n; i++) { //O(n)
    console.log(i)
	}
}
boo(5) //O(1)

function arrayOfHiNTimes(n){
	let hiArray = [];
	for (let i = 0; i < n; i++) { //O(n)
    hiArray[i] = 'hi'
	}
}

arrayOfHiNTimes(6)  //O(n)
```

第一個function裡面，雖然是一個迴圈，但我們只有在for迴圈裡面宣告一個i，整個函式也只有宣告這個東西，可以說boo function的空間複雜度為O(1)。第二個就不一樣了，因為我們宣告了一個陣列，並且在陣列加入了n個elements，所以arrayOfHiNTimes function的空間複雜度為O(n)。

通常我們會用空間換取時間或時間換取空間，這沒有甚麼對或錯，看當下的project要怎麼做就好。