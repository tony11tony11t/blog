---
title: "[Complete React Developer in 2022]React基本概念"
image: /blog/2021/12/06/React-Tutorial-02/thumbnail.png
date: 2021-12-06 11:33:42
tags:
- React
categories: 
- Complete React Developer in 2022
description: npm是node package manage，可以利用這個指令在terminal做很多事情，yarm跟npm一樣，只是yarn是facebook開發的，以下是他們的指令對照...
---

**<font color=#FF6600>本篇為Complete React Developer in 2022教學影片筆記文</font>**

## NPM vs YARM

npm是node package manage，可以利用這個指令在terminal做很多事情，yarm跟npm一樣，只是yarn是facebook開發的，以下是他們的指令對照：

| Install dependencies from package.json | yarn | npm install |
| --- | --- | --- |
| Install a package and add to package.json | yarn add package  | npm install package  --save |
| Install a devDependency to package.json | yarn add package --dev | npm install package --save-dev |
| Remove a dependency from package.json | yarn remove package | npm uninstall package --save |
| Upgrade a package to its latest version | yarn upgrade | npm update --save |
| Install a package globally | yarn global add package | npm install package -g |

## NPX

npx是建立在npm下面的指令，假設我們在terminal下了下面這段指令：

> npm install -g cowsay
> 

表示我利用npm安裝cowsay這個package，-g表示global，安裝在全局，就是整個電腦的環境裡面。如果沒有寫-g表示安裝在當下資料夾裡面。

如果要解安裝只要在install前加上un即可。那甚麼是npx呢，簡單的理解就是說npx幫你先把package下載下來並且執行，一執行完馬上解安裝，讓你的電腦不會存在這個package以便節省記憶體。npx的寫法只要在後面加上package name和帶入的參數即可。

> npx cowsay hiiiiiii~~~
> 

## Create React App

這是facebook開發的package，用於快速打造react專案，以下介紹幾個地方表示的意義：

| package.json | 專案的所有設定都包含在這裡，包含版本、用的套件、腳本等。 |
| --- | --- |
| package.json → dependencies | 裡面是所有用到的套件以及版本 |
| package.json → dependencies→ react | 最重要的部分，react的核心庫 |
| package.json → dependencies→ react-dom | react是一個跨平台的框架，他可以利用react-native來建造手機app，又或者接上VR打造VR的應用程式等。在這邊因為是要開發網頁，所以要引入此package來控制網頁上的DOM。 |
| package.json → dependencies→ react-script | 給CLI用的腳本，透過在scripts裡面設定的指令可以讓CLI讀懂輸入的指令，例如start、build等 |

接著打開index.js可以發現程式的進入點，利用render function來渲染畫面，React.StrictMode主要是確認我們沒有用到版本遺棄的指令，讓程式處在一個安全的狀態。這邊有寫到在root這個節點裡面渲染，這個節點的位置在index.html裡面，這個檔案就是我們主要載入的html，react也只會載入這個html並置換裡面內容達到SPA的效果。

| start | 開啟server進行網頁預覽 |
| --- | --- |
| build | 將整個react專案打包，資料夾內會產生一個build資料夾，裡面只會有html、css和js，主要是給瀏覽器看的資料，通常我們也只會把build好的檔案丟到server上。 |
| test | 執行測試專案 |
| eject | 自訂webpack or babel的設定，當我們執行此指令後，會出現很多設定的檔案，這些設定主要用於build階段，但在此專案創建的時候，create react app這個指令其實都幫我們做了最優化的設定，所以沒事不需要更改。 |

## componenets

一段程式碼用來顯示視覺化的UI，UI包含HTML、CSS、javaScript。透過ReactDOM，我們可以把component當作HTML tag來使用。一般來說建立component有兩種方式，class和hooks，hooks，一般我們都會用class來建立，因為很多程式語言都有物件導向的觀念，所以這邊先介紹class版的components

### State

```jsx
class App extends Component{

	//建構子，主要是設定state初始值的地方
  constructor(){
		//繼承Component，主要用於呼叫Component的建構子
    super();

		//設定state
    this.state = {
      string : "Hello Tony"
    }
  }

  render(){
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>{ this.state.string }</p>
					{/*在onclick裡面加上setState的方法，讓按鈕可以更改string字串*/}
          <button onClick={() => this.setState({string: 'Hello Tang Jia Jun'})}>Change Text</button>
        </header>
      </div>
    );
  }
}
```

這是將範例改成class的形式，按下按鈕可以更改文字內容，這邊的重點是state，react的核心，透過setState可以改變資料內容，利用這個特性可以達成網頁的互動效果。那renden裡面的html內容又是甚麼呢？他是jsx，和html很像，是react用來編譯成html的一種形式，當我們的畫面有變動的時候，也就是setState讓state有更動的時候，就會觸發render的執行，把更改的html送回UI上。

setState是一個非同步的指令，表示這個指令並不會立即的執行，所以他的第二個參數是callback function，當setState成功後會執行的function，可以利用這個部分來測試setState是否成功。

### Asynchronous setState

當我們在使用setState的時候，因為他是非同步行為，不會即時更改，所以當我們要做類似計數器的功能的時候，要避免以下的寫法：

```jsx
this.setState({count:this.state.count + 1})
```

上面的程式碼看似沒問題，但因為react會等到適當的時機才執行這段程式碼，我們不能保證每次取到的count值都已經被+1了，有可能兩次的setState都取得同樣的count值，要解決以上問題，就必須在setState裡面帶入函式：

```jsx
this.setState((prevState, prevProps) => {
	retrun {count : prevState.count + 1}
})
```

這邊就先停住，更多的資訊可以看這篇 [https://medium.com/javascript-scene/setstate-gate-abc10a9b2d82](https://medium.com/javascript-scene/setstate-gate-abc10a9b2d82)，之後會再整理一篇文章說明這個問題。

### Key attribute

```jsx
this.state.monsters.map(monster => <h1 key={monster.id}>{monster.name}</h1>)
```

當我們要使用map() function把陣列裡的資訊列出來的時候，react會叫我們把所有的tag都加上key，因為react自動幫我們篩選那些tag有更動那些沒有，透過key找出有更動的tag並且只更新那些部分，避免每一次的小更動卻要重新把所有東西都render一次。

### Props

```jsx
//App.js
<CardList name = "Tony">Happy</CardList>

//card-list.component.jsx
export const CardList = props => {
    return (<div className='card-list'>{props.children}</div>)
}
```

react的第二個核心觀念，當一個components創建時，他會有一個屬性props紀錄傳進來的參數，像上面的例子，傳入name屬性，並且在tag裡面夾入字串，當我們在使用components的時候，props就會把上面兩個屬性記錄下來，tag裡面的東西可以利用props.children來取得，tag上的屬性用key取得即可。

總結state只會活在一個component裡面，他可以往下面的ocmponents傳，但是下面的components是利用props來接收，並且只能向下傳送不能向上。

### When do we break things down into components?

當一個元件可以被重複用很多次獲用在很多地方的時候，就需要獨立成一個components。

### function VS class

要如何決定component要用function還是class，可以先思考他要不要有state，如果他只是一個不需要互動的component，那可以利用function的方式來建造，比較易讀也比較簡單，反之如果component比較複雜且互動性比較高的話，就可以先使用class來建造。

> 延伸：要如何知道state放在哪一個component，可以將所有component的關聯圖建立起來，如果component的state只會影響到自己children的UI，那state可以放在自身身上，如果會影響到parent or sibling，就要往上層放，直到state可以涵蓋所有被影響的component才能停止向上。
> 

### "this" in class

當我們在寫component裡面要使用state的時候，我們會寫成this.state，這個this指的是component這個class，又因為這個class繼承React裡面的component class，所以今天我們在呼叫像是constructor或render的時候，可以使用this.state來找到這個變數。如果今天是在class裡面自訂一個方法並且在裡面使用this的話，因為React.Component沒有自動綁定this，所以自訂的函式會視this為undefined，以下有兩種方法改善：

```jsx
//自己綁定
constructor(){
    super();
    this.foo = this.foo.bind(this);
}

//利用arrow function的特性
//this的指向會依照語彙範疇來設定
//因為函式在class裡面宣告所以會指向此class
foo = e => {
   this.setState({searchField:e.target.value})
}

```

### 原始的React

creat react app這個package幫我們建立了很棒的開發環境，但如果把jsx和babel抽掉只留下react的話，就會像以下範例一樣用呼叫API的方式來撰寫。

```jsx
const App = () => {
	//利用createElement來建立react dom的物件，第一個參數是HTML tag，第二個是attributes，第三個是children的內容
	//這邊的children就是再塞了一個h1 tag
	return React.createElement(
		'div',
		{},
		React.createElement('h1' , {} , "React IS RENDERED!!!")
	)
}

//這個方式也可以寫成模組化，如果有多個children就用array表示
const Person = props => {
	return React.createElement('div' , {} , [
		React.createElement('h1' , {} , props,name)
		React.createElement('p' , {} , props,occupation)
	])
}

//第一個參數除了寫Html tag外還可以寫react component
const App = () => {
	return React.createElement('div',{},[
		React.createElement(Person , {name:"tony" , occupation:"developer"})
		React.createElement(Person , {name:"tang" , occupation:"cooker"})
	])
}
```

### View → Actions → State(→View→...)

在React中，DOM總共有兩種，virtulDOM和actualDOM，網頁上顯示的是actualDOM，當使用者與網頁做出互動，改變state的時候，virtulDOM會與actualDOM做比對，看是哪個DOM被更改，並且給render更改後的component。資料的流向是單向的，Debug的時候就可以知道是哪個環節出問題，如果UI有問題就可以找State，如果互動有問題就要檢查View等等。

### Lifecycle methods

![Untitled](/blog/2021/12/06/React-Tutorial-02/lifeCycle.png)
