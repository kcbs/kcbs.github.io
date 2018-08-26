---
layout: default
title: Heroku를 사용하여 node.js 서버 제작하기
category: Tips
tags:
- tip
- heroku
- nodejs
---

## Heroku란?

최근에 클라우드 서비스가 많이 부각되고 있습니다. 아마존의 AWS, 마이크로소프트의 Azure 등의 서비스를 필두로 다양한 클라우드 제공 회사들이 등장하고 있습니다.

그중, 핫한 클라우드 서비스가 있는데, 바로 `Heroku`라는 서비스입니다!

이 클라우드 서비스는 PaaS (Platform as a Service)를 제공하기 때문에 가벼운 어플리케이션 서버를 제작하여 올리기 적합합니다. 다양한 언어를 지원하고 있기 때문에 원하는 언어를 업로드해서 서비스 할 수 있습니다. 본 글에서는 간단한 `Node.js` 서버를 만들어서 올리는 방법에 대하여 알아보겠습니다.

## 다운로드
 * heroku CLI: https://devcenter.heroku.com/articles/heroku-cli
 * git client: https://git-scm.com/
 * node.js: https://nodejs.org/ko/

## node.js App 만들기

우선, Node.js Application을 만들어야 합니다. 다음 명령어를 사용하여 초기화시켜줍시다.

```shell
mkdir helloheroku
npm init
```

`npm init` 명령어를 사용하면 다양한 질문이 쏟아지는데, App의 이름 등을 입력하게 됩니다. 귀찮을 경우, 꼭 필요한 항목만 빼고 다 그냥 엔터 키를 눌러 넘겨버려도 됩니다.

짜잔! 간단한 Node.js Application이 만들어졌습니다.

## Express 앱 만들기

이제 Node.js 어플리케이션을 웹 서버로 만들기 위하여 express 모듈이 필요하게 됩니다. 아래 명령어를 실행해봅시다.

```shell
npm install express
```

잠시 기다리면 express가 설치 완료 될 것입니다.

이제 helloheroku 폴더에 엔트리포인트로 `index.js` 파일을 만들고, 아래와 같은 내용을 입력하여 봅시다.

```javascript
var PORT = process.env.PORT || 8080;

var express 	= require('express');
var app 	= express();

app.get('/', function(req, res) {
	res.send('Hello, World!');
});

app.listen(PORT, function() {
	console.log('HTTP Server opened on port ' + PORT);
});
```

간단하게 "Hello, World!"를 프린트하는 app을 만들어봤습니다. 자, 이제 `package.json`을 수정하여 "start" 스크립트를 만들어줍시다.

```json
{
	"name": "helloworld",
	...
	"scripts": {
		"start": "node index.js"
	}
	...
}
```

자, 이제 node.js app은 준비가 완료된 듯 합니다.

## Heroku app 만들기

우선, Heroku 로그인을 해봅시다. 아래 명령어를 실행합니다.

```shell
heroku login
```

아이디와 패스워드를 입력해주면 heroku에 로그인이 되었을 것입니다. 이제부터 실행하는 모든 heroku 명령어들은 로그인 되어있는 계정에 대하여 실행되게 됩니다.

Heroku는 git을 활용하여 소스코드를 업로드 하게 됩니다. 즉, 아까 만들어둔 app을 git repository로 만들 필요성이 생깁니다.

```shell
git init
```

이제 heroku 서버에 우리의 App을 만들 컨테이너를 생성해야 합니다. 아래와 같은 명령어를 실행하여 만들 수 있습니다. `APPNAME`은 원하는 이름으로 설정합시다.

```shell
heroku create APPNAME
```

짠! 잠시 기다리면 `Creating example... done` 이라는 말이 나오며 Heroku 서버에 서비스가 생성되게 됩니다. 이제 아까 만든 App을 업로드만 하면 될 듯 합니다!

```shell
git add -R .
git commit -m "Initial Commit"
git push heroku master
```

마지막 push 명령어를 실행하면 git remote에서 많은 메시지들이 출력되는 것을 볼 수 있는데, heroku 서버에서 방금 올린 소스코드를 빌드하는 메시지들입니다. 코드에 오류가 있을 경우 BUILD가 실패하게 되며, 메시지에서 확인할 수 있습니다.

## 테스트하기

만들어진 App은 웹브라우저에서 `http://APPNAME.herokuapp.com`로 접속하면 확인할 수 있게 됩니다.  접속하면 다행히도(!) 우리가 만든대로 'Hello, World!'라는 메시지가 출력됩니다.


