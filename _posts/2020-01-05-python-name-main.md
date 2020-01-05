---
layout: post
title: "[Python] if __name__ == '__main__': ?? 이게 뭘까"
date: 2019-1-05 00:00:00 +0300
comments: true
img: python.png
visible: 1
description: if __name__ == '__main__' 이거 대체 뭐냐고~
categories: Python
tags: [Python]
---

Python을 사용하다 보면 이런 코드를 많이 볼 수 있습니다.

```python
if __name__ == '__main__':
```

이 때,  `__name__` 은 뭐고 `__main__`은 뭘까요?

 `__name__`은 모듈(파일)의 이름을 나타냅니다. 예를 들어, 실행된 python 파일의 이름이 kim.py 라면 `__name__` 의 값은 kim이 되는 겁니다. 

그럼 `__main__`은 뭘까요?  사실 `__name__`은 특별한 기능이 하나 더 있습니다. 

해당 python 파일이 import 되지 않고 직접적으로 실행될 때, 즉 main program으로서 작동 했을 때 `__name__`의 값은 모듈 이름이 아니라 `__main__`으로 나타나게 됩니다.

말이 어려우니 코드를 쳐봅시다.

먼저 python 파일을 2개 만들어 보겠습니다.

```
test/
    test1.py
    test2.py
```

```python
# test1.py

print(__name__)
```

```python
# test2.py

import test1
```

이런식으로 test1.py 파일과 test2.py 파일을 만들고 실행해 보겠습니다. 결과는 아래와 같습니다.

```shell
$ python test1.py
__main__
```

```shell
$ python test2.py
test1
```

test1.py 파일을 직접 실행했을 때는 `__name__`의 print 값이 `__main__`으로 나타났습니다. 하지만 test2.py 에서 test1을 import 한 후 test2.py를 실행 했을 때는 `__name__`의 값이 `test1`이라고 나온걸 알 수 있습니다.

위와 같이 test1.py가 직접 실행되었을 때(main program으로서 실행되었을 때)는 module의 이름이 `__main__`이라고 정해지고 import 되어 실행된다면 module의 이름은 해당 파일의 이름이 됩니다. 



예시 코드를 하나 더 만들어 보겠습니다.

```python
# test1.py

print('this is test1.py')
if __name__ == '__main__':
    print('this file is executed as a script')
else:
    print('this file is imported')
```

```python
# test2.py

import test1

print('this is test2.py!!')
```

위와 같이 수정을 하고 python 파일을 각각 실행해 보면 아래와 같은 결과가 나옵니다.

```shell
$ python test1.py
this is test1.py
this file is executed as a script
```

```shell
$ python test2.py
this is test1.py
this file is imported
this is test2.py!!
```

test1.py를 직접 실행했을 때는 `this is test1.py`라는 문장이 먼저 프린트 되고 `__name__`이 `__main__`이기 때문에 if 문이 `True` 가 되므로 `this file is executed as a script`라는 문장이 프린트 되었습니다.

test2.py를 실행했을 때도 마찬가지고 `this is test1.py`라는 문장이 프린트 되었습니다. test1.py를 import 했기 때문이죠(*python은 module을 import하면 module의 모든 코드를 다 읽습니다) 

그 아래는 test1.py를 실행했을 때와는 다르게 `this file is imported`라는 문장이 출력되었습니다. test1 이 import 되어 사용되었기 때문에 `__name__` 값이 `test1` 이 되고 if 문이 `False` 이기 때문에 else에 결과가 실행이 된 것입니다. 

test1의 코드가 모두 실행이 된 후에 test2.py 의 코드인  `this is test2.py!!`라는 문장이 출력됩니다. 



### 결론

`__name__`은 모듈의 이름을 나타내고 직접 실행될 경우(main program 으로서 실행, script로서 실행)에는 `__main__`이라는 이름을 가진다.