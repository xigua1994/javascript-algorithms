## 链表

>链表是一种递归的数据结构，它或者为空(null)，或者是指向一个节点(node)的引用，该节点
含有一个泛型的元素和一个指向另一个链表的引用。

### 设计一个基于对象的单链表

在面向对象编程中，用一个嵌套类来定义节点的抽象数据结构类型。
```angularjs
function Node(element){
  this.element = element;
  this.next = null;
}
```

```angularjs
function LinkedList(){
  this.head = new Node("head")
}
LinkedList.prototype.find = function(item){
  var currNode = this.head;
  while(currNode.element != item){
    currNode = currNode.next;
  }
  return currNode;
}
LinkedList.prototype.insert = function(newEle,item){
  var newNode = new Node(newEle);
  var current = this.find(item);
  newNode.next = current.next;
  current.next = newNode;
}
LinkedList.prototype.findPrevious = function(item){
  var currNode = this.head;
  while(!(currNode.next == null) && (currNode.next.element != item)){
    currNode = currNode.next;
  }
  return currNode;
}
LinkedList.prototype.remove = function(item){
  var prevNode = this.findPrevious(item)
  if(!(prevNode.next == null)){
    prevNode.next = prevNode.next.next;
  }
}
LinkedList.prototype.advance = function(n){
  while( (n>0) && !(this.currentNode.next == null)){
    this.currentNode = this.currentNode.next;
    n --;
  }
}
LinkedList.prototype.back = function(n){
  while( (n>0) && !(this.currentNode.element == "head")){
    this.currentNode = this.currentNode.previous;
    n --;
  }
}
```

### 双向链表

双向链表与单链表的区别就在于双向链表有一个指向前一个指针，所以就要将其节点的数据结构改下如下：

```
function Node(element){
  this.element = element;
  this.previous = null;
  this.next = null;
}
```

```
function doubleLinkedList(){
  this.head = new Node("head");
}
```

### 循环链表

其和单向链表相比，其头节点的```next```属性指向它本身，即```head.next = head```

循环链表的数据结构如下：

```
function LList(){
  this.head = new Node("head");
  this.head.next = this.head;
}
LList.prototype.display = function(){

}
```

由于上面的文字解释太过干涩，所以下面来两道真题帮助理解链表这种数据结构。

合并两个有序链表，将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
//listNode的定义
function ListNode(val){
  this.val = val;
  this.next = null;
}
```

答案：
```
var mergeTwoLists = function(l1, l2) {
  let tempNode = new ListNode(0);
  let current = tempNode;
  while(l1 != null && l2 != null){
    if(l1.val < l2.val){
      current.next = l1;
      l1 = l1.next;
    }else{
      current.next = l2;
      l2 = l2.next;
    }
    current = current.next;
  }
  if(l1 == null){
    current.next = l2;
  }else{
    current.next = l1;
  }
  return tempNode.next;
};
```






给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。
```
示例：
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.
//listNode的定义
function ListNode(val){
  this.val = val;
  this.next = null;
}

var removeNthFromEnd = function(head,n){
  //to do
  return null;
}
```
下面是解题思路：

* 先获取链表的长度len；

* 将第len-n个节点的next设置为第len-n-1个节点的next，这就完成删除倒数第n个节点的操作，当然需要注意的是极端条件（即列表中只有一个节点或需要删除头节点的情况），这时就需要设置一个位于列表头部的临时节点。

答案：

```
var removeNthFromEnd = function(head,n){
  let node = head,
    len = 0,
    tempNode = new ListNode(0);
  tempNode.next = head;
  
  while(node){
    len ++;
    node = node.next;
  }

  len -= n;
  node = tempNode;
  while(len){
    len --;
    node = node.next;
  }
  node.next = node.next.next;
  return tempNode.next;
}
```