# Java LinkList

链表（Linked list）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的地址。

链表可分为单向链表和双向链表。

![img](https://www.runoob.com/wp-content/uploads/2020/06/ArrayList-1-768x406-1.png)



一个单向链表包含两个值: 当前节点的值和一个指向下一个节点的链接。

![img](https://www.runoob.com/wp-content/uploads/2020/06/408px-Singly-linked-list.svg_.png)

一个双向链表有三个整数值: 数值、向后的节点链接、向前的节点链接。

![img](https://www.runoob.com/wp-content/uploads/2020/06/610px-Doubly-linked-list.svg_.png)

与 ArrayList 相比，LinkedList 的增加和删除对操作效率更高，而查找和修改的操作效率较低。

**以下情况使用 ArrayList :**

- 频繁访问列表中的某一个元素。
- 只需要在列表末尾进行添加和删除元素操作。

**以下情况使用 LinkedList :**

- 你需要通过循环迭代来访问列表中的某些元素。
- 需要频繁的在列表开头、中间、末尾等位置进行添加和删除元素操作。