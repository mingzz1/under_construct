---
layout: post
title: ! "[Python 오류] command errored out with exit status 1 python setup.py egg_info 오류"
excerpt_separator: <!--more-->
comments : true
categories : [Error/Python]
tags:
  - Error
  - Python
---

`Linux` 서버에서 `pip install`로 `Python` 모듈을 설치하려고 하니까 계속 오류가 났다.  

오류 해결 방법은 다음과 같다.  

<!--more-->

발생한 오류는 제목과 같이 `command errored`로 시작하는 오류였다.  

```
ERROR: command errored out with exit status 1 python setup.py egg_info
```

이 경우, 아래와 같이 입력한 후 다시 `pip install`을 통해 설치를 시도해 보면 된다.  

```
# pip install --upgrade setuptools
```