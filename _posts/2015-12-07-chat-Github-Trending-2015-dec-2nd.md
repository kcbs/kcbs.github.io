---
layout: default
title: 2015년 12월 둘째주 Github Trending
category: Github Trending
tags:
- Chat
- Github
- Github-Trending
keywords:
- 깃헙
- 깃헙 트렌딩
- 프로그래밍 언어
- Git
- Repository
- 랭킹
- 2015년 12월
- awesome-interviews
- FreeCodeCamp
- activate-power-mode
- IncludeOS
- XActivatePowerMode
---

매주 Github Trending을 보며 이런저런 이야기를 해보는 시간입니다. 핫한 Repository를 분석해봅니다.
## HOT Repository

### 1. <a href="https://github.com/openalpr/openalpr">openalpr/openalpr</a>
이번부의 1위는 openalpr입니다. 이름에서 어떤 repo인지 눈에 확 들어오지는 않네요. 네이밍 센스가 부족한듯 합니다... 어쨌튼 이 repo는 바로 **차량 번호판 인식기** 입니다. 사진을 입력해주면 사진에 나타나있는 번호판을 인식해서 글자 인식해서 출력해줍니다. 아무래도 항상 100%로 인식하기는 힘들기 때문에, 인식을 하게 되면 confidence라는 수치도 같이 표기되며, 이는 정확도를 나타내게 됩니다.

C++로 작성되어있어서 왠만한 개발환경(iOS, Android, OSX, Linux, Windows 등등)에 다 간단히 추가할수 있는것도 좋은 부분이네요. 오늘만 728개의 Star를 받았습니다.

### 2. <a href="https://github.com/ipselon/structor">ipselon/structor</a>
<img src="/image/2015-12-07-github-trending/title-background.png">
2위는 Structor로, 페이스북의 새로운 언어인 React의 UI 빌더입니다. 요즘 여러모로 핫한 언어이다 보니까 관련된 프로젝트들도 같이 주목받고 있네요.

<a href="https://www.youtube.com/watch?v=AY65e6Ry_rY&list=PLAcaUOtEwjoR_U6eE2HQEXwkefeVESix1">여기</a>서 튜토리얼 영상을 보실 수 있습니다. (YouTube)

### 3. <a href="https://github.com/nathancahill/Split.js">nathancahill/Split.js</a>
이번에는 오랫만에 웹 어플리케이션입니다. Split.js는 이름 그대로 화면을 분할해주는데, 가로, 세로 등으로 간단하게 화면을 분할해주며, Resizing도 쉽게 가능합니다.

<a href="http://nathancahill.github.io/Split.js/">여기</a>서 쉽게 데모를 확인할 수 있습니다. 가로+세로 등의 복합적인 레이아웃도 간단히 적용 가능하군요. 여러보로 쓸모있는 라이브러리 같아 보입니다.

... 일단 가볍게 본 블로그에도 submodule로 추가해뒀습니다.

### 4. <a href="https://github.com/hashcat/hashcat">hashcat/hashcat</a>
Hashcat은... 간단히 말하면 해킹툴입니다. 명목상으로는 "CPU-based password recovery utility"라고 되어있지만, 실상은 단순한 비밀번호 복호화 툴입니다. MIT라이선스로 공개되어 제약이 거의 없고, 100개 이상의 공격을 제공한다고 하는군요. 윈도우 7/8/10, OS X, GNU/Linux 등등의 OS의 패스워드파일을 복호화할 수 있는 모양입니다...

얼마나 높은 성공률로 뚫을 수 있을지는 모르겠지만 상당히 유용한 툴인건 확실해 보입니다. 좋은 쪽으로만 사용된다면 말이죠(...)

### 5. <a href="https://github.com/ChALkeR/notes">ChALkeR/notes</a>
상당히... 괴상한 Repo입니다. 들어가보시면 아시겠지만 정말 그냥 노트입니다. 블로그 대신에 적어둔거라고 하고... 그냥 포스팅도 하나밖에 없습니다. 하루만에 242개의 Star를 받은게 신기하긴 합니다.

개인적으로 추측해보면 그 하나의 포스팅의 퀄리티가 상당히 뛰어나기 때문으로 보입니다. `Credential Leaks를 얕보지 말라`는 글인데, 읽어보면 알겠지만 상당히 디테일합니다. 보안적으로 Hack이 가능했던 프로그램들이라던지, 자주 문제가 되는 파일들이라던지...

보안쪽으로 관심이 있으신 분들은 한번쯤 읽어보시면 좋을법한 글입니다. npm과 Github에 관련된 내용이 많으며, 여러가지 생각지도 못한 파일들도 언급합니다. 예를들면, `Sublime Text`의 설정파일도 조심하라고 적혀있는데, 여기에 Github의 oAuth 토큰 정보가 담겨져있다고 합니다.

글의 작성자도 언급하지만, 저 글에 나와있는건 극히 일부일 뿐이므로, 보안에는 정말 주의해야할 듯 합니다.

## 마무리
1위의 차량 번호판 인식기는 신박한 물건인 듯 합니다. 이미지 처리 기법은 제가 다뤄본적이 없는 분야이기 때문인지는 몰라도, 항상 신기하게 느껴집니다.
2위와 3위는 Front End를 타겟으로 하는 물건들이였네요. 둘다 UI에 도움되는 물건이니까요. 개인적으로는 2위의 React UI Builder가 눈에 띄는데, React의 발전에 조금 더 도움이 되었으면 하는 바람입니다.
이번주에는 아무래도 상위권보다는 조금 하위권의 보안 관련 repo들이 눈에 띄는군요. 해킹은 컴퓨터 역사상 가장 중요하게 여겨져온 분야이고, 아직까지도 여러가지 공격방식, 방어방식이 연구되고 있습니다. 4위가 Hash를 복호화하는 공격방식이고 5위가 개인정보를 보호하는 방어방식인 것을 보면 의미심장 하네요.