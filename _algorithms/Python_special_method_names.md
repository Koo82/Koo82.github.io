---
title: "Python Special method names"
image:
  path: ../assets/images/python_image.bmp
  thumbnail: ../assets/images/python_image.bmp
  caption: "Photo from [Python](https://www.python.org/)"
---


Python의 클래스는 특별한 구문으로 작동하는 방식을 구현할 수 있다.  
(산술 연산, 부분 인자 확인, 슬라이싱 등등.)  

연산을 새롭게 정의하거나 연산자 오버로딩을 통해서 구현이 가능하다. 예를 들어보면 아래와 같이 우리가 흔히 생각하는 인덱싱 x[i]의 경우, Complier 입장에서 보면 이것은 type(x).\__getitem__(x, i)와 대략적으로 동등하다고 볼 수 있다. 즉 새로운 클래스를 정의하거나, 기존에 존재하는 방법에 나만의 특별한 함수를 만들고 싶다면 아래와 같은 'Special method name'을 사용하여 구현할 수 있다.

- 'basic customization' methods  
object.\__str__(): str(object), format(), print() 함수에 의해 호출되며, 객체의 프린트 표시 가능한 문자열 객체를 계산하는데 사용.

- 'rich comparison' methods (같다, 작다 등의 비교)  
object.\__lt__() : x < y 호출 x.\__lt__(y)  
object.\__le__() : x <= y 호출 x.\__le__(y)  
object.\__eq__() : x == y 호출 x.\__eq__(y)  
object.\__ne__() : x != y 호출 x.\__ne__(y)  
object.\__gt__() : x > y 호출 x.\__gt__(y)  
object.\__ge__() : x >= y 호출 x.\__ge__(y)  

- 'binary arthmetic operation' methods (더하기, 곱하기, 나누기 등등..)  
object.\__add__(self, other): +  
object.\__sub__(self, other): -  
object.\__mul__(self, other): *  
object.\__matmul__(self, other): @  
object.\__truediv__(self, other): /  
object.\__floordiv__(self, other): //  
object.\__mod__(self, other): %  
object.\__divmod__(self, other): divmod()  
object.\__pow__(self, other[, modulo]): pow(), **  
object.\__lshift__(self, other): <<  
object.\__rshift__(self, other): >>  
object.\__and__(self, other): &  
object.\__xor__(self, other): ^  
object.\__or__(self, other): |  

- 'container type' methods  
object.\__len__() : len() 작동시 호출
object.\__getitem__() : self[key] 호출시 호출
object.\__setitem__() : self[key] 할당시 호출

Python 공식 문서 [Special method names](https://docs.python.org/3/reference/datamodel.html#object.__add)  

Example Code:
```
class ComplexN:
    def __init__(self, real, img):
        self.real = real
        self.img = img

    def __add__(self, c_num):
        return ComplexN(self.real+c_num.real, self.img+c_num.img)

    def __sub__(self, c_num):
        return ComplexN(self.real-c_num.real, self.img-c_num.img)

    def __mul__(self, num):
        if type(num) == ComplexN:
            return ComplexN(self.real*num.real-self.img*num.img, self.real*num.img + self.img * num.real)
        elif type(num) == int:
            return ComplexN(self.real*num, self.img*num)
    def __len__(self):
        return (self.real ** 2 + self.img ** 2)

    def __str__(self):
        return f'{self.real} + {self.img}j'

    def __abs__(self):
        return self.__len__()**0.5

    def __eq__(self, cn):
        return self.real == cn.real and self.img == cn.img

    def __ne__(self, cn):
        return not (self.real == cn.real and self.img == cn.img)

a = ComplexN(3,4)
b = ComplexN(5,7)
print(type(a))
print(a)
print(a + b)
print(a - b)
print(a * b)
print(a * 4)
print(len(b))
print(abs(a))
print(a == b)
print(a != b)

```
* result:  
    <class '__main__.ComplexN'>  
    3 + 4j  
    8 + 11j  
    -2 + -3j  
    -13 + 41j  
    12 + 16j  
    74  
    5.0  
    False  
    True
