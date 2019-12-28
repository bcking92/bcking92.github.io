---
layout: post
title: "[Rasa]Open Source를 이용해 날씨 챗봇 만들기-1"
date: 2019-12-23 00:00:00 +0300
comments: true
img: Rasa/Rasa-logo.png
visible: 1
description: Rasa open source를 이용해 간단한 날씨 챗봇을 만들어 봅시다.
categories: Chatbot
tags: [Chatbot, Rasa]
sitemap:
---

### Rasa?

[Rasa](https://rasa.com)는 파이썬 기반의 대화형 인공지능 프레임워크입니다.



### Rasa X?

Rasa X는 Rasa open source를 통한 챗봇 개발을 위한 UI입니다. 

Rasa X를 통해 챗봇을 더 쉽게 만들 수 있습니다.



Rasa를 이용해서 날씨 정보를 알려주는 날씨 챗봇을 만들어 봅시다.



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
anaconda prompt나 윈도우 cmd를 사용하시면 해결이 됩니다(정확한 이유는 모르겠습니다... 아시는 분들은 댓글 달아주시면 감사하겠습니다)



### 구조 살펴보기

프로젝트를 생성했으면 바로 기본으로 생성되어 있는 moodbot과 대화해 볼 수 있습니다. 챗봇을 더 학습시키기 전에 RASA가 어떻게 작동하는지 먼저 알아봅시다. 라사는 NLU와 Core로 나누어져 있습니다.

- NLU는 Natural language understanding, 즉 유저의 메세지를 이해하는 부분입니다. NLU에서는 유저의 메세지를 분석해 Intent와 entity를 찾아냅니다. Intent는 문장의 의도를 말하고 entity는 문장에 있는 핵심 키워드입니다. 
  예를 들어 유저가 '오늘 서울 날씨좀 알려줘' 라고 말한다면 이 문장의

  intent 는 '날씨 질문' 이 되고
  entity는 '날짜' = '오늘', '위치' = '서울' 이 됩니다.

  지금 무슨 말인지 몰라도 하다보면 점점 이해가 됩니다.

- Core는 dialogue management를 하는 부분입니다. 한 마디로 유저에게 어떤 응답을 돌려주어야 할지 결정합니다. 이 결정은 학습된 대화 스토리 라인을 기반으로 이루어 집니다.

더 구체적으로 Rasa에서 메세지를 받고 메세지를 내보내는 과정은 아래 그림과 같습니다. 

<img src="https://rasa.com/docs/rasa/_images/rasa-message-processing.png">

1. 사용자로 부터 받은 메세지는 Interpreter를 통해 Python dictionary형태(Object형태)로 변환됩니다. 이 object에는 original text, intent, entity들이 포함되어 있고 이 부분은 Rasa NLU가 담당합니다.
2. Tracker는 대화기록을 저장하는 Object입니다. 1번에서 변환된 object형태의 정보를 tracker에 저장 합니다.
3. tracker가 가지고 있는 현재 정보를 policy에게 넘기면
4. Policy는 다음에 어떤 Action(response)을 할지 선택합니다.
5. 선택된 action은 다시 대화기록을 저장하는 tracker에 저장하면서
6. 유저에게도 response를 내어줍니다.



다음 글에서 실제로 코드를 통해 학습을 시켜 보겠습니다.