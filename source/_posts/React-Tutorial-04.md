---
title: "[Complete React Developer in 2022]React Router and Routing"
image: /blog/2021/12/12/React-Tutorial-04/thumbnail.png
date: 2021-12-12 17:38:42
tags:
- React
categories: 
- Complete React Developer in 2022
description: 一個網站會有很多網頁，以前的方式是當使用者loading一個網頁時，他會從server把所有檔案傳送過來，但React不這麼做，React只載入一個HTML file...
---

**<font color=#FF6600>本篇為Complete React Developer in 2022教學影片筆記文</font>**

一個網站會有很多網頁，以前的方式是當使用者loading一個網頁時，他會從server把所有檔案傳送過來，但React不這麼做，React只載入一個HTML file，利用javaScript來更換頁面，要實現這個功能我們必須下載react-router-dom，透過這個package來控制我們的網頁路徑，這個package是利用瀏覽器的history API來達到就算是用javaScript換頁也可以有上一頁下一頁的歷史紀錄，跟傳統的網頁一樣，但比傳統網頁的體驗更好一些。

> 最近react-router-dom有新的6.0.0版本，此教學文為5.0.0，因寫法稍有不同所以在此註記。
> 

## Conflict

當我們安裝完成package並且要下yarn start的指令的時候，可能會遇到package與現有create react app這個package有版本的衝突，解決的方法是在package.json裡面加入以下程式碼：

```jsx
"resolutions":{
	<package name> : <version number>	 //"babel-jest" : "24.7.1"
}
```

## Route

首先我們要在App.js新增一個tag

```html
ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```

下面是Route的寫法，Route tag有3種attributes，一般來說只要url相同，react就會載入後面標記的component，例如現在的url是/hats，react就會把兩個Route都載入，並不用「完全」相同，為了避免以上問題，我們會加上exact attribute，表示此Route的path一定要跟url完全相同才行，多一個字少一個字都不行。

再來還有一個問題，如果今天兩個Route都符合條件就會都載入，但我們只需要一個的話，就會用Switch包起來，跟程式的switch邏輯一樣，由上開始往下判斷，只要有一個符合就會只載入那一個，所以當我們沒有在第一個Route加上exact的時候，我們不管url是甚麼都會符合，這個Switch就會永遠都載入第一個，要小心。

```html
<Switch>
	<Route exact path='/' component = {HomePage} />
	<Route path='/hats' component = {HatsPage} />
</Switch>
```

## withRouter

每個被Route呼叫的component都會帶入一些props，包含一些url的資訊，當我們今天是此component的下下層要使用這些資訊的時候，就會產生需要一直往下傳的props tunnels，這時候就可以利用withRouter來取得這些資訊，避免往下傳送更多的資訊。

```html
const MenuItem = ({title , imageUrl , size , linkUrl , history , match}) => (
    <div className={`menu-item ${size ? size : ""}`} onClick={() => history.push(`${match.url}${linkUrl}`)}>
        <div className='backgroundImage' style={{
                backgroundImage:`url(${imageUrl})`
        }}
        />
        <div className='content'>
            <h1 className='title'>{title.toUpperCase()}</h1>
            <span className='subtitle'>SHOP NOW</span>
        </div>
    </div>
);

export default withRouter(MenuItem)
```

## Link and Dynamic change page

當我們要製作一個切換分頁的按鈕時有兩種方法，第一種是用Link tag，可以指定要去到的page，跟html的a tag一樣。第二種方法是呼叫history.push()方法，history是Route載入component時給他的參數，有許多可以對history操作的API。

```html
<Link to='/hats' />
<div onClick={() => history.push(`${match.url}${linkUrl}`)} />
```