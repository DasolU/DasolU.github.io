---
layout: post
title: Data Structure Stack
subtitle: Stack이란 단어는 난생 처음이라구요?
categories: Basic
tags: [Basic, Data Structure]
---
제 인생 첫 코딩 테스트를 보기 3일전에 Stack이란 단어를 처음 봤습니다.  
구글링 덕분에 코딩 테스트 전에 개념을 파악할 수 있었지만  알고리즘 구현은 생소하고, queue(큐)와 헷갈립니다.  

## 정의
Stack은 list의 **한쪽 끝으로만 데이터의 삽입&삭제가 가능한** data structure(자료 구조)입니다.  
Stack은 data structure 중 선형 구조(linear Structure)에 속하며, 포스트 잇을 한 장씩 쌓아올리는 것처럼 데이터를 쌓습니다.  
따라서 데이터를 삭제할 때, 나중에 들어온 데이터를 먼저 삭제하는 방식(Last In First Out)으로 데이터를 처리합니다.  

## 호출 스택의 중요성
컴퓨터는 호출 스택이라고 불리는 스택을 사용합니다.  

```python
def add(i):
   print(i+100)

def multiply(i):
   print(i*100)

def main(i):
   multiply(i)
   add(i)
```
위의 예시처럼 컴퓨터가 main 함수를 실행하는 경우를 생각해볼게요.    
우리가 main(1)이라고 명령하면 컴퓨터에서는 어떤 일이 벌어질까요?  
1. 먼저 multiply 함수 호출을 위해서 메모리가 할당되고 숫자 1이 메모리에 저장됩니다.  
2. 다음으로 add 함수가 호출되며 새로운 메모리가 할당되며 숫자 1이 메모리에 저장됩니다.   
**중요한 점은**, 이때 두 번째 메모리가 첫 번째 메모리의 **위**에 올려지기 때문에    
add 함수가 먼저 실행되어 1*100 계산 결과를 반환하고 나서야 
멈춰있던 첫 번째 함수인 multiply가 실행된다는 점입니다.  


이처럼 여러 개의 함수를 호출할 때 나중에 호출한 함수의 변수를 가장 위에 저장하는 스택을 호출 스택이라 정의합니다.  
