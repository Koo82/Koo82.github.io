---
title: "[Baekjoon] BJ_1365 (LIS/Binary Search Tree)"
---

백준 1074번 문제 [Baekjoon 1365](https://www.acmicpc.net/problem/1365)

최장 증가 부분 수열(Longest Increasing Subsequences) 문제는 전형적인 동적 계획법의 문제다.  
동적 계획법으로 풀기 위해서는 최적 부분 구조가 성립함을 확인해야 한다.
아래 코드를 확인해 보면 어떻게 동작하는지 알 수 있다.

* O(n2) Code:  

```
import sys
from math import inf
import bisect
DEBUG=True


def log(message):
    if debug:
        print(message)


def LIS(start):
    # memoization의 값이 존재하면 그 값을 그대로 return
    if cache[start] != -1:
        return cache[start]
    # 항상 arr[start]는 존재하기 때문에 최소값은 1
    ret = 1
    for next in range(start+1, len(arr)):
        # start가 0인 경우는 초기 스타트의 경우로 첫 번째 부터 마지막까지 모두 수행해 줘야함
        # 이 때문에 최종값이 1만큼 커지는 효과를 가지게 되므로 최종 값에서 이를 제외해야 함
        if (start == 0) | (arr[start] < arr[next]):
            ret = max(ret, LIS(next)+1)
    return ret

N = int(sys.stdin.readline())
arr = [-inf] + list(map(int, sys.stdin.readline().split()))
cache = [-1] * (N+1)

sys.stdout.write(f'{N - (LIS(0)-1)}')
```

다만, 이 문제의 경우는 input의 갯수가 10만이기 때문에 O(n2) 알고리즘으로는 시간초과를 유발하므로 O(nlogn) 알고리즘으로 풀어야 한다.

* key point:  
1) 동작 원리는 LIS_output_array를 만들고 input_array의 값과 LIS_output_array[-1]의 값을 비교하여 input_array의 값이 크면 그대로 append하고 그렇지 않으면 LIS_output_array에서 input_array의 값이 같은 처음의 위치(lower_bound)를 찾아서 그 위치에 넣어주는 원리다.  
2) 위치를 찾기 위해서는 binary search tree를 이용하며 이를 위한 python 모듈은 bisect library의 bisect_left를 사용한다.  
3) 결과적으로 얻어지는 LIS_output_array의 값 자체는 올바른 값이 아니며, 길이만 유효하다. 값 자체를 얻기위해서는 추가적인 구현이 필요하다.  

* O(nlog(n)) Code:  

```
import sys
from math import inf
import bisect
DEBUG=True


def log(message):
    if debug:
        print(message)


def LIS2():
    # 초기화, input의 첫번째 원소를 LIS 결과 arr에 넣어주고 시작
    ans_arr = [arr[0]]
    for item in arr[1:]:
        # arr의 해당 요소의 값이 LIS_결과 arr의 맨 마지막보다 크다면 그대로 삽입
        if item > ans_arr[-1]:
            ans_arr.append(item)
        # 그렇지 않다면 해당 위치를 binary_search를 통해서 위치를 정해서 삽입
        else:
            loc = bisect.bisect_left(ans_arr, item)
            ans_arr[loc] = item
    return len(ans_arr)


N = int(sys.stdin.readline())
arr = list(map(int, sys.stdin.readline().split()))
cache = [-1] * N
ans_arr = []

sys.stdout.write(f'{N - (LIS2())}')



```
