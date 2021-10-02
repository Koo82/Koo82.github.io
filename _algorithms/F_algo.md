---
title: "BJ 1074"
---

Sort: Divide & Conquer Problem

백준 1074번 문제 [Baekjoon 1074](https://www.acmicpc.net/problem/1074)

* Key_note:  
 1. 전형적인 분할 정복 문제로, 맵을 쪼갤 수 없을때까지 재귀호출을 진행하면서
 counter 변수를 활용해서 순서를 찾아가 주는 것이 핵심.
 맵을 절반으로 줄여나가면서 맵의 위치를 이용해서 counter에 숫자를 더해 주면서 계산  
 2. 기저 사례를 잘 찾아주는 것이 팁이라면 팁이다.


Solution:
```
import sys
DEBUG=True

def log(message):
    if DEBUG:
        print(message)

n, row, col = map(int, sys.stdin.readline().split())
ans = 0
log((n, row, col))

def divide_map(n, row, col):
    if n == 1: # 기저 사례
       return 0
    o_row = o_col = n // 2
    map_size = o_row * o_col
    counter = map_size * (2 * (row // o_row) + col // o_col)
    return counter + divide_map(n//2, row % o_row, col % o_col)

ans = divide_map(2**n, row, col)
sys.stdout.write(f"{ans}")
```
