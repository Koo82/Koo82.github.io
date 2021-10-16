---
title: "[Leetcode] Symmetric Tree"
---

Binary Tree 문제 중 [Symmetric Tree](https://leetcode.com/explore/learn/card/data-structure-tree/17/solve-problems-recursively/536/)

Tree의 특성상 Recursively coding 하는 것이 자연스럽다.

* recursive Code:  

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:

        # recursive solution
        def lr_sym(left, right):
            if not left and not right: return True
            if (not left and right) or (left and not right): return False
            if left.val != right.val: return False

            return lr_sym(left.left, right.right) and lr_sym(left.right, right.left)

        if not root: return True
        return lr_sym(root.left, root.right)

```

* key point:  
left, right node를 switching하여 같은 value가 저장되어 있는지 확인하면 되겠다는 생각은 쉽게 도출되었다. 문제는 어떻게 switching 하느냐이다. 다음과 같이 3개의 기저 사례를 생각해 볼 수 있다.  
1) left와 right가 모두 None일 경우 -> Symmetric  
2) left와 right node 중 어느 하나만 None일 경우 -> Asymmetric  
3) left.val와 right.val가 다를 경우 -> Asymmetric  
위의 세가지 경우를 제외하고는 다음 자식 노드로 진행하되 left.left와 right.right를 비교한 결과와 left.right와 right.left를 비교한 결과를 and 처리하면 depth와 관계없이 모든 노드를 비교할 수 있다는 점이 생각하기 어렵다.  

* iterative Code:  

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:

        # iterative solution

        if root is None:
            return True
        stack = [(root.left, root.right)]

        while stack:
            left, right = stack.pop()

            if not left and not right: continue
            if (not left and right) or (left and not right): return False
            if left.val != right.val: return False

            stack.insert(0, (left.left, right.right))
            stack.insert(0, (left.right, right.left))

        return True


```

* key point:  
iterative하게 풀기 위해서는 stack이나 queue를 이용해서 비교에 사용될 left와 right node를 저장해 두었다가 pop을 이용해서 하나씩 처리하며, 저장된 node를 모두 소진할 경우 종료하면 된다.  
stack의 모든 노드를 소진할 때 까지 수행하면 symmetric하다는 것을 주의해서 보자.
