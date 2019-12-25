---
layout: post
title: "[Rasa] Open Source를 이용해 날씨 챗봇 만들기 - 1"
date: 2019-12-23 00:00:00 +0300
comments: true
img: python.png
visible: 1
description: Rasa open source를 이용해 간단한 날씨 챗봇을 만들어 봅시다.
categories: Chatbot
tags: [Chatbot, Rasa]
---



# [Rasa] Open source를 이용해 날씨 챗봇 만들기 - 1

### Rasa?

[Rasa](https://rasa.com)는 파이썬 기반의 대화형 인공지능 프레임워크입니다.



### Rasa X?

Rasa X는 Rasa open source를 통한 챗봇 개발을 위한 UI입니다. 

Rasa X를 통해 챗봇을 더 쉽게 만들 수 있습니다.



### 설치하기

Rasa 를 설치하기 위해선 [Python(3.6 버전 또는 3.7 버전)](https://www.python.org/downloads/)이 설치되어 있어야 합니다.

파이썬이 없다면 [아나콘다](https://www.anaconda.com/distribution/#download-section)를 설치하는 것이 좋습니다.

또 [Microsoft Visual C++ 14.0](https://visualstudio.microsoft.com/ko/downloads/) 가 설치되어 있어야 합니다.

명령 프롬프트에서 아래의 명령어로 Rasa와 Rasa X를 설치합니다.

```shell
pip install rasa-x --extra-index-url https://pypi.rasa.com/simple
```

Rasa는 파이썬의 여러 라이브러리들을 사용하기 때문에 모두 설치하는데 꽤 오랜시간이 걸립니다.

텍스트 에디터는 Visual Studio Code를 사용합니다.



### 시작하기

새로운 Rasa Project를 생성하기 위해서 프로젝트를 생성할 폴더에서 아래와 같은 명령어를 통해 새 프로젝트를 생성합니다.

```shell
rasa init
```

이 때, git bash를 사용할 경우 unicode encoding 오류가 납니다.
anaconda prompt나 윈도우 cmd를 사용하시면 해결이 됩니다.(정확한 이유는 모름...)


