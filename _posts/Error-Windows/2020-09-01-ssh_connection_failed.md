---
layout: post
title: ! "[VMware Connection failed] VMware SSH 연결 오류 - ip 구성이 올바르지 않습니다"
excerpt_separator: <!--more-->
comments: true
categories : [Error/Windows]
tags:
  - Error
  - Windows
  - Xshell
  - Vmware
---

또 Vmware의 가상머신에 SSH로 연결하려 했더니 연결 오류가 났다.  

지난번에는 오류 문구라도 있었는데, 이번에는 그냥 `Connection failed`다.  

<!--more-->

오류 상황은 아래와 같다.  

```
Connecting to 192.168.171.134:22...
Could not connect to '192.168.171.134' (port 22): Connection failed.

Type `help' to learn how to use Xshell prompt.
```

`ping` 명령어를 이용 해 봐도 제대로 응답이 오지 않길래, 내 Windows에서 `ipconfig`를 통해 네트워크를 확인 해 보았다.  

![](/images/error/ssh_connection_failed/01.png)  

확인 해 보니, 내 `NAT`로 구성되어 있는 내 가상머신들의 `IP`는 `192.168.171.0` 대역인데, `VMware Network Adapter VMnet8`은 `169.254.251.75`이다.  

도대체 왜 바뀐지를 모르겠다.  

`VMWare`에서 `Edit > Virtual Network Editor`를 선택 해 확인 해 보면 내 가상머신의 서브넷 주소를 알 수 있다.  

![](/images/error/ssh_connection_failed/02.png)  

즉, `VMware`에서 설정되어 있는 `VMNet8`의 대역과 내 Windows PC에서 설정 된 대역이 다른 것이다.  

이를 맞추기 위해서는 `Virtual Network Editor`를 변경해도 되는데, 나는 그냥 아래 명령어를 통해서 Windows에 설정을 변경했다.  

```
> ipconfig/renew
```

![](/images/error/ssh_connection_failed/03.png)  

그 결과 `VMware NEtwork Adapter VMnet8`의 IP 대역이 변경 된 것을 알 수 있다.  

다시 연결을 시도 해 보면 정상적으로 연결할 수 있다.  