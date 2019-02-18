---
layout: post
title: React 튜토리얼 기초 [2]
image: https://upload.wikimedia.org/wikipedia/commons/thumb/1/18/React_Native_Logo.png/800px-React_Native_Logo.png
comments: true
category: tutorial
tags:
  - Programming
  - Tutorial
  - React
  - Javascript
---

지난 강좌에서는 기초적인 React의 개념에 대해서 살펴보았다. 사실 이해를 못하고 넘어와도 된다. 앞으로 진행될 강좌를 따라가다보면 어느정도의 감은 잡힐 것이다... 라고 믿고 있다.

자, 우선 기본적인 환경설정을 해보자. 필자는 사실 환경설정 하는 방법에 대한 글을 작성하는게 제일 좋다. 별다른 설명이 필요 없기 때문이다. 머리 쓸 필요 없이 아래 나오는 설명들을 따라해보도록 하자.

## node.js 설치

설치는 Ubuntu 14.04 LTS 버전을 기준으로 진행하도록 한다.

자, 우선 당연히 node.js 서버를 설치해야된다. 그 전에, nvm을 이용하여 더 정확한 node.js 버전컨트롤을 진행할 수 있도록 세팅해보자.
~~~bash
sudo apt-get update
sudo apt-get install build-essential checkinstall libssl-dev
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
~~~

이제 bash를 재시작 하면 nvm을 사용할 수 있다. nvm을 사용하여 현재 사용되는 LTS 버전인 10.15.1 버전을 설치하자.

~~~bash
# input
nvm install 10.15.1
~~~

~~~bash
# output
Downloading https://nodejs.org/dist/v10.15.1/node-v10.15.1-linux-x64.tar.xz...
######################################################################## 100.0%
Now using node v10.15.1 (npm v6.4.1)
Creating default alias: default -> 10.15.1 (-> v10.15.1)
~~~

짜잔! 이제 node(v10.15.1)과 npm(v6.4.1)이 제대로 설치되었을 것이다!


## create-react-app 설치

자, 이제 react 프로젝트를 간단히 생성할 수 있도록 도와주는 create-react-app을 설치해보자. create-react-app은 npm을 사용하여 간단히 설치할 수 있다.

~~~bash
npm install -g create-react-app
~~~

-g 옵션을 통하여 nodejs global 앱을 서버에 설치하였다. 이제 bash 쉘에서 create-react-app이라고 치는 것으로 간단한 react 프로젝트가 생성 가능하다.


## 프로젝트 생성

~~~bash
create-react-app tutorial-project
~~~

더이상의 설명은 필요 없을 것이다. 정말 위의 명령어만 치면 프로젝트 폴더가 자동으로 생성되고 모든 dependency가 설정되게 된다.


## 프로젝트 실행

이제 모든 준비가 끝났다. create-react-app으로 생성된 프로젝트를 실행해 보는 일만 남았다.

~~~bash
cd tutorial-project
npm start
~~~

`npm start` 명령어를 사용하면 `Starting t he development server...`라는 메시지가 나오고, 잠시 기다리면 `Compiled successfully!`라는 메시지와 함께 접근할 수 있는 주소가 나오게 되고, 사용하는 브라우저를 사용해서 해당 주소에 접근하면 다음과 같은 화면이 보이게 된다.



## 마치며

자, 이제 모든 세팅이 끝났다. 다음 글에서는 이제 react의 기초부터 설명해가면서 진행해야 된다. 벌써부터 막막하다. 최대한 쉽게 쓰는 것을 목표로 하고 있기 때문에 우리 착한 독자 여러분은 그냥 따라오기만 하면 될 것이다. 이해가 안가는 부분은 다른 사람들의 블로그를 참고하길 바란다. 잔뜩 나올 것이다...


