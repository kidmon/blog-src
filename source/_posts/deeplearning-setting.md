---
toc: true
widgets:
  - type: toc
    position: right
  - type: category
    position: right
  - type: recent_posts
    position: right
sidebar:
  right:
    sticky: true
title: 딥러닝 입문자를 위한 Tensorflow-GPU 개발 환경 처음부터 끝까지 구축하기(+CUDA, cuDNN, Anaconda, PyCharm)
date: 2019-11-03 02:55:50
categories: [Deep Learning, Tensorflow]
tags: [Deep Learning, Tensorflow, Python, 개발 환경]
thumbnail:
---

이번 포스팅에서는 Windows 10에서 `CUDA, Anaconda, Tensorflow`를 이용한 딥러닝 환경을 구축하는 과정을 알아보겠습니다.
<!--more-->
사실 구글링을 해보면 딥러닝 환경 구축에 대한 좋은 포스팅이 많이 있습니다. 그러나 저처럼 Python 및 IDE 설치부터 Tensorflow까지 딥러닝 공부를 처음 시작하는 사람이 참고하기에는 조금 어려운 내용이 많더군요…ㅠㅠ

그래서 이번에는 처음 딥러닝 공부를 시작하시는 분들에게 조금이나마 도움이 되고자 `처음부터 끝까지` 차근차근 진행해보겠습니다!!

---

## 어떻게 개발 환경을 구축하나요?
딥러닝 개발을 지원하는 프레임워크는 제가 이번에 사용할 Tensorflow부터 Keras, Theano, Torch 등 다양한 종류가 있습니다.

그중에서도 제가 `Tensorflow`를 선택한 이유는 가장 인기 있고 많이 사용되고 있으며, 사용자가 많다 보니 도중에 오류가 발생하거나 혼자 해결하기 힘든 문제가 생겼을 때 참고할 커뮤니티가 활성화되어있기 때문입니다. 구글링을 했을 때 자료가 가장 많기도 하고요ㅋㅋㅋ

이번에 구축할 개발 환경의 각 버전은 다음과 같습니다.

> - Python -- ***3.6***
> - CUDA -- ***9.0***
> - cuDNN -- ***9.0***
> - Tensorflow -- ***1.8***

### Python
**Python**은 이번 딥러닝 환경에서 사용될 `프로그래밍 언어`입니다. 자세한 설명은 [위키백과](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%B4%EC%8D%AC)를 참고해주세요.

### PyCharm
**PyCharm**은 Python 프로그래밍에 사용되는 `IDE(Integrated Development Environment, 통합개발환경)`입니다. 한마디로 Python을 이용한 개발을 가능하게 해주는 `작업실`이라고 할 수 있습니다.

### CUDA
> CUDA ("Compute Unified Device Architecture", 쿠다)는 [그래픽 처리 장치](https://ko.wikipedia.org/wiki/%EA%B7%B8%EB%9E%98%ED%94%BD_%EC%B2%98%EB%A6%AC_%EC%9E%A5%EC%B9%98)(GPU)에서 수행하는 (병렬 처리) 알고리즘을 C 프로그래밍 언어를 비롯한 산업 표준 언어를 사용하여 작성할 수 있도록 하는 [GPGPU](https://ko.wikipedia.org/wiki/GPGPU) 기술이다. CUDA는 [엔비디아](https://ko.wikipedia.org/wiki/%EC%97%94%EB%B9%84%EB%94%94%EC%95%84)가 개발해오고 있으며 이 아키텍처를 사용하려면 엔비디아 GPU와 특별한 스트림 처리 드라이버가 필요하다. CUDA는 G8X GPU로 구성된 지포스 8 시리즈급 이상에서 동작한다. CUDA 플랫폼은 [컴퓨터 커널](https://ko.wikipedia.org/wiki/%EC%BB%B4%ED%93%A8%ED%84%B0_%EC%BB%A4%EB%84%90)의 실행을 위해 GPU의 가상 [명령 집합](https://ko.wikipedia.org/wiki/%EB%AA%85%EB%A0%B9_%EC%A7%91%ED%95%A9)과 병렬 연산 요소들을 직접 접근할 수 있는 소프트웨어 계층이다.
>
> 출처 - [위키백과](https://ko.wikipedia.org/wiki/CUDA)

네 그렇습니다. **CUDA**는 게임을 할 때만 사용되는 줄 알았던 그래픽카드의 연산장치인 `GPU를 이용하여 프로그래밍 연산`을 가능하게 해주는 기술입니다. 저도 제대로 이해한 건 이번이 처음이네요!!

### cuDNN
**cuDNN(CUDA Deep Neural Network library)**은 위에서 설명한 CUDA에서 사용되는 `딥러닝 라이브러리`입니다.  CUDA를 사용한 딥러닝 개발환경에 특화되어 있습니다.

### Tensorflow
**Tensorflow**는 `딥러닝 개발 프레임워크` 중 가장 유명하고 또 많이 사용되는 라이브러리입니다. Google Brain 팀에서 만들었고 현재 오픈소스로  공개되어 있습니다.

설명은 이쯤에서 마무리하고 이제 딥러닝 환경 구축을 위한 준비를 시작해보겠습니다.

---

## 내 컴퓨터 성능 확인하기
딥러닝 환경 구축을 시작하기 전에, 먼저 내 컴퓨터에서 `Tensorflow-GPU`를 사용할 수 있는지 확인해야 합니다. 아래는 Tensorflow에서 공식적으로 요구하는 컴퓨터 사양입니다. 자세한 내용은 [여기](https://www.tensorflow.org/install/gpu)에서 확인 가능합니다.

<center>
<br>

![Tensorflow를 사용하기 위한 요구사항들](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572709533799_image.png)

<br>
</center>

물론 CUDA를 사용하지 않더라도 딥러닝 환경 구축이 가능합니다. 말씀드렸다시피 CUDA는 `프로그래밍 연산에 GPU를 사용`할 수 있게 해서 연산 속도를 빠르게 하는 기술이지만, 딥러닝 환경에 필수적인 것은 아닙니다. GPU가 안 되면 CPU로 계산하면 되니까요.

당연하게도 `Tensorflow는 CPU 버전과 GPU 버전 두 가지를 모두 제공`하고 있습니다. 그래도 이왕이면 GPU를 사용해서 CUDA를 써보는 게 좋겠죠??

참고하실 분들을 위해 현재 제가 집에서 사용하고 있는 컴퓨터 사양을 공개합니다.

> - OS : Windows 10 Pro
> - CPU : AMD Ryzen 5 1600 3.2GHz
> - VGA : NVIDIA GeForce GTX 1060 3GB

막상 적어놓고 보니 업그레이드하고 싶은 마음이 솟구치네요…ㅋㅋㅋ

CUDA를 사용하기 위해서는 가장 먼저 본인의 `그래픽카드의 Compute capability`가 얼마인지부터 확인하셔야 합니다. 최신 버전의 텐서플로우를 사용하기 위해서는, Compute capability가 ***3.5*** 이상이 되어야 한다고 하네요.

NVIDIA GPU에서 지원하는 그래픽카드 모델별 Compute capability는 [여기](https://developer.nvidia.com/cuda-gpus)에서 확인하실 수 있습니다.

<center>
<br>

![그래픽카드 모델별 Compute Capability](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572770441751_image.png)

<br>
</center>

제가 사용 중인 GeForce GTX 1060 모델은 Compute Capability가 6.1로 CUDA 사용이 가능합니다. 뭐 엄밀히 따지자면 GeForce GTX 1060보다 약간 하위 모델인 GeForce GTX 1060 3GB 지만 다른 모델과 비교해보면 무리 없이 사용이 가능할 것 같습니다.

자, 내 컴퓨터에서 CUDA를 사용할 수 있다는 것을 확인했으니 이제부터 진짜로 환경 구축을 시작해봅시다!!는 개뿔 아직 한 가지가 더 남았습니다…

바로 `그래픽카드 드라이버 최신버전 업데이트`입니다.

그래픽카드 드라이버는 ***410.x*** 이상의 버전을 설치해주셔야 합니다. [여기](http://www.nvidia.com/Download/Find.aspx?lang=en-us)를 통해 내 그래픽카드가 410.x 이상을 지원하는지 확인한 후 드라이버를 다운받아서 설치해주시면 됩니다.

<center>
<br>
    
![드라이버 다운로드](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572709641611_image.png)

<br>
</center>

---

## 호환 가능한 버전 확인
드라이버 다운로드 및 설치까지 완료하셨다면 이제부터가 진짜 시작입니다. CUDA, Anaconda, Tensorflow를 서로 `호환 가능한 버전`으로 준비해줘야 합니다.

사실 프로그래밍 환경 구축에서 가장 어려운 부분이 바로 이거죠. 저를 비롯한 여러 초보 개발자분들이 종일 구글링을 하시는 이유이기도 하고요.

미리 호환 여부를 확인하지 않고 설치를 진행하시면 중간에 `처음부터 다시 시작`해야 하는 불상사가 생길 수도 있습니다. 저도 그랬거든요…ㅠㅠ

아까 도입부에서 말씀드린 것처럼 저는 아래와 같은 버전을 사용할 예정입니다.

> - Python -- ***3.6***
> - CUDA -- ***9.0***
> - cuDNN -- ***9.0***
> - Tensorflow -- ***1.8***

현재 Tensorflow 2.0 버전이 10월 1일부로 Release되었고 많은 부분이 변경되어 사용하기가 더 편리해졌다고 합니다.

그럼에도 불구하고 제가 1.8 버전을 사용하는 이유는 딥러닝을 처음 공부하는 학생 입장에서 참고하고 공부할 자료가 많은 것이 좋다고 생각했기 때문입니다. 실제로 구글링 했을 때 나오는 포스팅이나 현재 출판된 많은 책들이 1.x 버전을 토대로 하고 있습니다.

그래도 언제까지 옛날 버전을 사용하고 있을 수는 없겠죠?? 얼른 공부를 끝내고 다음에는 Tensorflow 2.0에 관한 포스팅을 쓸 수 있도록 하겠습니다!!

---

## 설치 파일 다운로드
### Anaconda
먼저 `Python과 각종 라이브러리를 한 번에 설치`할 수 있게 해주는 Anaconda부터 다운받아보겠습니다. Anaconda는 [여기](https://repo.anaconda.com/archive/)에서 다운받으실 수 있습니다.

<center>
<br>

![Anaconda Archive](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572772293446_image.png)

<br>
</center>

참고로 저와 다른 버전의 Anaconda를 사용하고자 하시는 분들은 [여기](https://docs.anaconda.com/anaconda/packages/oldpkglists/)를 참고하셔서 Anaconda 버전별로 포함된 Python 및 라이브러리를 확인하고 본인에게 필요한 버전을 다운받으시면 됩니다.

저는 `Python 3.6이 포함된 Anaconda3-5.2.0 버전`을 준비하겠습니다.

### CUDA
다음으로 CUDA를 다운받아야 합니다. 제가 이번에 사용할 `Tensorflow 1.8 버전`과 호환이 가능한 것은 `CUDA 9.0 버전`입니다. CUDA는 [여기](https://developer.nvidia.com/cuda-toolkit-archive)에서 다운로드받으시면 됩니다.

<center>
<br>

![CUDA Archive](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572709723142_image.png)

<br>
</center>

### cuDNN
다음은 cuDNN입니다. CUDA와 마찬가지로 `cuDNN 9.0 버전`을 사용하겠습니다. cuDNN은 [여기](https://developer.nvidia.com/cudnn)에서 다운받으시면 됩니다. cuDNN을 다운로드하기 위해서는 회원가입이 필요합니다. 금방 끝나니까 얼른 가입하시고 다운받아주세요^^

<center>
<br>

![cuDNN 다운로드](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572709789760_image.png)

<br>
</center>

Anaconda, CUDA, cuDNN 다운로드를 완료하셨다면 이제 절반은 끝났습니다!! 이후 설치 과정은 정말 간단합니다. 프로그램 간에 버전 충돌만 없다면요…

그런데 왜 Tensorflow는 다운받지 않냐고요?? Tensorflow는 이후 Anaconda를 이용한 가상환경 구축과정에서 다운받을 예정입니다. 정말 간단하니 걱정하지 않으셔도 됩니다.

---

## CUDA, cuDNN, Anaconda 설치
### CUDA
그럼 이제 설치를 진행해볼까요?? 가장 먼저 CUDA를 설치해줍니다. CUDA 설치를 진행하기 전에 아까 다운받은 `그래픽카드 드라이버`를 꼭 설치해주세요!!

<center>
<br>

![CUDA 설치 - 1](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572714677753_image.png)

![CUDA 설치 - 2](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572714698607_image.png)

![CUDA 설치 - 3](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572714728855_image.png)

<br>
</center>

설치 옵션에서는 사용자 정의 설치를 선택해주시면 되는데요. 굳이 빠른 설치가 아닌 사용자 설치를 선택하는 이유는 필요 없는 소프트웨어 설치와 그래픽카드 드라이버 다운그레이드를 막기 위함입니다. 설치 경로는 기본 경로 그대로 두시면 됩니다.

<center>
<br>

![CUDA 설치 - 4](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572714795008_image.png)

<br>
</center>

여기서 [다음]을 눌러주시고 설치가 완료될 때까지 기다려주시면 CUDA 설치는 끝납니다. 정말 간단하죠?? 이후에는 더 별거 없습니다.

### cuDNN
다음은 cuDNN을 설치해보겠습니다. 사실 설치라고 할 것까지도 없습니다. 그냥 압축을 풀고 `복사, 붙여넣기`만 하면 끝나거든요.

다운받은 cuDNN의 압축을 풀고 bin, include, lib 폴더를 복사해서 CUDA가 설치되어있는 C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0 폴더에 붙여넣기 해주시면 됩니다.

<center>
<br>

![CUDA 설치 경로](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572782007775_image.png)

<br>
</center>

그 후 CUDA가 설치된 폴더를 `환경 변수에 추가`해줍니다. 환경 변수는 [내컴퓨터] 마우스 우클릭 → 좌측 상단 [고급 시스템 설정] → 우측 하단 [환경 변수]로 들어가서 확인 가능합니다.

<center>
<br>

![CUDA 환경 변수 추가](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572773492888_image.png)

<br>
</center>

그런데 환경 변수를 확인해보니 이미 `CUDA_PATH, CUDA_PATH_V9_0`이 추가가 되어있네요. 아마 설치과정에서 자동으로 등록된 것 같습니다. 개꿀이네요.

이제 CUDA와 cuDNN 설치는 완료되었습니다.

### Anaconda
다음으로 Anaconda를 설치하겠습니다.

<center>
<br>

![Anaconda 설치 - 1](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572711654014_image.png)

<br>
</center>

Anaconda 설치도 간단합니다. 아까 다운받은 설치파일을 실행한 후 [Next]를 클릭합니다.

<center>
<br>

![Anaconda 설치 - 2](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572711675923_image.png)

<br>
</center>

딥러닝 환경에 사용하실 컴퓨터가 공용이라면 [Just Me], 공용 컴퓨터가 아니라면 [All Users]를 선택해주시면 됩니다. 설치 경로는 기본 경로로 해주시고요.

<center>
<br>

![Anaconda 설치 - 3](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572712393382_image.png)

<br>
</center>

위의 체크 박스는 `Anaconda 환경 변수를 자동으로 추가`해주는 옵션입니다. Not recommend라고 되어있지만 기존에 설치해둔 Python이나 Anaconda가 없으니 체크하고 진행하시면 되겠습니다.

<center>
<br>

![Anaconda 설치 - 4](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572712345982_image.png)

<br>
</center>

마지막으로 Microsoft VSCode를 설치하라는 화면이 나옵니다. VSCode대신에 PyCharm을 쓸 예정이니 여기는 그냥 Skip 해주세요.

이제 Anaconda 설치도 끝났습니다.

---

## PyCharm 설치 및 가상 환경 구축
진짜 마지막으로 이번에는 `Python을 이용한 개발을 더 쉽게 해 주는 IDE,  PyCharm`을 설치해봅시다. PyCharm은 [여기](https://www.jetbrains.com/pycharm/download/#section=windows)에서 다운로드받으시면 됩니다.

Professional과 Community 버전이 있는데 Professional 버전은 유료로, `Community 버전은 무료`로 사용할 수 있습니다. (대학생이신 분들은 간단한 등록과정을 통해 Professional 버전을 무료로 사용 가능합니다.) Community 버전으로도 충분히 딥러닝 환경 구축이 가능하니 저는 Community 버전을 사용하겠습니다.

<center>
<br>

![PyCharm 다운로드](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572712069414_image.png)

<br>
</center>

PyCharm을 다운받은 후에는 바로 설치를 진행하시면 됩니다. 설치과정 캡처가 좀 생략되었는데, 정말 별거 없으니 그냥 [Next], [Next] 눌러주시고 기본 경로에 설치해주시면 됩니다.

<center>
<br>

![PyCharm Theme 선택](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572712484646_image.png)

<br>
</center>

설치 후에 PyCharm을 실행시켜서 Theme를 선택하고,

<center>
<br>

![PyCharm PlugIn 설치](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572712498246_image.png)

<br>
</center>

필요한 PlugIn을 설치하면 아래와 같은 화면이 나옵니다. (저는 포스팅 편집을 위해 Markdown을 설치했습니다. 여러분은 안 하셔도 괜찮습니다.)

<center>
<br>

![PyCharm 설치 및 설정 완료](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572712520233_image.png)

<br>
</center>

여기까지 하셨으면 잠시 Anaconda로 한 번 갔다 와야 합니다. 아까 말씀드린 것처럼 `PyCharm에서 사용할 가상 환경`을 만들어야 하거든요.

Windows 검색을 이용해서 `Anaconda Prompt`를 실행하고
```
conda create -n 가상환경이름 python=버전
```
처럼 입력해주시면 가상 환경이 만들어집니다.

저는 tensorflow라는 이름의 Python 3.6.5 버전을 사용하는 가상 환경을 만들기 위해
```
conda create -n tensorflow python=3.6.5
```
커맨드를 입력했습니다.

그  후 Python과 함께 설치될 다른 라이브러리의 정보가 나오고, [Y]를 입력해주시면 가상 환경 생성이 완료됩니다.

<center>
<br>

![Anaconda 가상 환경 생성](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572715297240_image.png)

<br>
</center>

가상 환경이 생성되고 나면
```
activate 가상환경이름(저의 경우에는 tensorflow)
```
커맨드 입력을 통해 가상 환경을 활성화합니다.

가상 환경을 활성화하고 난 후
```
pip install tensorflow-gpu==버전
```
커맨드 입력을 하시면 드디어 Tensorflow가 설치됩니다!!

저는 1.8.0 버전 설치를 위해
```
pip install tensorflow-gpu==1.8.0
```
커맨드를 입력했습니다.

<center>
<br>

![가상 환경에서 Tensorflow 설치](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572715386322_image.png)

<br>
</center>

Tensorflow는 `CPU 버전과 GPU 버전을 모두 지원`하기 때문에, CUDA와 함께 GPU 버전을 이용하실 분들은 tensorflow-gpu 설치를, CPU 버전을 이용하실 분들은 그냥 tensorflow를 설치해주시면 됩니다.
```
pip install tensorflow-gpu #GPU 버전 설치
pip install tensorflow #CPU 버전 설치
```

<center>
<br>

![Tensorflow-GPU까지 설치 완료](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572715503688_image.png)

<br>
</center>

이제 설치는 모두 끝났습니다. 그럼 간단한 커맨드 입력으로 설치가 잘 되었는지 확인해봅시다.

<center>
<br>

![과연 설치가 잘 되었을까요??](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572715575031_image.png)

<br>
</center>

python이라는 커맨드를 입력해서 Python 인터프리터로 넘어간 후에
```
import tensorflow as tf
```
딱 한 줄만 입력해주시면 설치가 잘 되었는지 확인할 수 있습니다. 오류가 안 뜨면 설치가 성공적으로 완료된 겁니다!!

<center>
<br>

![띠용…?? 오류 메시지인가??](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572715619150_image.png)

<br>
</center>

아마 깜짝 놀라셨을 수도 있습니다… 뭔 오류 메시지 비슷한 것들이 주르륵 출력되었으니까요.

하지만 다행스럽게도 위와 같은 메시지는 오류가 아니라 `numpy의 버전으로 인한 경고 메시지` 입니다.

<center>
<br>

![numpy 다운그레이드](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572715690181_image.png)

<br>
</center>

아래와 같이 `1.17 버전 이하의 numpy로 다운그레이드`해 주시면 경고 메시지는 사라집니다.
```
pip install "numpy<1.17"
```

<center>
<br>

![클ㅡ린하게 설치 완료!!!](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572715714878_image.png)

<br>
</center>

다시 PyCharm으로 돌아가서 방금 만든 가상 환경을 적용해줍시다. 아까 봤던 PyCharm 실행 화면에서 우측 하단의 [Configure]로 들어갑니다.

<center>
<br>

![Configure 클릭](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572712520233_image.png)

<br>
</center>

그 후 왼쪽에 보이는 [Project Interpreter]로 들어갑니다.

<center>
<br>

![Project Interpreter 클릭](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572716191012_image.png)

<br>
</center>

[Project Interpreter]로 들어가서 좌측 상단에 [Conda Environment]를 클릭합니다. 그 후 [Existing Environment]를 선택하고 아까 만들어 놓은 가상 환경을 선택합니다. 저는 tensorflow라는 이름으로 가상 환경을 만들었었죠.

Anconda를 기본 경로로 설치했을 때 가상 환경이 저장되는 경로는 
> `C:\Users\사용자이름\AppData\Local\conda\conda\envs`

입니다.

<center>
<br>

![만들어 놓은 가상 환경 선택](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572716376841_image.png)

<br>
</center>

이제 프로젝트를 실행할 수 있는 Interpreter에 Anaconda에서 만든 가상 환경이 추가되었습니다.

<center>
<br>

![가상 환경 추가 완료](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572716422402_image.png)

<br>
</center>

이후 [Apply]를 눌러주시고 설정을 끝내면 아래와 같이 Interpreter 업데이트가 완료됩니다.

<center>
<br>

![드디어 끝](https://paper-attachments.dropbox.com/s_598BBF9D3854C8BA18AAD1FA32CB0BF349B2A099BA33988E57F1DF8A4C6F0832_1572716492831_image.png)

<br>
</center>

여기까지 오셨다면 Tensrflow-GPU 딥러닝 환경 구축이 완료된 것입니다. 정말 고생 많으셨습니다…ㅠㅠ

---

## 마치며
환경 구축을 진행하면서 오류나 충돌이 한 번도 없었다면 다행이지만, 오류나 충돌이 발생했다면 내가 설치하고자 하는 버전 간의 호환이 가능한지 다시 한번 확인하고 처음부터 차근차근 진행해보시길 바랍니다. 또한 구글링하면 참고할 수 있는 좋은 포스팅이 많이 있습니다.

부족한 포스팅이지만 누군가에게는 도움이 되길 바라며 이만 마무리 하겠습니다. 모두 딥러닝 환경 구축에 성공하시고 얼른 딥러닝의 세계로 입문하시길 기원합니다. 감사합니다!!
