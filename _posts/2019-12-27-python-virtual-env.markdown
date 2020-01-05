---
layout: post
title: "[Python] Python 가상환경 만들기/ alias 등록하기"
date: 2019-12-27 00:00:00 +0300
comments: true
img: python.png
visible: 1
description: Python 가상환경 설정하기기기기
categories: Python
tags: [Python]
---

### 가상환경 사용하기

python 가상환경을 사용하기 위해 python venv 모듈을 이용합니다. (python 3.5이상)

운영체제 : window

cli : git bash

```shell
python -m venv 가상환경설치경로
```

Ex)

1. 가상환경을 설치할 폴더를 만든다.

```shell
$ mkdir ~/python-venv/
```

2. 그 폴더에 가상환경을 설치한다.

```shell
$ python -m venv ~/python-venv/project1
```

3. 가상환경 실행하기

   Python 가상환경을 실행하기 위해서는 Scripts폴더(Window) 또는 bin폴더(리눅스나 MacOS) 안에 있는 activate 파일을 실행시켜주면 됩니다.

```shell
$ source ~/python-venv/project1/Scripts/activate
```



### alias 등록하기

가상환경을 실행할 때 마다 매번 경로로 들어가 실행시킬 수 없으니 alias를 등록합시다.

홈 디렉토리로와서 .bashrc 파일에 alias를 등록해줍니다.

```shell
$ vim .bashrc
```

파일을 생성하고

```.bashrc
alias venv='source ~/python-venv/project1/Scripts/activate'
```

를 입력해 주고 저장합니다.(:wq 엔터)

git bash창을 닫았다 키면 적용이 됩니다.

