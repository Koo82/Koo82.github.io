---
title: "Python random seed, state"
---


Python의 random function은 기본 내장 함수로써, random한 수를 생성하기 위해 사용한다.
그런데 random 함수는 진정한 의미에서의 random이 아니다.  

원문에서는 이렇게 표현한다.  

"Module implements pseudo-random number generators for various distribution."  

즉 random은 의도적으로 숫자를 재생성 해낼수 있다는 말이다. 이를 확인하기 위해 seed 함수와 state에 대해서 알아보자.

- random.seed()  
랜덤 숫자 생성기를 초기화 시킨다. 초기화 숫자로 같은 숫자를 넣게 될 경우, 같이 숫자를 생성 시킬 수 있다. 아래와 같이 같은 seed를 주게 되면 계속 같은 값을 얻을 수 있다.

```
In [91]: a = list([1,2,3,4,5])

In [92]: random.seed(4)

In [93]: random.choice(a)
Out[93]: 2

In [94]: random.seed(4)

In [95]: random.choice(a)
Out[95]: 2
```

- random.getstate()  
random generator 의 현재 내부 상태를 캡쳐한 객체를 리턴

- random.setstate()  
random generator 의 특정한 내부 상태를 재현(복원)

```
In [96]: random.seed(4)

In [97]: random.choice(a)
Out[97]: 2

In [98]: random.choice(a)
Out[98]: 3

In [99]: random.choice(a)
Out[99]: 1

In [100]: random.choice(a)
Out[100]: 4

In [102]: b= random.getstate()

In [103]: random.choice(a)
Out[103]: 4

In [104]: random.choice(a)
Out[104]: 2

In [105]: random.choice(a)
Out[105]: 1

In [106]: random.choice(a)
Out[106]: 1

In [107]: random.setstate(b)

In [108]: random.choice(a)
Out[108]: 4

In [109]: random.choice(a)
Out[109]: 2

In [110]: random.choice(a)
Out[110]: 1

In [111]: random.choice(a)
Out[111]: 1
```

위와 같이 random sequence 의 랜덤 내부 상태를 캡쳐해서 저장하면 특정한 상태에서의 값을 그대로 재현해 낼 수 있다. 자세한 내용은 공식 홈페이지를 참고하자.


Python 공식 문서 [random](https://docs.python.org/3/library/random.html)  
