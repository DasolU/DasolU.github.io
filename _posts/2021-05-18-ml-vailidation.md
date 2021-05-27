---
layout: post
title: 모델 성능 평가 지표
subititle: Confusion matrix, Precision, Recall, Accuracy?
categories: AI
tags: [Vailidation]
---
**‘현재 딥러닝을 하고 있다면 축하한다. 딥러닝을 시작하려고 마음을 먹었다면 축하한다. 만약, 세상을 바꾸고 싶다면, 여기가 바로 그런 곳이다’.** -Andrew Ng-

## Confusion matrix

* 정답
  * True를 **True**로 예측: True **Positive**(TP)
  * False를 **False**로 예측: True **Negative**(TN)
* 오답
  * True를 **False**로 예측: False **Negative**(FN) 
  * False를 **True**로 예측: False **Positive**(FP)

## Precision

* 정밀도 = 모델이 True라고 분류한 것 중에서 실제 True인 것의 비율

* **Precision = True Positive/(True Positive+False Positive)**
* Positive 정답률, PPV(Positive Predictive Value)
* 모델이 True라고 분류한 데이터 중에 실제 True인 경우가 많을수록 정밀하다.

## Recall

* 재현율 = 실제 True인 것 중에서 모델이 True라고 예측한 것의 비율
* **Recall = True Positive/(True Positive+False Negative)**
* Sensitivity, hit rate
* 실제 데이터에서 True인 경우 중 모델이 True라고 말한 경우가 많을술록 재현이 잘되었다고 말한다.

### 좋은 모델이란?

* Precision의 관점에서 실제 False이지만 True라고 분류한 경우의 수(**False Positive**)가 적어야 하며,

* 동시에 Recall의 관점에서 실제 True이지만 False로 분류한 경우의 수(**False Negative**)가 적어야 한다.

### Precision과 Recall의 관계

* **False Positive**와 False Negative는 하나가 줄면 하나가 증가하는 trade-off 관계이므로 Precision과 Recall을 동시에 증가시키기 어렵다.

## Accuracy

* 정확도 = 전체 중에서 정답을 맞춘 비율
* **Accuracy = (True Positive + True Negative) / (TP+TN+FP+FN)**
* 사용하는 데이터가 True or False에 bias되었을 때 accuracy는 모델을 평가하는 적절한 지표가 아닐 수 있다.

## Reference

https://sumniya.tistory.com/26

