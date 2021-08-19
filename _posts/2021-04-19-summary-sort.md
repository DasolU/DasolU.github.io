---
layout: post
title: Summary for Sort Algorithm
subtitle: 정렬 알고리즘 풀이를 위한 필수 함수 총정리
categories: CodingTest
tags: [CodingTest, Summary]
---
🌟코딩테스트에서 **정렬** 문제를 풀기 위해 꼭 필요한 함수 총 정리!!!!!🌟

코테 전에 **정렬 알고리즘 필수 요약** 보고 들어가세요!

계속 업데이트 합니다. 

## 정렬 방법
### List 정렬

* list 원본을 변경하거나 정렬한 list를 return하는 두 가지 방법이 있으며 두 방법 모두 key와 reverse 모두 사용 가능하다.

* 정렬의 default는 오름차순이다.

#### List 원본 변경

예시) 첫 번째 key(x[1])를 기준 오름차순 정렬한 뒤, 두 번째 key(-x[0])를 기준으로 내림차순 정렬

list.sort(key=lambda x: (x[1], -x[0]), reverse=True)



이 방법은 반환 값이 없으며 (Return None) 원본을 바꾸는 방법입니다.

#### 새로운 list 반환

sorted_list = sorted(list, key=lambda x: x[1]**2, reverse=True)

#### 예시: 문자열 정렬

[프로그래머스 가장 큰 수][1] 문제를 풀기 위해서 **"문자열 비교 연산 방법"** 에 대한 이해가 필요합니다.

* String(문자열) 비교 연산은 첫번째 인덱스를 비교하고 같으면 다음 인덱스를 비교한다.

  

즉, 문자열 비교 연산이 첫 번째 원소 비교-> 두 번째 원소 비교... 순서로 이루어지기 때문에,

**입력된 숫자의 자릿수가 서로 다를 경우 문자열 곱셈을 통해 가장 짧은 문자열의 자리수를 늘려줍니다.**

```python
numbers = [30,3,34]
strings = list(map(str,numbers))

# 입력된 숫자의 자릿수가 서로 다를 경우
# key에 문자열 곱셈 이용하여 문자열의 길이를 맞춰준다.
# key=lambda x: x*2 예시)'1'*2 -> '11'
strings_sorted = sorted(strings,key=lambda x: x*2, reverse=True) 
print(strings_sorted) 
#->['34', '3', '30']

integer_sorted = sorted(numbers,key=lambda x: x*2, reverse=True)
print(integer_sorted) 
#->[34, 30, 3]
```

### Array 정렬

Import numpy as np

np.sort(array)

* reverse(거꾸로): np.sort()[::-1]

## List 덧셈

list = [1,2,3]

### 다른 리스트 내부의 원소 추가

#### list+list

list+[4,5] 

-> [1,2,3,4,5]

#### list.extend(리스트)

⚠️ extend(리스트) ⭕️ extend(원소) ❌ : extend 함수는 input에 리스트만 넣을 수 있다

list.extend([4,5])

-> [1,2,3,4,5]

### 다른 리스트 전체 추가

#### list.append(리스트, 원소)

🌟 append(리스트) ⭕️ append(원소) ⭕️ : append 함수는 input에 리스트와 원소 모두 넣을 수 있다.

🌟 따라서 [stack][2], [queue][3]를 구현하고 원소를 추가할 때는 list.append(node)를 사용하면 된다.

⚠️ 하지만 list를 사용하면 시간 복잡도가 증가하므로  **`collections.deque`** 를 사용하도록 하자!

([deque 관련 글][4]을 참고하세요)

list.append([4,5])

-> [1,2,3,[4,5]]

list.append(4)

-> [1,2,3,4]

### String 덧셈

문자열(string)으로 구성된 list의 모든 원소들을 더할 때.

```python
''.join(['a','b','c'])
#-> 'abc'
'_'.join(['a','b','c'])
#-> 'a_b_c'
```

## Zip과 Enumerate
길이가 같은 두 list의 각 원소를 짝지어 데리고 다니고 싶을 때.

특히, for loop 사용하며 해당 원소의 index(인덱스)를 사용하고 싶을 때 아주 유용.

```python
singer = ['zico', '적재', '크러쉬']
genre = ['hip-pop', 'indi', 'R&B']

for idx, (s, g) in enumerate(zip(siger, genre)):
  print(idx, s, g)
```
## Map

List 안에 모든 원소들의 자료형을 동시에 바꾸고 싶을 때. For문 말고 이거 쓰세요!

```python
numbers = [1,2,3]
numbers = list(map(str, numbers))
print(numbers)
# -> ['1','2','3']
```



[1]: https://programmers.co.kr/learn/courses/30/parts/12198
[2]: https://dasolu.github.io/basic/2021/04/15/data-structure-stack.html
[3]: https://dasolu.github.io/algorithm/2021/04/20/BFS.html

[4]: https://dasolu.github.io/codingtest/2021/04/21/list-pop-vs-collections-deque.html