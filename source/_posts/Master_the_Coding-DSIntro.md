---
title: "[Master the Coding Interview]資料結構介紹"
image: /blog/2021/12/07/Master_the_Coding-DSIntro/thumbnail.jpeg
date: 2021-12-07 19:38:08
tags: 
- Data structure
categories: 
- Master the Coding Interview
description: Data Structure就是電腦儲存資料的結構與方式，有非常非常多種資料結構，區塊鏈也是一種資料結構，但我們只需要知道幾種重要的就好，這邊需要了解的重點就是How to Build One和How to Use it。
---

**<font color=#FF6600>本篇為Master the Coding Interview教學影片筆記文</font>**

Data Structure就是電腦儲存資料的結構與方式，有非常非常多種資料結構，區塊鏈也是一種資料結構，但我們只需要知道幾種重要的就好，這邊需要了解的重點就是How to Build One和How to Use it。

## How Computers Store Data?

電腦儲存資料的方式有兩種，RAM和storage，如果需要快速的暫存資料，資料就會存在RAM裡面，當我們把電腦關掉的時候資料也一併會被清除，反之，當我們是需要電腦關機後資料還存在的話就需要把它存入storage，但讀取的速度就會較慢。當我們要向RAM取得資料時，CPU會告訴RAM controller他要的address，RAM controller就可以快速的幫CPU找到資料，不需要從第一個位置開始尋找。CPU本身也有一個非常小的Cache會把最近取得的資料記錄起來減少資料傳輸。

RAM的資料結構會像下面表格一樣：

| address | data |
| --- | --- |
| 0 | 00000000 |
| 1 | 00000000 |
| 2 | 00000000 |
| 3 | 00000111 |

假設我們今天宣告一個var a = 7，那記憶體就會用上面的方式幫我們存入，因為javaScript沒有integer，只有64bit的float，所以每一次存一個變數就是會占用八個位置。

有興趣可以看這篇：[64-bit floating point: a JavaScript story](https://medium.com/@sarafecadu/64-bit-floating-point-a-javascript-story-fa6aad266665)