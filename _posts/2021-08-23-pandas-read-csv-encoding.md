---
layout: post
title: Pandas pd.read_csv의 engine과 encoding
subtitle: 시간은 째깍째깍 가는데 한글이 깨지고 있다면..?
tags: [CodingTest]
categories: CodingTest
---

데이터 분석가 사전 테스트를 보면 csv파일을 읽어서 데이터 분석을 진행하는 경우가 있습니다.

이럴 때 한글이 깨져서 보이면 당황스럽죠,,

mac에서 jupyter notebook으로 pandas.read_csv()로 파일을 읽어올 때 다음과 같이 하시면 됩니다!

간단하게 해결하세요!

## 입력 예시

```python
df = pd.read_csv('test.csv', engine="python", encoding='cp949')
```

