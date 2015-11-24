---
layout: default
title: 2015년 11월 넷째주 Github Trending
category: Chat
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
- 2015년 11월
---

매주 Github Trending을 보며 이런저런 이야기를 해보는 시간입니다. 언어 사용 추세, 핫한 Repository등, 여러 각도에서 분석해봅니다.

## <a href="http://githut.info/">이번주 HOT 언어</a>
> 1. JavaScript
> 2. Java
> 3. Python
> 4. CSS
> 5. PHP

이런 순서로 순위가 매겨졌습니다. 우선 주목할만한 것은 당연히 Javascript/CSS/PHP입니다. 최근 웹 환경의 강세가 한눈에 확 들어오는군요. Javascript/CSS/PHP가 웹 프로그래밍에 적극 활용되기 때문에 이러한 결과가 나온 듯 합니다. 

Java가 2위를 차지하고 있는 것은 안드로이드의 힘이 크겠네요. Obj-C와 Swift는 전체적인 순위에는 올라와있지 않지만 New Fork/New Watchers에서의 순위가 3위권 안에 속해있습니다. 

Python은 이전부터 쭉 오픈소스의 강자로서 군림하고 있었기 때문에 무난하게 3위를 차지한 것으로 보여지네요.

## HOT Repository

### 1. <a href="https://github.com/Mircosoft/vscode">Microsoft / vscode</a>
이번주 1위는 무려 Microsoft가 개발한 `Visual Studio Code`입니다!! 무려 MIT 라이센스로 공개된 이번 VS Code의 소스코드는 많은 사람들의 관심을 끌어모으기 충분했습니다. 공개된지 2주여만에 500여개의 Issue가 달렸고, 60여개의 Pull Request가 들어오는등 많은 개발자들의 사랑을 받았습니다. 이후의 VS Code의 행보가 궁금해지는군요.

### 2. <a href="https://github.com/NARKOZ/hacker-scripts">NARKOZ / hacker-scripts</a>
개그성 Repository입니다. 개인적으로는 상당히 웃었네요. `README.md`에 따르면 배경 설명은 이렇습니다.
>xxx: 우리 회사에 있던 빌드 엔지니어가 다른 회사로 가게 됬어. 그놈은 Terminal에 푹 빠져있는 사람이였지. 알잖아, vim을 사랑하고 모든 그림을 점으로 표현하고 Wiki에 Markdown으로 글을 쓰거나 그런 사람들... 그리고 뭐든 90초 이상 설리는 작업이 있으면 그놈은 그걸 자동화 하기 위해서 Script를 짜뒀지.

>xxx: 그래서 우리는 지금 그놈 컴퓨터 앞에서 그걸 보고있어. 음... "인정"...

>xxx: 너도 보면 아마 좋아할거야.

>xxx: `smack-my-bitch-up.sh` - 그놈 와이프에게 "회사에서 늦는다"고 문자를 보냄. 여러 문장들중 무작위로 하나는 골라거 보냄. 만약 9시 이후에 서버에 SSH 세션이 하나 이상 떠있다면 자동으로 실행됨.

>xxx: `kumar-asshole.sh` - 이메일 수신함에서 "Kumar"(고객 회사의 DBA)를 찾음. 그리고 메일에서 "help", "trouble", "sorry"등의 키워드를 찾음. 키워드가 존재하면 고객 서버에 SSH로 접속해서 제일 최신 백업 버전으로 롤백함. 그리고 나서 "no worry mate, be careful next time"이라고 이메일을 보냄.

>xxx: (이건 오스카상 수상해야함) `fucking-coffee.sh` - 정확하게 17초(!) 기다린 후에 커피머신에 SSH로 접속 (우리는 커피머신이 네트워크에 접속되어있을줄 꿈에도 몰랐음. 심지어 리눅스가 깔려있고 SSHD가 돌아가고 있음.) 그리고 이상한 데이타를 전송함. 바이너리같음. 알고보니까 이게 중간 사이즈의 카페인 반짜리 라떼를 만들고 24초(!)를 기다린 후에 컵에 따라주는 놈이였음. 저 시간은 정확하게 그놈이 자리에서 일어나서 커피머신까지 도착하는 시간이였음.

>xxx: Holy Sh*t. 이거 킵해야됨.

... 웃긴 이야기인듯 하지만 충분히 현실성 있는 이야기라고 생각합니다(...) Cron을 이용해서 자동화시켜둔 듯 하며, 그 소스코드는 모조리 저 Repository에 공개되어 있습니다(...)

### 3. <a href="https://github.com/Automattic/wp-calypso">Automattic / wp-calypso</a>

Calypso는 WordPress의 새로운 프론트엔드 앱 입니다. IE11 이하 버전을 제외하면 **모든** 웹 브라우저를 지원합니다. 모든 워드프레스 사이트들을 한군데서 관리할 수 있게 해주며, 상당히 깔끔한 디자인을 가지고 있는 것으로 보여집니다. 

위의 VS Code와 비슷한 시기에 올라왔지만 역시나 블로깅 분야의 선두주자인 만큼 Issue와 Pull Request가 더 많이 기록되었네요. 다만 VS Code보다 관리는 덜 되고 있는지 Close된 이슈의 수가 상당히 적습니다.


### 4. <a href="https://github.com/docker/dockercraft">docker / dockercraft</a>
이것도 상당히 괴팍한(...) Repository입니다. 마인크래프트를 이용해서  <a href="https://www.docker.com/what-docker">Docker</a>를 관리할수 있게 도와주는 플러그인 입니다(...)

저도 Docker에 대해서는 잘 알지 못해서 <a href="https://www.docker.com/what-docker">여기</a>에서 조금 찾아봤습니다만, 간단히 말하면 모든 OS에서 같은 방식으로 돌아가는 시스템을 만들어주는... 즉, 가상머신과 비슷한 역할을 해주는 물건이였습니다. 여러 대형 회사에서 사용중인듯 합니다.

### 5. <a href="https://github.com/plotly/plotly.js">plotly / plotly.js</a>
자바스크립트 그래프 라이브러리입니다. Plot.ly라는 프로젝트의 일부이며, 해당 코드는 (진리의)  MIT 라이선스로 배포되었습니다. 샘플 차트는 여기서 확인하실 수 있습니다: <a href="https://plot.ly/javascript/">https://plot.ly/javascript/</a>

## 마무리
이번주 가장 기억에 남는 Repository는 두가지네요. Microsoft가 오픈소스계에 한발짝 더 다가서는 Milestone이 될 `Visual Studio Code`, 그리고 상당히 황당하고 재밌었던 `Hacker Script`. 이 두가지가 제일 기억에 남습니다. 특히나 `Hacker script는 웃기기는 하지만 한편으로는 저도 구현해서 사용해보고 싶을 만큼 매력적이네요. (저희 회사 커피머신은 네트워크에 연결되어있지는 않습니다만...)