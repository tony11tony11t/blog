---
title: "[Complete React Developer in 2022]React介紹"
date: 2021-11-30 22:13:25
tags:
- React
categories: 
- Complete React Developer in 2022
description: 傳統的網頁呈現方式，是將所有的HTML、CSS、JS的檔案上傳到server，等到使用者要讀取網頁的時候再從server呼叫出來顯示在瀏覽器上，每一次有一個新的頁面時就會再重複一次從server讀取檔案的這個步驟，這是一套行之有年的網頁模式...
image: /blog/2021/11/30/React-Tutorial-01/thumbnail.png
---
**<font color=#FF6600>本篇為Complete React Developer in 2022教學影片筆記文</font>**

傳統的網頁呈現方式，是將所有的HTML、CSS、JS的檔案上傳到server，等到使用者要讀取網頁的時候再從server呼叫出來顯示在瀏覽器上，每一次有一個新的頁面時就會再重複一次從server讀取檔案的這個步驟，這是一套行之有年的網頁模式。但漸漸的問題來了，越來越多種瀏覽器問世，每種瀏覽器又有不同的編譯方式，導致開發者需要開發許多種網頁來因應每種瀏覽器，讓網頁開發增加了許多難度。

接著，jQuery問世了，他整合了所有瀏覽器的問題，做出了非常簡單的API工具，透過jQuery可以快速的讓使用者與網頁互動，並且大大縮短開發速度。但人的慾望沒有極限，工程師開始會想要開發更大的專案，功能開始變的複雜，像是Facebook，有帳戶、可以線上即時聊天、寄信等，不再只是像blog一樣發發文章做做新的頁面了。

當jQuery沒辦法再應付大型專案的時候，backbone.js出來了，SPA(single page application)的概念也跟著出來，網頁不再只是每次要新的就去server load，而是變成放大js的功能，縮小html的地位，利用js來改變當前html的內容，達到SPA的一個概念，這也是為什麼網頁不再只是一個頁面而是稱為應用程式了。

2010年，由Google創造的Angular.js出現，不同於jQuery，有了MVC的概念，把每一塊程式碼都變成一個包裹的概念，讓其不會互相干擾，讓工程師之間更容易合作。但很快就有一個問題出現了，網頁上的每個部份都會互相影響，迎來的是資料越來越散落在各個包裹裡，讓Debug越來越難。

2013年，Facebook是出了第一版的React，解決了資料流的問題，讓資料不會散落在各地，也是因為如此，2014年的時候Angular.js意識到自己沒辦法再創造出好的SPA後，他們直接重寫了library，並改名為Angular，的確就是把js拿掉，但也因為這個重寫，很多開發者直接轉向投入React，也讓現今一堆大公司都使用了React來作為主要框架。

以下是react的幾個原則：

1. Don't touch the DOM. I'll do it. 
只要給React資料，就可以利用他幫忙套入資料，不需要更改DOM來達到更換頁面呈現的資料。
    
2. Build websites like lego blocks
React的一大特性就是components，模組化跟樂高一樣，一個網頁就像是很多樂高很多組件拼湊而成的，開發的components還可以到處重複利用，十分彈性。
    
3. Unidirectional data flow
react的資料流向，有一個限制就是只能往下不能往上，資料只能單向溝通，這讓開發者可以更清楚知道資料在app裡面的流向，更容易去處理bug。
    
4. UI, The rest is up to you
React專注於ocmponenet的產生，只要有這個React的藍圖，我們就可以在任何地方建置他，手機、電腦、terminal等等都可以，這就是React跨平台的應用，當然，如果是一般的網頁，我們就要用到React何React-DOM
    
如果要成為一個成熟的React工程師，要記得以下三點開發的原則

1. Decide on Components
2. Decide the State and where it lives
3. What changes when state changes