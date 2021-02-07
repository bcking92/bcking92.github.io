---
layout: post
title: "[python] 내가 제일 좋아하는 조합 알고리즘(바이너리 조합)"
date: 2021-02-07 00:00:00 +0300
comments: true
description: 이진 조합 알고리즘
img: python.png 
visible: 1
categories: python
tags: [algoritm]
---

조합 알고리즘을 구하는 다양한 방법이 있지만 내가 제일 좋아하는 알고리즘은 이진연산을 이용한 조합알고리즘이다.

이진연산을 이용한 조합 알고리즘을 처음 봤을 때 "와 개쩐다" 고 생각했던 그 기분이 잊혀지지 않는다.

```python

def combination(arr, num):
    """
    @param arr 리스트
    @param num 몇개를 뽑을지
    @returns 경우의 수의 배열을 리턴
    """
    result = []
    for i in range(2 ** len(arr)):
        temp = []
        for j in range(len(arr)):
            if i & (1 << j):
                temp.append(arr[j])
        if len(temp) == num:
            result.append(temp[:])
    return result
```

킹왕짱!