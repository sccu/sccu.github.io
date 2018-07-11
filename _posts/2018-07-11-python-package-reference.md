---
category: python
tags: python import package reference module
---
(이 글은 python 3.6 기준으로 작성되었다.)

패키지는 파이썬의 모듈에 대한 네임스페이스를 점(.)이 들어간 모듈 이름을 사용해 구조화하는 방법이다. 패키지를 임포팅할 때, 파이썬은 패키지 하위 디렉토리를 찾기 위해 ```sys.path``` 상의 디렉토리들을 검색한다. 

디렉토리를 패키지로 취급하도록 하기 위해서는 그 디렉토리에 ```__init__.py``` 파일이 있어야 한다. ```__init__.py``` 파일은 빈 파일일 수도 있고, 패키지를 위한 초기화 코드를 실행할 수도 있다.

만약 import하고자 하는 모듈이 포함된 패키지가 패키지 경로에 포함되지 않았다면, 다음과 같은 에러 메시지를 만나게 된다.
```bash
Traceback (most recent call last):
  File "../../integration/make_items.py", line 10, in <module>
    from utils import cvt
ModuleNotFoundError: No module named 'utils'
```

패키지 경로를 추가하는 방법은 다음과 같다.
#### 1. PYTHONPATH에 패키지 경로 추가
```bash
PYTHONPATH=my/project/root python hello.py
```

#### 2. ```sys.path```에 패키지 경로 추가
```python
"""
hello.py
"""

import sys
sys.path.append("my/project/root")
```
단, 이 방식은 ```sys.path.append``` 부분이 다른 import문보다 앞에 오게 되는데, 이는 각종 IDE들의 inspection에서 warning을 발생시킬 수도 있다.


이글에 대한 보다 상세한 내용은 파이썬 튜토리얼의 [Packages](https://docs.python.org/3/tutorial/modules.html#packages)에서 확인할 수 있다.

