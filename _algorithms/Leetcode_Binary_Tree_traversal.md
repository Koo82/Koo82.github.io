---
title: "[Leetcode] Binary Tree Traversal"
---

Binary tree를 순회하는 방법 [Binary Tree Traversal](https://leetcode.com/explore/learn/card/data-structure-tree/134/traverse-a-tree/992/)

Binary Tree를 순회하는 방법은 노드를 방문하는 순서에 따라 pre-order, in-order, post-order 총 3가지가 있고, coding style은 recursive 또는 iterative하게 작성할 수 있다. 아래의 코드를 확인해 보면 알겠지만, recursive하게 coding을 진행할 때는 노드 방문 순서만 변경해 주면 되기 때문에 코드를 이해하기가 직관적이고 짜기도 비교적 수월하다. 하지만, iterative하게 짜려면 순서에 대해서 약간은 더 고민해 줘야 한다.

1) Pre-order Traversal:  
Root -> left -> right 의 순서로 tree를 순회한다.  

```
# Definition for a binary tree node.
# class Node:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        return self.bfs(root)

    def dfs(self, node):
        result = []

        if node is None:
            return []
        else:
            result.extend([node.val])
            if node.left is not None:
                result.extend(self.dfs(node.left))
            if node.right is not None:
                result.extend(self.dfs(node.right))

        return result

    def bfs(self, node):
        #pre-order
        result = []

        current = node
        stack = []
        while True:
            if current is not None:
                stack.append(current)
                result.append(current.val)
                current = current.left
            elif stack:
                current = stack.pop()
                # result.append(current.val)
                current = current.right
            else:
                break
        return result
```

* key point:  
   - recursive method: root -> left -> right 순서로 depth first search로 순회 알고리즘 작성  
   - iterative method: 현재 node가 None이 아니면 stack에 추가하고 current node값을 결과 리스트에 저장, 현재 node에 left node를 대입  
                현재 node가 None이면 스택에서 node를 꺼내 current node에 대입 후, root노드 값은 이미 저장되어 있으므로 현재 노드에 right node를 대입  

2) In-order Traversal:  
left -> root -> right 의 순서로 tree를 순회한다.  

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        return self.bfs(root)

    def dfs(self, node):
        result = []

        if node is None:
            return []
        else:
            if node.left is not None:
                result.extend(self.dfs(node.left))
            result.extend([node.val])
            if node.right is not None:
                result.extend(self.dfs(node.right))

        return result

    def bfs(self, node):
        #in-order
        result = []

        current = node
        stack = []
        while True:
            if current is not None:
                stack.append(current)
                current = current.left
            elif stack:
                current = stack.pop()
                result.append(current.val)
                current = current.right
            else:
                break
        return result

```

* key point:  
   - recursive method: left -> root -> right 순서로 depth first search로 순회 알고리즘 작성  
   - iterative method: 현재 node가 None이 아니면 stack에 추가하고, 현재 node에 left node를 대입  
                현재 node가 None이면 스택에서 node를 꺼내 current node에 대입 후, current node값을 결과 리스트에 저장하고 현재 노드에 right node를 대입  
                Pre-order와 다른 점은 current node가 None이 아닌 상황에서 값을 바로 결과 리스트에 저장하지 않고, left node로 먼저 진행한다는 점이 다른 것이 특징

3) Post-order Traversal:  
left -> right -> root 의 순서로 tree를 순회한다.  
node를 delete할 때 post-order sequence process 를 사용하고, mathmatical expression에서도 광범위하게 사용함.

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        return self.dfs(root)

    def dfs(self, node):
        result = []

        if node is None:
            return []
        else:
            if node.left is not None:
                result.extend(self.dfs(node.left))
            if node.right is not None:
                result.extend(self.dfs(node.right))
            result.extend([node.val])

        return result

    def bfs(self, node):
        #post-order
        result = []

        current = node
        stack = []
        while True:
            if current is not None:
                stack.append(current)
                if current.right is not None:
                    stack.append(current.right)
                current = current.left
            elif stack:
                current = stack.pop()
                result.append(current.val)
            else:
                break
        return result

```

* key point:  
   - recursive method: left -> right -> root 순서로 depth first search로 순회 알고리즘 작성  
   - iterative method: 현재 node가 None이 아니면 stack에 추가하고, current.right가 None이 아니라면 right node를 스택에 먼저 추가하고, 현재 node에 left node를 대입  
                현재 node가 None이면 스택에서 node를 꺼내 current node에 대입 후, current node값을 결과 리스트에 저장한다.
                Pre-order와 다른 점은 current node가 None이 아닌 상황에서 값을 바로 결과 리스트에 저장하지 않고, right node를 먼저 추가하고 난후 left node를 스택에 저장한다는 것이 특징 (스택의 특징 상 나중에 추가한 노드가 먼저 나오게 됨)
