---
title: Tree 문제 재귀적으로 풀기 (Solve Tree Problems Recursively)
---

Tree 문제는 재귀적으로 풀어나갈 떄 코드가 간결해 지는 장점이 있고 tree 자체도 재귀적으로 정의되기 때문에 tree 묹에 재귀를 많이 사용하고 있으며 방법론으로 크게 top-down approach와 bottom-up approach가 있다.

leetcode를 참고하여 작성 [leetcode tree problem](https://leetcode.com/explore/learn/card/data-structure-tree/17/solve-problems-recursively/534/)


* "Top-down" Solution:  
 1. 현재 노드에서 필요한 값을 계산하고 이 값을 자식 노드에 전달하여 최종적인 값을 계산하는 방식  
 2. Considered as a kind of preorder traversal


Example code(C++) of tree maximum depth top-down search:
```
int answer; // don't forget to initialize answer before call maximum_depth
void maximum_depth(TreeNode* root, int depth) {
    # 기저 사례, root == null 이면 stop
    if (!root) {
        return;
    }
    # children 노드가 하나도 없으면 leaf 노드가 되고, depth 값을 update
    if (!root->left && !root->right) {
        answer = max(answer, depth);
    }
    # leaf node가 아닐 경우 왼쪽, 오른쪽으로 재귀 탐색
    maximum_depth(root->left, depth + 1);
    maximum_depth(root->right, depth + 1);
}
```

* "Bottom-up" Solution:  
 1. 재귀적으로 leaf node까지 자식 노드를 탐색하고, 원하는 값을 return하여 부모 노드로 전달해서 root로 올라가며 값을 갱신해 나가는 방식
 2. Considered as a kind of postorder traversal

Example code(C++) of tree maximum depth top-down search:  
```
int maximum_depth(TreeNode* root) {
    # 기저 사례: root가 널이면 0을 반환
    if (!root) {
        return 0;                                 // return 0 for null node
    }

    # children node traversal
    int left_depth = maximum_depth(root->left);
    int right_depth = maximum_depth(root->right);

    # 자식 노드의 값을 바탕으로 depth 갱신
    return max(left_depth, right_depth) + 1;      // return depth of the subtree rooted at root
}
```
