---
layout: post
title: Mutable & Immutable
subtitle: integer는 불러와야 하는데, list는 안불러와도 그냥 바로 쓸 수 있다!
categories: Basic
tags: [Basic, CodingTest]
---
python 함수 밖에 있는 데이터를 함수 안에 가져와서 연산하고 변화된 데이터를 return해야할 때가 있죠!

python 기초 공부를 마치신 분들은 integer를 함수 안으로 가져오는 방법에 대해서 익숙하실겁니다.

저도 integer에 대해서 공부했기때문에, list를 가져오는 방법도 동일할 것이라고 생각했습니다.

📌 그렇지만 list는 integer와 달리 불러오지 않아도 함수 안에서 바로 사용할 수 있습니다‼️

이유가 뭘까요?

## mutable과 immutable

### 필요성

- python은 객체 지향이므로 **객체 생성 후 변경 여부 관리가 중요**

- 예를 들어 객체를 **함수의 parameter로 전달할 때**, **변경 가능한 객체의 관리가 필요**

### mutable (참조 객체)

변수에 저장되는 것? **객채의 값들이 저장된 참조**

따라서 실제 **값 변경이 가능**

#### 종류

list

dic

set

#### 적용 방법

- 함수의 parameter 또는 변수로 사용하며 원본 값 변경을 하고 싶은 경우?
  - 참조만 복사하는 shallow copy
- 원본 값 변경하지 않으려면?
  - 참조와 전체 값을 복사하여 다른 객체를 생성하는 deep copy

### immutable (값 객체)

변수에 저장되는 것? **객채의 값**

따라서 **변경 불가 (변수 치환은 가능)**



#### 종류

tuple

string

Numbers(숫자형)

## shallow & deep copy

#### shallow

객체의 **주소**를 복사한다.

📌 따라서 복사한 값을 변경하면 원본도 바뀐다.

```python
a = [0,1]
copy_a = a
id(a), id(copy_a)
#->140225591189056 140225591189056

a[1] = 100
print(a, copy_a)
#-> [0, 100] [0, 100]
```



#### deep copy

객체의 값을 복사하여 주소가 다른 새로운 객체를 생성한다.

📌 따라서 복사한 값을 변경해도 원본은 바뀌지 않는다.

```python
a = [0,1]
copy_a = a[:]
print(id(a), id(copy_a))
#->140225331150528 140225591181376
a[1] = 100
print(a, copy_a)
#->[0, 100] [0, 1]
```

```python
import copy
a = [0,1]
copy_a = copy.deepcopy(a)
print(id(a), id(copy_a))
#->140225591154176 140225331159744
a[1] = 100
print(a, copy_a)
#->[0, 100] [0, 1]
```



## 함수 밖의 integer를 함수 안으로 가져오는 방법

두 가지 방법이 알려져 있습니다.

1. **매개변수**로 가져오기
* def function(매개변수)에서 "매개변수" 자리에 integer를 넣어준다.
   
* 함수 안에서 연산한다.
   
* 변화된 integer 값을 (new_integer) return 으로 내보낸다.

```python
integer = 1
def function(integer):
    integer +=1
    return integer
new_integer = function(integer)
print(new_integer)
#-> 2
```

2. **global**을 사용하기
   * 매개변수를 사용하지 않고 global interger로 가져온다.
   * 함수 안에서 연산한다.
   * return으로 변화된 값을 내보낸다.

```python
integer = 1
def function():
    global integer
    integer +=1
    return integer
new_integer = function()
print(new_integer)
#-> 2
```

## 함수 밖의 list를 함수 안으로 가져오는 방법

📌list는 함수 밖 list를 사용할 때, 그냥 바로 사용하면 됩니다.

​	integer와 달리 매개변수로 데러오지 않아도, global로 선언하지 않아도 됩니다‼️

그 이유는? list가 mutable객체이기 때문입니다.

```python
l = [1,2,3]
def function():
    l[0]+=100
    l.pop()
    
function()
print(l)
#-> [101, 2]
```

## list와 integer 함수 매개변수 사용 방법 차이 이유?

📌 integer는 **immutable**(변화 불가능한) 

* integer가 정의되면 특정 주소에 저장되기 때문에, integer를 복사하고 그 값을 연산해도 원본 값은 변화하지 않는다. 
* 따라서 매개변수 또는 global로 직접 값을 가져와서 연산해줘야 원본에 변화를 줄 수 있다.

📌list는 **mutable**(변화 가능한)

* list.pop()과 같은 연산은 list 원본에 변화를 줄 수 있다.
* 따라서 **함수 내부에서 list의 연산은 함수 밖의 list 원본에 영향을 미친다.** 

## Reference

- https://stackoverflow.com/questions/23029727/why-do-list-operations-in-python-operate-outside-of-the-function-scope
- 포스코 AI&BigData 아카데미 수업



