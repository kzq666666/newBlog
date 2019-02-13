---
title: "数据结构"
date: 2018-12-26T09:20:11+08:00
showDate: true
draft: false
tags: ["dataStructure", "structure"]
---

感谢邱老师这一个学期的数据结构课的教导，让我了解到什么是数据结构和其重要性，以及相关的算法和实现。
<br>这是一篇关于数据结构的复习。

### 基本概念

1.程序 = 算法 + 数据结构 &emsp; ------ Nicklaus Wirth
<br>一个程序就是通过具体的某种计算机语言将算法进行实现

2.数据结构：相互之间存在一种或多种特定关系的数据元素的集合
具体什么是数据结构，包含下面三个部分=>

- 逻辑关系：线性关系、非线性关系
- 存储方式：顺序存储、链接存储、散列存储
  <br>（存储存的除了要存数据，还要存它们之间的关系，这一点是邱老师在刚上数据结构讲这些基本概念的时候特别强调的，我印象挺深的）
- 运算集合：查找和排序（插入=>直接法，二分法、交换=>冒泡排序，快速排序、选择=>堆排序）

  3.算法：对特定问题求解步骤的一种描述。
  <br>一个算法还具有下列 5 个重要特性

- 有穷性&emsp;一个算法必须在执行有穷步之后结束，但一个程序则可以无穷，比如说无限死循环
- 确定性&emsp;算法的每一条指令必须有确切的含义
- 可行性&emsp;一个算法是能行的
- 输入&emsp;一个算法有零个或多个输入
- 输出&emsp;一个算法有一个或多个输出

<br>一个好的算法需要达到的目标

- 正确性
- 可读性
- 健壮性&emsp;当输入数据非法时，算法也能做出反应或进行处理，即要可以处理一些特殊和极端情况
- 效率和低存储量需求&emsp;时间复杂度低，算法执行时间短。满足需求的同时尽可能使用低的存储量消耗

  4.时间复杂度：&nbsp;算法中基本操作重复执行的次数是问题规模 n 的某个函数 f(n)，即
  T(n) = O(f(n))
  <br>5.空间复杂度：&nbsp;算法所需存储空间的量度，即 S(n)=O(f(n))

### 线性表

1.逻辑关系：线性关系/结构

- 存在唯一一个被称作"第一个"的数据元素
- 存在唯一一个被称作"最后一个"的数据元素
- 除第一个之外，集合中每个数据元素均只有一个前驱
- 除最后一个之外，集合中每个数据元素均只有一个后继

总的来说就是只有第一个元素有直接后继，没有前驱，只有最后一个元素有直接前驱，没有后继，在这两个元素之间的元素既有一个直接前驱也有一个直接后继

<br>2.存储方式和运算
<br>（1）顺序存储：用一组地址连续的存储单元依此存储线性表中的数据元素

```js
// 在JavaScript中，数组就是一种隐式的存储关系

// 初始化数组
function listInit() {
  return new Array();
}

// 插入=>第i-1个位置和第i个位置之间插入元素,i从1开始
function listInsert(list, i, data) {
  let len = list.length;
  if (i < 1 || i >= len + 1) {
    throw new Error("i的位置有误");
  }
  for (let j = len - 1; j >= i - 1; j--) {
    list[j + 1] = list[j];
  }
  list[i - 1] = data;
}

// 删除=>删除第i个位置的元素
function listDelete(list, i) {
  let len = list.length;
  if (i < 1 || i > len) {
    throw new Error("i的位置有误");
  }
  for (let j = i - 1; j <= len - 1; j++) {
    list[j] = list[j + 1];
  }
  // 切记不能用len--，因为是原始值，len改变并不会改变list.length
  list.length--;
}
```

（2）链式存储：用一组任意的存储单元存储线性表的数据元素（这组存储单元可以是连续的，也可以是不连续的）

- 一个结点包含两个域，一个是数据域，一个是指针域，此链表的每个结点中只包含一个指针域，故又称为线性链表或单链表

```js
// 单链表
function LinkListNode(data) {
  this.data = data;
  this.next = null;
}

var headNode = new LinkListNode(null);
var len = 0;
// 获取第i个元素
function getElem(i) {
  var p = headNode.next;
  var j = 1;
  while (p && j < i) {
    p = p.next;
    j++;
  }
  return p ? p.data : null;
}

// 插入，在第i个位置之前插入元素e
function linkListInsert(LinkListNode, i, e) {
  let newNode = new LinkListNode(e);
  var j = 1;
  p = headNode;
  if (i < 1 || i > len + 1) {
    return new Error("i的范围有误");
  }
  while (j <= i - 1 && p.next) {
    p = p.next;
    j++;
  }
  newNode.next = p.next;
  p.next = newNode;
  len++;
}
// 删除，删除第i个位置的结点
function linkListDelete(i) {
  var j = 1;
  pre = headNode;
  p = pre.next;
  while (j < i && p.next) {
    pre = p;
    p = pre.next;
    j++;
  }
  if (j == i) {
    return new Error("超出链表范围");
  }
  pre.next = p.next;
  len--;
}
```

- 双向链表：结点有两个指针域，其一指向直接后继，另一指向直接前驱

```js
// 双链表
function DuListNode(data, prior, next) {
  this.data = data || null;
  this.prior = prior || null;
  this.next = next || null;
}
var headNode = new DuListNode();

// 获取第i个位置的结点（i从1开始）
function getDuList(i) {
  var p = headNode;
  var j = 1;
  while (j <= i && p.next) {
    p = p.next;
    j++;
  }
  return p.data ? p.data : null;
}

// 获取表长
function getDuListLen() {
  var j = 0;
  var p = headNode;
  while (p.next) {
    p = p.next;
    j++;
  }
  return j;
}

// 在带头结点的双链表的第i个位置之前插入元素e
function insertDuList(i, e) {
  if (i < 1 || i > getDuListLen() + 1) {
    return new Error(
      "i的范围应该不小于1且不大于表长加1,即len>=1 && len<=" +
        (getDuListLen() + 1)
    );
  }
  var j = 1;
  var p = headNode;
  var newNode = new DuListNode(e);
  while (p.next && j < i) {
    p = p.next;
    j++;
  }
  if (p.next) {
    newNode.next = p.next;
    p.next.prior = newNode;
    p.next = newNode;
    newNode.prior = p;
  } else {
    p.next = newNode;
    newNode.prior = p;
  }
}

// 删除第i个位置的结点
function delDuListNode(i) {
  var j = 1;
  var p = headNode;
  if (getDuList(i) !== null) {
    while (j <= i) {
      p = p.next;
      j++;
    }
  } else {
    return new Error("不存在第" + i + "个结点");
  }
  p.prior.next = p.next;
}

// 打印每个结点(包含头结点)
function printDuList() {
  p = headNode;
  while (p || (p && !p.prior && !p.next)) {
    console.log(p);
    p = p.next;
  }
}
```

- 循环链表：表中最后一个结点的指针域指向头结点，整个链表形成一个环，从表中任一结点出发均可找到表中其他结点
  <br>其操作和单链表和双链表的操作差不多，只不过算法的循环条件变成了 p.next 是否为头指针或者 p 是否为头指针

### 栈和队列

#### 栈

1.&nbsp;逻辑结构：运算受限的线性表（限定仅在表尾进行插入或删除操作的线性表）

- FILO（First In Last Out）先进后出
- LIFO（Last In First Out）后进先出
- 栈顶：表尾端
- 栈底：表头端

  2.&nbsp;存储和运算:

* 顺序栈

```js
// 栈
function Stack() {
  // 数据
  this.data = [];
  // 栈顶
  this.top = 0;
  // 栈底
  this.base = 0;
  // 入栈
  this.entryStack = entryStack;
  // 出栈
  this.exitStack = exitStack;
  // 返回栈顶元素
  this.getTop = getTop;
  // 长度
  this.length = getLength;
}

function entryStack(e) {
  this.data[this.top++] = e;
}

function exitStack() {
  return this.data[--this.top];
}

function getTop() {
  return this.data[top - 1];
}

function getLength() {
  return this.top - this.base;
}

// 利用栈进行数制转换
var s = new Stack();
var n = prompt("请输入数字");
var d = prompt("请输入要转换的进制");
console.log(n, d);
while (n) {
  s.entryStack(n % d);
  n = parseInt(n / d);
}
while (s.length()) {
  console.log(s.exitStack());
}

// 利用栈计算一个数的阶乘
var s = new Stack();
var n = prompt("请输入你要计算的数：");
var result = 1;
while (n > 1) {
  s.entryStack(n--);
}
while (s.length()) {
  result *= s.exitStack();
}
console.log(result);
```

- 链栈

<br>栈的链式表示
<img src="/linkStack.png" style="height:60%">

#### 队列

1.逻辑结构

- FIFO（first in first out）
- LILO（last in last out）
- 一端进行插入，另一端删除元素
- 允许插入的一端叫做队尾（rear）
- 允许删除的一端叫做队头 （front）

  2.存储和运算

（1） 顺序存储

```js
// 队列
function Queue() {
  // 数据
  this.data = [];
  // 队头
  this.front = 0;
  // 队尾
  this.rear = 0;
  // 获取队头
  this.getFront = getFront;
  // 获取队尾元素
  this.getRear = getRear;
  // 入队
  this.entryQueue = entryQueue;
  // 出队
  this.exitQueue = exitQueue;
  // 获取队列长度
  this.length = getLength;
  // 队列是否为空
  this.isQueueEmpty = isQueueEmpty;
}

function getFront() {
  return this.data[this.front];
}

function getRear() {
  return this.data[this.rear - 1];
}

function entryQueue(e) {
  this.data[this.rear++] = e;
}

function exitQueue() {
  return this.data[this.front++];
}

function getLength() {
  return this.rear - this.front;
}

function isQueueEmpty() {
  return this.front == this.rear ? true : false;
}
```

（2） 链式存储

```js
// 单链队列（不引入头结点）
function linkQueue() {
  this.front = null;
  this.rear = null;
  this.length = 0;
}

linkQueue.prototype.qNode = function(e) {
  this.data = e;
  this.next = null;
};

// 判断队是否为空
linkQueue.prototype.isQueueEmpty = function() {
  return this.front == this.rear && this.front == null ? true : false;
};

// 入队
linkQueue.prototype.entryQueue = function(e) {
  var newNode = new this.qNode(e);
  if (this.length == 0) {
    this.front = this.rear = newNode;
  } else {
    this.rear.next = newNode;
    this.rear = newNode;
  }
  this.length++;
  return true;
};

// 出队
linkQueue.prototype.exitQueue = function() {
  if (!this.isQueueEmpty()) {
    var p = this.front;
    this.front = this.front.next;
    // 当队列最后一个元素出队后，队列的尾指针也丢失，则需要从新复制
    if (this.rear == p) {
      this.rear = this.front;
    }
    this.length--;
    return p;
  } else {
    return new Error("当前队列为空");
  }
};

// 打印当前队列
linkQueue.prototype.printQueue = function() {
  var str = "";
  var p = this.front;
  while (p) {
    str += p.data + " ";
    p = p.next;
  }
  console.log("当前队列为：" + str);
};
```

（3）循环存储
设顺序存储队列用一维数组 q[m]表示，其中 m 为队列中元素个数，队列中元素在向量中的下标从 0 到 m-1。
<br>
在出队的时候，front 头指针向右移动，如果队尾指针指向 m-1，队列中仍有空闲单元，所以队列不是真的满了，
这时候入队操作，就会出现假溢现象。为了避免多余的空闲单元浪费（假溢出现），则引入循环队列，仅仅用 front==rear 无法判断队列空间是空还是满，有两种处理方法，一种是另外设置一个标志位来区别队空和队满的区别，另一种是少用一个元素空间，约定以“头指针在队尾指针的下一位置上”作为队列呈“满”状态的标志，这里是第二种

```js
// 循环队列
function CQueue(maxLength) {
  this.maxLength = maxLength;
  this.data = new Array(maxLength);
  // 初始化的时候头指针和尾指针都为0，每入队，rear指针加一，指向下一个位置
  this.front = 0;
  this.rear = 0;
  this.length = 0;

  // 获取队列长度
  this.getLength = function() {
    return (this.rear - this.front + this.maxLength) % this.maxLength;
  };

  // 入队
  this.entryQueue = function(e) {
    if ((this.rear + 1) % this.maxLength == this.front) {
      return new Error("队列已满");
    }
    this.data[this.rear] = e;
    this.rear = (this.rear + 1) % this.maxLength;
    this.length++;
  };

  // 出队
  this.exitQueue = function() {
    if (this.front == this.rear) {
      return new Error("队列为空");
    }
    var p = this.data[this.front];
    this.front = (this.front + 1) % this.maxLength;
    return p;
  };

  // 打印当前队列元素
  this.printQueue = function() {
    var str = "";
    var p = this.front;
    while (p % this.maxLength < this.rear) {
      str += this.data[p] + " ";
      p = (p + 1) % this.maxLength;
    }
    console.log(str);
  };
}
```

### 树和二叉树

1.逻辑结构：

- 树：n（n > 0）个节点的有限集
- 二叉数：每个结点的度最多为二（最多有两个子树）

  2.存储和运算（二叉树）

- 顺序存储：用一组地址连续的存储单元依次自上而下，自左向右存储完全二叉数的结点元素，以‘0’表示不存在此结点。
- 链式存储

```js
// 创建二叉树（这里实现二叉排序树）
// 二叉排序树（Binary Sort Tree）BST：左子树上结点的值小于ta的根结点的值，而右子树上结点的值大于ta的根结点的值，没有键值相等的节点
function BinaryTree() {
  // 根节点
  this.root = null;

  // 节点
  this.Node = function(data) {
    this.data = data;
    // 左指针
    this.left = null;
    // 右指针
    this.right = null;
  };

  // 插入
  this.insert = function(data) {
    let newNode = new this.Node(data);
    if (this.root === null) {
      this.root = newNode;
    } else {
      this.insertNode(this.root, newNode);
    }
  };
  this.insertNode = function(root, newNode) {
    if (newNode.data < root.data) {
      if (root.left === null) {
        root.left = newNode;
      } else {
        this.insertNode(root.left, newNode);
      }
    } else {
      if (root.right === null) {
        root.right = newNode;
      } else {
        this.insertNode(root.right, newNode);
      }
    }
  };

  // 先序遍历
  this.preOrderTraversal = function(callback) {
    this.preOrderTraversalNode(this.root, callback);
  };
  this.preOrderTraversalNode = function(node, callback) {
    if (node !== null) {
      callback(node.data);
      this.preOrderTraversalNode(node.left, callback);
      this.preOrderTraversalNode(node.right, callback);
    }
  };

  // 中序遍历（中序遍历二叉排序树得到的就是按从小到大的顺序访问所有节点）
  this.inOrderTraversal = function(callback) {
    this.inOrderTraversalNode(this.root, callback);
  };
  this.inOrderTraversalNode = function(node, callback) {
    if (node !== null) {
      this.inOrderTraversalNode(node.left, callback);
      callback(node.data);
      this.inOrderTraversalNode(node.right, callback);
    }
  };

  // 后序遍历
  this.postOrderTraversal = function(callback) {
    this.postOrderTraversalNode(this.root, callback);
  };
  this.postOrderTraversalNode = function(node, callback) {
    if (node !== null) {
      this.postOrderTraversalNode(node.left, callback);
      this.postOrderTraversalNode(node.right, callback);
      callback(node.data);
    }
  };
  this.printNode = function(value) {
    console.log(value);
  };

  // 获取BST中的最小值
  this.minData = function(){
    let p = this.root;
    while(p && p.left){
      p = p.left;
    }
    return p.data;
  }

  // 获取BST中的最大值
  this.maxData = function(){
    let p = this.root;
    while(p && p.right){
      p = p.right;
    }
    return p.data;
  }

  // 查询一个节点
  this.findNode = function(key,node=this.root){
    if(node !== null){
      if(key < node.key){
        this.findNode(key,node.left);
      }else if(key > node.key){
        this.findNode(key, node.right);
      }else{
        return node;
      }
    }else{
      return null;
    }
  }
  // 移除一个节点
  this.removeNode = function(key){
    let p = root;
    while(p.data)
    if(node==null){
      return null;
    }

  }
}
```

3.二叉树的性质

- 在二叉数的第 i 层上至多有 2^(i-1)个结点（i>=1）
- 深度（树中结点 最大的层次）为 k 的二叉树至多有 2^k-1 个结点
  <br>2^0+2^1+...+2^k-1 = 2^0(1-2^k)/1-2 = 2^k - 1
- 对任何一颗二叉数 T，如果度为 0 的结点树为 n0，度为 2 的结点数为 n2，则 n2 = n0 + 1
- 满二叉树：一颗深度为 k 且有 2^k-1 个结点的二叉数称为满二叉树
- 完全二叉树：深度为 k，有 n 个结点的二叉树，当且仅当其每一个结点都与深度为 k 的满二叉树中编号从 1 至 n 的结点一一对应
