---
title: "[Leetcode] Design Linked List"
---

Design implementation of the linked list [Linked List](https://leetcode.com/explore/learn/card/linked-list/209/singly-linked-list/1290/)

Binary tree 공부 중에 binary tree 내부에 사용되는 Treenode에 관심이 생겨 Linked list design에 도전 했는데 내가 생각했던 것과 다르게 관련 function이 많고 생각하지 못한 것들이 많아 큰 도움이 되었다. 단순히 TreeNode가 아닌 탐색 및 삽입, 삭제에 대한 함수를 구현해야 한다.  

* Keypoint:  
1) Linked list의 시작을 head node로 관리. Head node 자체를 상징적인 node point로 보고 head node 다음에 원하는 Node를 삽입하는 방법이 있을 수 있고, head node와 첫번째 삽입되는 노드를 동일시 하는 방법이 있을 수 있다. 구현의 측면에서는 큰 차이는 없지만, head node자체가 바뀌지 않는 다는 점에서 head node를 따로 관리하는 것이 더 편리할 수 있다.  
2) Linked list의 size를 변수로 가진다는 생각을 하지 못해 처음에는 self.size 변수 없이 구현하였지만, size를 가지고 구현한 코드를 확인해 보니 더 편하게 구현이 가능하다는 생각이 든다. 이 부분에 대한 구현이 더 유리한 측면이 많다.  
3) Linked List 특성상 다음으로 연결되는 node 즉 next를 많이 이용하는데, next가 None인지 아닌지를 확인해줘야 하는 부분을 잘 생각해 줘야 한다.  
4) 얼만큼 순회해야 하는지에 대한 고민이 필요하다.  

* Code (without size, head node == first node)  

```
class nodeLink:
    def __init__(self, val):
        self.val = val
        self.next = None

class MyLinkedList:

    def __init__(self):
        self.head = None

    def get(self, index: int) -> int:
        if self.head is None:
            return -1
        node = self.head
        for _ in range(index):
            node = node.next
            if node is None:
                return -1
        return node.val

    def addAtHead(self, val: int) -> None:
        temp = self.head
        self.head = nodeLink(val)
        self.head.next = temp
        # print(self.head.val, self.head.next)

    def addAtTail(self, val: int) -> None:
        node = self.head
        if node is None:
            self.head = nodeLink(val)
            return None

        while node.next is not None:
            node = node.next
        node.next = nodeLink(val)
        # print(self.head.val, self.head.next.val)

    def addAtIndex(self, index: int, val: int) -> None:
        if index == 0:
            self.addAtHead(val)
            return

        node = self.head

        if node is None:
            return

        for _ in range(index-1):
            node = node.next
            if node is None:
                return None
        if node.next:
            temp = node.next
            node.next = nodeLink(val)
            node.next.next = temp
        else:
            node.next = nodeLink(val)


    def deleteAtIndex(self, index: int) -> None:
        if index == 0:
            self.head = self.head.next
            return None

        node = self.head
        for _ in range(index-1):
            node = node.next
            if node is None:
                return None
        if node.next is None:
            return None
        if node.next.next:
            node.next = node.next.next
        else:
            node.next = None

```

* Code (with size, head node != first node)  

```
# size introduce part one. Need to analyze
class Node:
    def __init__(self, val = None):
        self.val = val
        self.next = None

class MyLinkedList:

    def __init__(self):
        self.size = 0
        # val = 0 인 head node, 상징적으로 사용
        self.head = Node(0)


    def get(self, index: int) -> int:
        # index out_of_range situation
        if index < 0 or index >= self.size:
            return -1
        curr = self.head
        for _ in range(index +1):
            curr = curr.next

        return curr.val

    def addAtHead(self, val: int) -> None:
        self.addAtIndex(0, val)

    def addAtTail(self, val: int) -> None:
        self.addAtIndex(self.size, val)

    def addAtIndex(self, index: int, val: int) -> None:
        if index > self.size:
            return
        if index < 0:
            index = 0
        # size add part
        self.size += 1

        prev = self.head
        to_add = Node(val)
        for _ in range(index):
            prev = prev.next

        to_add.next = prev.next
        prev.next = to_add


    def deleteAtIndex(self, index: int) -> None:
        if index >= self.size or index < 0:
            return
        # size subtraction part
        self.size -= 1
        curr = self.head
        for _ in range(index):
            curr = curr.next

        curr.next = curr.next.next


```
