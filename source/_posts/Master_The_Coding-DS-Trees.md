---
title: "[Master the Coding Interview]Trees"
image: /blog/2021/12/12/Master_The_Coding-DS-Trees/thumbnail.png
date: 2021-12-12 17:31:14
tags: 
- Data structure
categories: 
- Master the Coding Interview
description: 樹狀結構是一種有等級制度的資料結構，很多地方都看得到這種結構，像是HTML DOM，abstract syntax tree等...
---

**<font color=#FF6600>本篇為Master the Coding Interview教學影片筆記文</font>**

樹狀結構是一種有等級制度的資料結構，很多地方都看得到這種結構，像是HTML DOM，abstract syntax tree等。linked list也可以說是一種tree，但他每個node都是單向也只有一個child node。正常的tree中會有一個root，node可以有0~多個child nodes，一切都看要建造的tree的規則，例如red-black tree、binary tree等。

## Binary Trees

二元樹，每個節點都只有left node和right node，Perfect Binary Tree表示節點數量是一直加倍下去的，第一層1個，第二層2個，第三層4個以此類推。Full Binary Tree表示每個node只會有2個或0個child node。Binary search tree是接下來要介紹的資料結構，他的查找、插入和刪除都是O(logN)。

每個node最多只能有兩個child，所以root最多2^0個，第一層最多2^1個，第二層最多2^2個以此類推。由此可以歸納出以下結論：

Level 0 = 2 ^ 0

Level 1= 2 ^ 1

Level 2 = 2 ^ 2

Level 3= 2 ^ 3

N of nodes = 2 ^ h - 1

log node = steps

因為在利用binary search tree查找的時候，利用的是divide and conquer的觀念，每次往下一個節點，都等於把資料再分割，直到找到要的資料為止，假設有7個節點(height = 3)，log 7 就會接近3，所以時間複雜度才會是O(logn)。如果binary search tree是unblance的狀態，所有的時間複雜度就會變成O(n)，像是tree中的linked list。

| 優點 | 缺點 |
| --- | --- |
| better than O(n) | No O(1) operations |
| Flexible Size |  |
| Ordered |  |
|  |  |

## Implement an tree

在面試的時候，通常不會要實作一個tree的結構，只需要了解它的運作方式即可。

```jsx
class Node{
    constructor(value){
        this.left = null
        this.right = null
        this.value = value
    }
}

class BinarySearchTree{
    constructor(){
        this.root = null;
    }
    insert(value){
        let newNode = new Node(value)
        if(!this.root)
            this.root = newNode;
        else{
            let nowNode = this.root
            while(nowNode){
                if(value > nowNode.value){
                    if(!nowNode.right){
                        nowNode.right = newNode;
                        break;
                    }
                    nowNode = nowNode.right
                }else{
                    if(!nowNode.left){
                        nowNode.left = newNode;
                        break;
                    }
                    nowNode = nowNode.left
                }
            }
        }
        return this;
    } 
    lookup(value){
        let nowNode = this.root;
        while(nowNode){
            if(value > nowNode.value){
                nowNode = nowNode.right
            }else if(calue < nowNode.value){
                nowNode = nowNode.left
            }else if(nowNode.value == value){
                return nowNode;
            }
        }
        return null;
    }

    remove(value) {
        if (!this.root) {
            return false;
        }
        let currentNode = this.root;
        let parentNode = null;
        while(currentNode){
            if(value < currentNode.value){
                parentNode = currentNode;
                currentNode = currentNode.left;
            } else if(value > currentNode.value){
                parentNode = currentNode;
                currentNode = currentNode.right;
            } else if (currentNode.value === value) { 
                //Option 1: No right child: 
                if (currentNode.right === null) {
                    if (parentNode === null) {
                        this.root = currentNode.left;
                    } else {
                        
                        //if parent > current value, make current left child a child of parent
                        if(currentNode.value < parentNode.value) {
                        parentNode.left = currentNode.left;
                        
                        //if parent < current value, make left child a right child of parent
                        } else if(currentNode.value > parentNode.value) {
                        parentNode.right = currentNode.left;
                        }
                    }
                
                //Option 2: Right child which doesn't have a left child
                } else if (currentNode.right.left === null) {
                    currentNode.right.left = currentNode.left;
                    if(parentNode === null) {
                        this.root = currentNode.right;
                    } else {
                        
                        //if parent > current, make right child of the left the parent
                        if(currentNode.value < parentNode.value) {
                        parentNode.left = currentNode.right;
                        
                        //if parent < current, make right child a right child of the parent
                        } else if (currentNode.value > parentNode.value) {
                        parentNode.right = currentNode.right;
                        }
                    }
                
                //Option 3: Right child that has a left child
                } else {

                    //find the Right child's left most child
                    let leftmost = currentNode.right.left;
                    let leftmostParent = currentNode.right;
                    while(leftmost.left !== null) {
                        leftmostParent = leftmost;
                        leftmost = leftmost.left;
                    }
                    
                    //Parent's left subtree is now leftmost's right subtree
                    leftmostParent.left = leftmost.right;
                    leftmost.left = currentNode.left;
                    leftmost.right = currentNode.right;

                    if(parentNode === null) {
                        this.root = leftmost;
                    } else {
                        if(currentNode.value < parentNode.value) {
                        parentNode.left = leftmost;
                        } else if(currentNode.value > parentNode.value) {
                        parentNode.right = leftmost;
                        }
                    }
                }
                return true;
            }
        }
  }
}

const tree = new BinarySearchTree();
tree.insert(9);
tree.insert(4);
tree.insert(6);
tree.insert(20);
tree.insert(170);
tree.insert(15);
tree.insert(1);
tree.remove(20);
console.log(JSON.stringify(traverse(tree.root)));
//      9
//  4      20 
//1   6  15  170

function traverse(node){
    const tree = {value : node.value}
    tree.left = node.left === null ? null : traverse(node.left);
    tree.right = node.right === null ? null : traverse(node.right);
    return tree;
}
```

Insert的第一步是先判斷root是否有東西，有東西的話就可以利用while迴圈來找到要insert的點，Lookup也是一樣的方式，透過比較大小來查找目標node。Remove則需要移動node，移動的邏輯首要條件是判斷node的child位置：

1.  如果node沒有右邊的child
    
    表示node以下的child都比較小(全部都在左邊)，可以直接把node砍掉，用child接上，判斷好接在左邊還是右邊即可。
    
2. 如果node有右邊的child，但右邊的child沒有左邊的child
    
    表示node.right中最小的值就是第一個遇到的，所以我們會把node.right當成node的替代品。node左邊的所有node因為都會比node.right的值來的小，可以直接把node.left接到node.right.left。
    
3. 如果node有右邊的child，且右邊的child不管左右都有node。(以下簡稱找到的node為A，要刪除的node為D)
    
    第一步是找到右邊分支中最小的node，用while迴圈來找到右邊分支最左邊的A，A也是最接近D的值，
    
    第二步因為我們要把A直接替換掉D，必須先把A的右邊分支接到A的parent的左邊
    
    第三步就可以替換掉D完成移除D的步驟
    

## AVL Tree & Red Black Tree

這兩種tree不會在這邊多做說明，簡單來說就是一種blance的結構，讓tree的operation的時間複雜度永遠都是O(n)。

**AVL Trees:**

[Animation](https://www.cs.usfca.edu/~galles/visualization/AVLtree.html)

[How it Works](https://medium.com/basecs/the-little-avl-tree-that-could-86a3cae410c7)

**Red Black Trees:**

[Animation](https://www.cs.usfca.edu/~galles/visualization/RedBlack.html)

[How it Works](https://medium.com/basecs/painting-nodes-black-with-red-black-trees-60eacb2be9a5)

You can compare the technical details [between the two here](https://stackoverflow.com/questions/13852870/red-black-tree-over-avl-tree)

## Binary Heaps

一種完全的二元樹，跟binart search tree 不一樣的是它並沒有ordered，insert會從上至下，從左至右的填滿tree，因為沒有ordered，所以lookup的時間複雜度就變成O(n)。實作binary heaps的時候，當我們插入一個node，我們會確保node一定不會大於parent，如果大於parent就會交換順序，直到滿足上述條件為止。如此一來就可以確保root的值在binary heaps裡面最大，當我們在查找max value時，時間複雜度就會是O(1)。如果把priority的概念放入的話，越上面的node表示priority越高，insert的速度就可以更快。

## When can use arry?

| 優點 | 缺點 |
| --- | --- |
| better than O(n) | Slow lookup |
| Flexible Size |  |
| Fast Insert |  |
| Priority |  |