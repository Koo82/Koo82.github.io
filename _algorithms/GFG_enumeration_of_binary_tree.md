---
title: "[Geeksforgeeks] Enumeration of Binary Trees"
---

How to enumerate binary trees with labeled and unlabeled [enumeration of binary trees](https://www.geeksforgeeks.org/enumeration-of-binary-trees/)

n개의 노드를 가지는 Unlabeled binary tree의 갯수를 구하기 위해서는 결론적으로 n'th Catalan Number를 구하면 된다. 문제는 n'th Catalan Number가 무엇이고 왜 이 숫자가 Unlabeled binary tree의 갯수를 나타내냐는 것이다.

기본적인 아이디어는 Unlabeled binary tree의 갯수를 왼쪽과 오른쪽으로 구분해서 배치하는 경우의 수를 합해주는 것이다.

n = 0 -> count(0) = 1 (비어 있는 트리도 하나의 경우로 본다.)  
n = 1 -> count(1) = 1  
n = 2 -> count(2) = 2  
n = 3 -> count(2) * count(0) + count(1) * count(1) + count(0) * count(2)  = 5  
    (트리의 왼쪽 노드 갯수 count * 트리의 오른쪽 노드 갯수 count 형식)  
n = 4 -> count(3) * count(0) + count(2) * count(1) + count(1) * count(2) + count(0) * count(3) = 14  

위의 형식을 보면 자연스럽게 recursive하게 풀 수 있겠다는 생각이 든다. 이를 정리해 보면 다음과 같다.

```
memo = [0] * (n+1)
def catalan(n):
    # base case 0, 1
    if n<= 1:
        return 1
    # memoization loading
    if memo[n] != 0:
        return memo[n]

    result = 0
    for i in range(n):
        result += catalan(i) * catalan(n-i-1)
    memo[n] = result
    return result
```

이를 수식으로 정리하면 다음과 같다.

catalan_number(n) = (2n)! / (n+1)!n!

특이할 만한 사항은 binary_search_tree의 경우는 숫서가 존재하기 때문에 unlabeled binary tree와 같은 갯수를 가진다는 것이다.  
그렇다면 labeled bianry tree의 갯수는?  
n개의 노드를 순열로 표현할 수 있기 때문에 n!을 곱해주면 된다.

catalan_number(n) * n!
