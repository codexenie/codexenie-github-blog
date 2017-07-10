---
title: DOUBLE_FREE
tags: 'CWE-415, Double Free'
date: 2017-07-10 15:38:33
---

# double free(저승에서 저승으로)
 > 주제 그대로 같은 변수에 대해 중복 free를 할 경우

 ```cpp
    free(ptr);

    free(ptr);
 ``` 