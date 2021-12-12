---
title: "[Complete React Developer in 2022]設定專案"
image: /blog/2021/12/12/React-Tutorial-03/thumbnail.png
date: 2021-12-12 17:36:42
tags:
- React
categories: 
- Complete React Developer in 2022
description: 從這堂課開始，會實際做出一個電商網站，並從中學習關於React的知識。通常大型專案都會運用到git來做版本控管，這邊會介紹幾個簡單的Git指令。...
---

**<font color=#FF6600>本篇為Complete React Developer in 2022教學影片筆記文</font>**

## Git

從這堂課開始，會實際做出一個電商網站，並從中學習關於React的知識。通常大型專案都會運用到git來做版本控管，這邊會介紹幾個簡單的Git指令。

當我們要把別人的專案clone一份到本地端的時候，我們會用以下指令，第三個參數是專案的位置，第四個是package name

> git clone git@github.com:ZhangMYihua/lesson-3.git cloned-repo

當我們把檔案pull時，會在本地端有一份相同的檔案，但因為這是別人的git，我們不能直接Push上去更改檔案，所以我們必須改變remote。

當我們輸入git remote的時候會出現本地端的分支(origin)，這個分支是動連到別人的git。改變的方式就是先刪掉再新建。

> git remote remove origin

> git remote add origin git@github.com:tony11tony11t/reactLesson-Ecommerce.git

接著就可以push檔案到分支上了，第三個參數是remote的名稱，第四個參數是分支名稱

> git push origin master

更快的方法是fork別人的專案，這樣自己的git就會有一份專案的複製品了。

## Sass

一種加入巢狀概念來編寫的css，並且可以擁有變數等一般語言的特性。

> yarn add node-sass

這裡可能會遇到一個版本問題，可以在下指令的時候加入版本號來解決問題，如下面的範例：

> yarn add node-sass@6.0.0

## yarn.lock

我們在與他人共同協作的時候，因為大家各自在各自的電腦，開發環境中的每個package版本會有所不同，這個文件幫project鎖定住所有package的版本，讓大家的開發環境統一。

## Update Version

當我們要把project的所有package都更新到最新版的時候，可以依照以下的步驟來執行：

1.  刪除yarn.lock or package.json.lock，這兩個檔案一個是npm製作的一個是yarn製作的，都是為了鎖定開發環境用的，這裡是要更新到最新版，所以必須先刪除他。
2. npm update -D，-D表示所有dependencies
3. 接著就可以照著他的指示做，有可能會有vulnerability產生，嘗試去修復他即可。
