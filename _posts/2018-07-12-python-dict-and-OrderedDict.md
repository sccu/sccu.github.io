---
category: python
tags: python dict OrderedDict insert insertion order
title: Python dict and OrderedDict
---
Python 3.5까지 ```dict```는 삽입 순서(insertion order)를 유지하지 않았다. 3.6에서는 ```dict```가 삽입 순서를 유지하게 되었지만, 이는 dict 클래스의 구현 변경에 따른 결과이지 언어의 특성이 아니다. 따라서 이 특성을 가정하고 사용해서는 안 된다.Python 3.7부터는 ```dict```의 삽입 유지가 언어 특성으로 추가되었다. 

그러면 3.1에 도입된 ```OrderedDict```는 3.7부터는 더 이상 필요하지 않게 된 걸까? 그렇지 않다. ```OrderedDict```는 동일성 테스트(equality test)에서 ```dict```와 다르게 동작한다. 그 용도가 많이 줄어들기는 했지만 아직은 쓸모가 있다.

```python
In [1]: #python 3.6+

In [2]: dict({1:1, 2:2, 3:3}) == dict({3:3, 2:2, 1:1})
Out[2]: True

In [3]: OrderedDict({1:1, 2:2, 3:3}) == OrderedDict({3:3, 2:2, 1:1})
Out[3]: False
```
