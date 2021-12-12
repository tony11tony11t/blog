---
title: "[Master the Coding Interview]Graphs"
image: /blog/2021/12/12/Master_The_Coding-DS-Graphs/thumbnail.png
date: 2021-12-12 17:33:14
tags: 
- Data structure
categories: 
- Master the Coding Interview
description: 由N個nodes和M條links組合而成的資料結構就叫做Graphs，Linked list是一種Graph，Tree也算是一種Graphs。...
---

**<font color=#FF6600>本篇為Master the Coding Interview教學影片筆記文</font>**

由N個nodes和M條links組合而成的資料結構就叫做Graphs，Linked list是一種Graph，Tree也算是一種Graphs。

Graphs分成有向和無向的，undirected像是facebook的好友功能，當你和一個人成為好友的時候，你們是互相為好友，directed像是instagram的追蹤功能，當你追蹤一個帳號的時候，是單方面的，他不一定要追蹤你。

Graphs可以分為有權重和無權重的，當圖的link都有權重的時候，我們就可以來算最短路徑的，像是google map的最佳路徑功能。

Graphs可以分為Cyclic和Acyclic，有環和無環的圖形。

Graphs的資料可以利用以下3種方法來記錄：

```jsx
//Edge List
const graph = [[0,2] , [2,3] , [2,1] , [1,3]];

//Adjacent List
const graph = [[2] , [2,3] , [0,1,3] , [1,2]];

//Adjacent Matrix
const graph = [
	[0,0,1,0],
	[0,0,1,1],
	[1,1,0,1],
	[0,1,1,0],
]
```

## Implement an Graphs

```jsx
class Graph { 
    constructor() { 
      this.numberOfNodes = 0;
      this.adjacentList = {
      }; 
    } 
    addVertex(node)  { 
        this.numberOfNodes++;
        this.adjacentList[node] = []
    } 
    addEdge(node1, node2) { 
        this.adjacentList[node1].push(node2)
        this.adjacentList[node2].push(node1)
    } 
    showConnections() { 
      const allNodes = Object.keys(this.adjacentList); 
      for (let node of allNodes) { 
        let nodeConnections = this.adjacentList[node]; 
        let connections = ""; 
        let vertex;
        for (vertex of nodeConnections) {
          connections += vertex + " ";
        } 
        console.log(node + "-->" + connections); 
      } 
  } 
  } 
  
  const myGraph = new Graph();
  myGraph.addVertex('0');
  myGraph.addVertex('1');
  myGraph.addVertex('2');
  myGraph.addVertex('3');
  myGraph.addVertex('4');
  myGraph.addVertex('5');
  myGraph.addVertex('6');
  myGraph.addEdge('3', '1'); 
  myGraph.addEdge('3', '4'); 
  myGraph.addEdge('4', '2'); 
  myGraph.addEdge('4', '5'); 
  myGraph.addEdge('1', '2'); 
  myGraph.addEdge('1', '0'); 
  myGraph.addEdge('0', '2'); 
  myGraph.addEdge('6', '5');
  
  myGraph.showConnections(); 
  //Answer:
  // 0-->1 2 
  // 1-->3 2 0 
  // 2-->4 1 0 
  // 3-->1 4 
  // 4-->3 2 5 
  // 5-->4 6 
  // 6-->5
```

## When can use arry?

| 優點 | 缺點 |
| --- | --- |
| Relationships | Scaling is hard |