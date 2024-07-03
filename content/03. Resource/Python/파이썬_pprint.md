---
title: 파이썬_pprint
created: 2024-03-16
modified: 2024-03-16 23:06
cssclasses:
  - max
tags:
  - python
  - python/pprint
---
## 데이터를 보기 좋게 출력
```python
import pprint

result = {'userId': 1, 'id': 1, 'title': 'sunt aut facere repellat provident occaecati excepturi optio reprehenderit', 'body': 'quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto'}

pprint.pprint(result)

## 출력 결과
{'body': 'quia et suscipit\n'
         'suscipit recusandae consequuntur expedita et cum\n'
         'reprehenderit molestiae ut ut quas totam\n'
         'nostrum rerum est autem sunt rem eveniet architecto',
 'id': 1,
 'title': 'sunt aut facere repellat provident occaecati excepturi optio '
          'reprehenderit',
 'userId': 1}

```