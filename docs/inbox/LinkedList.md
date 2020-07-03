# 链表

链表是由一组节点组成的集合。每个节点都使用一个对象的引用指向它的后继。指向另一 个节点的引用叫做链。

数组元素靠它们的位置进行引用，链表元素则是靠相互之间的关系进行引用。

## 1. 单向链表的实现

```javascript
function Node(element) {
  this.element = element;
  this.next = null;
}

function LList() {
  this.head = new Node("head");
  this.find = find;
  this.insert = insert;
  this.display = display;
  this.findPrevious = findPrevious;
  this.remove = remove;
}

function remove(item) {
  var prevNode = this.findPrevious(item);
  if (!(prevNode.text == null)) {
    prevNode.next = prevNode.next.next;
  }
}

function findPrevious(item) {
  var currNode = this.head;
  while(!(currNode.next == null) && (currNode.next.element != item)) {
    currNode = currNode.next;
  }
  return currNode;
}

function display() {
  var currNode = this.head;
  while(!(currNode.next == null)) {
    print(currNode.next.element);
    currNode = currNode.next;
  }
}

function find(item) {
  var currNode = this.head;
  while (currNode.element != item) {
    currNode = currNode.next;
  }
  return currNode;
}

function insert(newElement, item) {
  var newNode = new Node(newElement);
  var current = this.find(item);
  newNode.next = current.next;
  current.next = newNode;
}

var cities = new LList();
cities.insert("Conway", "head");
cities.insert("Russellville", "Conway");
cities.insert("Carlisle", "Russellville");
cities.insert("Alma", "Carlisle");
cities.display();
console.log();
cities.remove('Carlisle');
cities.display();
```

### 1.1 反转单向列表

该题目来自 [LeetCode](https://link.juejin.im/?target=https%3A%2F%2Fleetcode.com%2Fproblems%2Freverse-linked-list%2Fdescription%2F)，题目需要将一个单向链表反转。思路很简单，使用三个变量分别表示当前节点和当前节点的前后节点，虽然这题很简单，但是却是一道面试常考题

以下是实现该算法的代码

```javascript
var reverseList = function(head) {
  // 判断下变量边界问题
  if (!head || !head.next) return head
  // 初始设置为空，因为第一个节点反转后就是尾部，尾部节点指向null
  let pre = null
  let current = head
  let next
  // 判断当前节点是否为空
  // 不为空就先获取当前节点的下一个节点
  // 然后把当前的节点的 next 设为上一个节点
  // 然后把 current 设为下一个节点，pre 设为当前节点
  while(current) {
    next = current.next
    current.next = pre
    pre = current
    current = next
  }
  return pre
}
```