## 堆和栈

### 列表

堆和栈都是一种列表，只不过其内部形式不同，所以我们可以先理解列表的抽象数据类型的定义。列表是一种
非常常见的数据结构，下面我们来实现一个列表类。

```angularjs
function List(){
  this.listSize = 0;
  this.pos = 0;
  this.dataStore = [];
}
//给list添加元素
List.prototype.append = function(element){
  this.dataStore[this.listSize++] = element;
}
//从列表中删除元素
List.prototype.remove = function(element){
  var foundAt = this.find(element);
  if (foundAt > -1) {
    this.dataStore.splice(foundAt,1);
    --this.listSize;
    return true;
  }
  return false;
}
//从列表中找到某个元素
List.prototype.find = function(element){
  for (var i = 0; i < this.dataStore.length; ++i) {
    if (this.dataStore[i] == element) {
      return i;
    }
  }
  return -1;
}
//返回列表长度
List.prototype.length = function() {
  return this.listSize;
}
//显示列表中的元素，但是返回的是一个数组，而不是一个字符串
List.prototype.toString = function() {
  return this.dataStore;
}
//向列表中插入一个元素
List.prototype.insert = function(element, after) {
  var insertPos = this.find(after);
  if (insertPos > -1) {
    this.dataStore.splice(insertPos+1, 0, element);
    ++this.listSize;
    return true;
  }
  return false;
}
//清空列表中的所有元素
List.prototype.clear = function(element, after) {
  delete this.dataStore;
  this.dataStore = [];
  this.listSize = this.pos = 0;
}
//判断给定值是否在列表中
List.prototype.contains = function(element) {
  for (var i = 0; i < this.dataStore.length; ++i) {
    if (this.dataStore[i] == element) {
      return true;
    }
  }
  return false;
}
//遍历列表
List.prototype.front = function() {
  this.pos = 0;
}
List.prototype.end = function () {
  this.pos = this.listSize-1;
}
List.prototype.prev = function () {
  if (this.pos > 0) {
    --this.pos;
  }
}
List.prototype.next = function () {
  if (this.pos < this.listSize-1) {
    ++this.pos;
  }
}
List.prototype.currPos = function () {
  return this.pos;
}
List.prototype.moveTo = function (position) {
  this.pos = position;
}
List.prototype.getElement = function () {
  return this.dataStore[this.pos];
}
```

list的实现有很多种，这里只是参考了[数据结构与算法JavaScript](https://item.jd.com/11523857.html)，要想更深入了解list，可以参考[list更加具体的介绍以及实现](http://www.collectionsjs.com/list)

### 栈

栈是一种基于后进先出（LIFO）策略的特殊列表，其内部的元素只能通过栈顶去访问，对栈的操作主要是入栈（push)和出栈(pop)，
当然还有peek(返回栈顶元素)，length(返回其有多少元素).

这里采用数组实现其数据结构：

```angularjs
function Stack(){
  this.dataStore = [];
  this.top = 0;
}
Stack.prototype.push = function(element){
  this.dataStore[this.top++] = element;
}
Stack.prototype.pop = function(){
  return this.dataStore[--this.top]
}
Stack.prototype.peek = function(){
  return this.dataStore[this.top--];
}
Stack.prototype.clear = function() {
  this.top = 0;
}
Stack.prototype.length = function() {
  return this.top;
}

```
在实际应用中，前端可以使用栈来实现判断回文。

```angularjs
function isPalindrome(word){
  var s = new Stack();
  for(var i=0;i<word.length;i++){
    s.push(word[i]);
  }
  var rword = "";
  while(s.length()>0){
    rword += s.pop();
  }
  if(word == rword){
    return true;
  }else{
    return false;
  }
}
```



## 队列

队列跟排队一样，排在最前面的总是先办业务（在队首删除元素），后面来的只能排在最后面
（在队尾插入元素），所以其是一种先进先出的数据结构。

以数组来实现的队列代码如下所示：
```angularjs
function Queue(){
  this.dataStore = [];
}
Queue.prototype.enqueue = function(element){
  this.dataStore.push(element)
}
Queue.prototype.dequeue = function(element){
  return this.dataStore.shift();
}
Queue.prototype.front = function(element){
  return this.dataStore[0];
}
Queue.prototype.back = function(element){
  return this.dataStore[this.dataStore.length-1];
}
Queue.prototype.dequeue = function(element){
  return this.dataStore.shift();
}
Queue.prototype.toString = function(element){
  var retStr = "";
  for (var i = 0; i < this.dataStore.length; ++i) {
    retStr += this.dataStore[i] + "\n";
  }
  return retStr;
}
Queue.prototype.empty = function(element){
  if(this.dataStore.length == 0){
    return true;
  }else{
    return false;
  }
}
```
