---
layout: post
title: python list 연산의 시간복잡도
subtitle: 시간복잡도를 알고 꼭 필요할 때만 사용하자!
tags: [CodingTest, Efficiency]
categories: CodingTest
---

요즘은 코딩테스트 준비를 위해 솔루션을 여러가지로 작성해보며 계산 시간과 메모리 효율성에 대해서 테스트 해보고 있습니다.

백준을 돌아다니던 와중에 **[자주 틀리는 요인에 대한 글][1]**을 읽으면서, list 자료형 사용시 조심해야겠다고 생각한 부분들이 나와서 반가웠습니다.

또한 제 고민이 헛되지 않았고, [제가 list 자료형에 대해 이해한 내용][3]이 맞다는걸 알게되어서 좋았습니다.

단순히 코딩테스트만을 위한 것이 아니라 비전공자 입장에서 코드 작성시 고려해야하는 점들에 대해서 배우는게 많았습니다.

## 시간 복잡도가 O(n)인 list 연산들

python list의 시간복잡도에 대해 정리된 [링크][2]를 보고 내용을 정리했습니다. 여러분도 한 번 읽어보세요!

* list는 내부적으로 array로 표시된다.
* 따라서 할당한 크기 이상으로 list 크기를 키우거나 줄인다면 모든 원소들을 이동시켜야하므로 O(n)처럼 많은 시간이 소요된다.

### 처음 or 중간에 추가/삭제

* Insert
  * list.pop(0): 처음에 추가하는 경우
  * list.insert(위치, 추가할 요소) 
* Delete Item
  * list.remove(요소)
* Pop intermediate
  * list.pop(중간 위치에 해당하는 index)

### 위치 반환

* list.index(요소)

### 포함된 요소 조사하기

* Iteration
  * x in list

* list.count(요소): 리스트에 포함된 요소 개수 세기
* min(list), max(list)

### 뒤집기

* list[:-1]



## 시간 복잡도가 O(1)인 list 연산들

### 마지막에 추가/삭제

* list.append(요소) : 마지막에 추가
* list.pop(): 마지막에 삭제

### 요소 가저오기

* Get Item

### list길이 확인

* Get Length



## collections.deque와 비교

### 시간 복잡도가 O(n)인 deque 연산들

* remove
* rotate

### 시간 복잡도가 O(1)인 deque 연산들

🌟처음과 끝에 추가/삭제하는 연산 모두 O(1)로 시간 단축이 가능하다‼️

⚠️위에서 소개한 [링크][2]에서도 stack과 queue처럼 양쪽 끝의 요소를 추가/삭제하는 경우, list❌ [collections.deque][4] ⭕️를 사용하라고 권장하고 있습니다.

따라서 stack이나 queue 구현시 반드시 collections.deque를 사용하도록 합시다!!

* deque.appendleft(), deque.append() : 처음과 마지막에 요소 추가
* deque.popleft(), deque.pop() : 처음과 마지막에 요소 제거





[1]: https://www.acmicpc.net/blog/view/70

[2]: https://wiki.python.org/moin/TimeComplexity
[3]: https://dasolu.github.io/basic/2021/04/14/data-structure-array-linked-list.html
[4]: https://dasolu.github.io/codingtest/2021/04/21/list-pop-vs-collections-deque.html