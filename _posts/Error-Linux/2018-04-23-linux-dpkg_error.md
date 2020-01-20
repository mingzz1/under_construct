---
layout: post
title: ! "[Linux 오류] Could not get lock 오류"
excerpt_separator: <!--more-->
comments: true
categories : [Error/Linux]
tags:
  - Error
  - Linux
---

Ubuntu에서 `apt-get`을 사용하다보면 아래의 오류를 자주 볼 수 있다.

요즘들어 특히 자주보여 블로그에 정리하려 한다.

<!--more-->

```
E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?
```

아래의 2가지 방법 중 하나를 사용하면 거의 해결된다.

### 1. lock 삭제

```
rm -rf /var/lib/dpkg/lock
```

### 2. clear cache

```
apt-get autoclean $$ apt-get clear cache
```

### 3. lock 삭제 후 apt update
```
rm /var/lib/apt/lists/lock
rm /var/cache/apt/archives/lock
rm /var/lib/dpkg/lock*
sudo dpkg --configure -a
apt update
```
