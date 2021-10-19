---
title: "[Leetcode] Build Binary Tree with in-order and post-order"
---

Construct Binary Tree from Inorder and Postorder Traversal [Build binary tree](https://leetcode.com/explore/learn/card/data-structure-tree/133/conclusion/942/)

![Binary_Tree](/assets/images/Binary_Build.bmp)

in-order, post-order traversal list를 이용해서 binary tree를 build하는 내용은 처음 생각하기 너무 어려웠다. 그래서 Geeksforgeeks 사이트[BuildBinaryTree](https://www.geeksforgeeks.org/construct-a-binary-tree-from-postorder-and-inorder/) 를 참고했다.

* Keypoint:  
1) post-order traversal 결과 맨 마지막 원소는 root node다.  
2) in-order traversal의 root 노드 좌, 우의 요소들은 각각 left subtree, right subtree를 형성한다.  
3) recursive하게 tree를 구성하는데, root - right node -> left node 순으로 tree를 재건설한다. (post-order의 역순인걸 눈치 챘는가?)  
4) post-order의 역순으로 값을 대입하되, subtree의 범위를 결정하기 위해 start, end index를 재귀함수에 전달한다.  
5) in-order list에서 root의 위치를 도출하기 위해 for문을 돌리는 것보다 hash table(dictionary mathing)을 이용하는 것이 큰 속도 향상을 불러온다.


```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:

        self.inorder = inorder
        self.postorder = postorder
        self.index = len(inorder) -1
        self.inorder_map = {val:idx for idx, val in enumerate(inorder)}

        return self.buildTreeSource(0, len(inorder) -1)

    def buildTreeSource(self, start, end):
        # base
        if start > end:
            return None

        # print(self.index)
        node_val = self.postorder[self.index]
        self.index -= 1

        node = TreeNode(node_val)

        if start == end:
            return node

        root_pos = self.inorder_map[node_val]
        # print("root_pos: ", root_pos)

        node.right = self.buildTreeSource(root_pos+1, end)
        node.left = self.buildTreeSource(start, root_pos-1)

        return node


```
