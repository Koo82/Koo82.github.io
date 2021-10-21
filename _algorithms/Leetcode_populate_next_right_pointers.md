---
title: "[Leetcode] Populating Next Right Pointers in Each Node"
---

Populating Next Right Pointers in Each Node [binary tree algo.](https://leetcode.com/explore/learn/card/data-structure-tree/133/conclusion/994/)

![Binary_Tree](/assets/images/Populate_right_next_tree.bmp)

Binary tree의 같은 레벨에 존재하는 노드를 왼쪽에서 부터 오른쪽으로 노드 포인터로 연결하는 문제.
Perfect binary tree이기 때문에, 레벨 단위를 생각해서 iterative하게 stack에 집어넣고 푸는 문제를 생각해 보았다. (deque를 이용하는 게 더 간단할 수도...)  
coding을 하고 다른 사람이 풀이한 내용을 비교해 보니, recursive하게 푼 방법이 훨씬 빠르고 간결해서 좀 놀랐다.

* Keypoint:  
1) iterative하게 풀이할 경우는 level을 고려해서 같은 레벨로 인식되면 다음 노드를 이전 노드와 연결해 주는 방식으로 구현  
2) level은 1부터 시작  
3) recursive하게 풀이할 경우는 부모 노드의 입장에서 자식 노드의 연결을 생각해서 구현하는 방식으로 더 간단하게 풀이할 수 있다.  
4) left 원소의 next는 right로 바로 연결, 부모 node의 next가 존재할 경우 pnode.right.next를 pnode.next.left로 연결  
5) parents node레벨에서 next가 존재할 경우 pnode.right.next 를 pnode.next.left로 연결하는 것이 핵심  

* Iterative coding  

```
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
class Solution:
    def connect(self, root: 'Node') -> 'Node':

        # complex time 130ms
        queue = []
        queue.append(root)
        level = 1
        count = 0

        if root == None:
            return root

        while queue:
            node = queue.pop(0)
            count += 1
            # print(count)
            if count == (2 ** level -1):
                level += 1
            else:
                node.next = queue[0]

            if node.left != None:
                queue.append(node.left)
                queue.append(node.right)

        return root

```

* Recursive coding

```
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
class Solution:
    def connect(self, root: 'Node') -> 'Node':    
        # base case
        if not root or not root.left or not root.right:
            return root

        root.left.next = root.right

        if root.next:
            root.right.next = root.next.left

        self.connect(root.left)
        self.connect(root.right)

        return root
```
