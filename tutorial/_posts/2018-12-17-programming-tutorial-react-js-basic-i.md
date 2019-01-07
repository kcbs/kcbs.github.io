---
layout: post
title: React 튜토리얼 기초 [1]
image: https://upload.wikimedia.org/wikipedia/commons/thumb/1/18/React_Native_Logo.png/800px-React_Native_Logo.png
comments: true
category: tutorial
tags:
  - Programming
  - Tutorial
  - React
  - Javascript
---

이 글을 읽기 전에, 인터넷에 `React 강좌` 라고 검색을 한번 해보자. 매우 많은 강좌가 쏟아져 나올 것이다. 

대표적으로는 `velopert`님의 [누구든지 하는 리액트](https://velopert.com/3613), `NOMAD CODER`님의 [리액트 처음이시라구요? React JS로 웹 서비스 만들기!](https://www.inflearn.com/course/reactjs-web/) 등이 있을 것이다.

그럼에도 불구하고 이 글에 들어오신 여러분들은 아마도 위의 글들을 읽으면서 조금씩 이해가 잘 안갔던 부분이 있어서 들어온 것이리라 생각한다.

즉, 독자 여러분들은 본 강의를 강의 본편보다는 아마도 보충학습 정도의 마음가짐으로 가볍게 읽게 될 것이다.

물론 필자도 마찬가지다.

상기된 튜토리얼들을 읽으며 지식을 쌓아왔고, 이해가 가지 않았던 부분은 구글신의 도움을 받아 다양한 웹사이트에서 보충학습을 했다.

그렇기 때문에 매우 가벼운 마음가짐으로 글 작성을 진행하려 한다.

## React의 역사...

> 젠장!! 여..역사시간이다..!! 도망ㅊ..ㅕ.....

자... 우선 React가 왜 등장하게 되었는지 그 역사에 대하여 가볍게 살펴보도록 하자. 재미 없으면 그냥 바로 설치하는 챕터로 넘어가자... 필자는 슬프지 않다...

React는 우리들이 너무나도 잘 아는 '그 기업', Facebook에서 제작한 프론트엔드 프레임워크다.

Facebook을 사용해보신 분들은 알겠지만 대량의 데이터들이 하나의 뉴스피드 상에 잔뜩 동적으로 나타났다 없어졌다 하게 되어있다.
그러한 UI상의 특성상, Facebook은 다양한 데이터들을 관리해줄 중심 코어가 필요하게 되었고, 그 코어가 현재의 React가 되었다.

그 덕분에 우리는 Facebook에서 쓸데없이 많은 무의미한 뉴스들과 광고글들을 빠른 속도로 만날 수 있게 되었다. 하...

초기의 React는 현재와는 전혀 다른 모습이였다. Facebook에서는 2010년도에 PHP 기반이였던 Facebook 엔진을 편하게 작성하기 위하여 [Xhp](https://www.facebook.com/notes/facebook-engineering/xhp-a-new-way-to-write-php/294003943919/)라는 물건을 제작하여 발표하게 되는데, 이때 Xhp의 문법을 살펴보면 현재의 JSX와 비슷한 점이 많이 보일 것이다.

XHP 문법:
~~~php
if ($_POST['name']) {
  echo Hello, {$_POST['name']};
} else {
  echo
    <form method="post">
      What is your name?
      <input type="text" name="name" />
      <input type="submit" />
    </form>;
}
~~~

2011년도에 사실 React의 기본적인 프로토타입은 완성되어 사용중이였다. 자바스크립트를 활용한, 당시에는 [FaxJS](https://github.com/jordwalke/FaxJs)라고 불리던 놈이였는데, github 페이지를 보면 알겠지만 현재의 React와 상당히 흡사한 구조를 가지고 있다. 이 FaxJS는 페이스북의 검색엔진쪽에 활용되었다.

React는 2013년도에 처음으로 오픈소스로 공개되게 된다. 당시에는 프론트엔드쪽 라이브러리는 HTML + jQuery가 장악하고 있었기 때문에 사람들의 반응은 매우 좋지 않았다. React의 방식이 매우 비효율적으로 보였기 때문이다. 

초반의 안좋은 반응이 무색하게 React의 개념은 사람들의 마음을 조금씩 돌려놓았다. 그 가능성을 알아본 대형 기업들의 React 도입으로 매우 빠른 속도로 React는 그 규모를 키워나가게 된다.

결국 React Native, Redux, Immutable.js 등등 React와 관련된 다양한 사이드 프로젝트들이 등장하면서 2018년 현재는 매우 거대한 프레임워크가 되었다.

## React의 편의성

자, 지금까지는 React의 "역사"에 대하여 살펴보았다면 이제는 "기술"적인 측면을 이야기해보아야 할 때가 왔다.

예전의 재미없는 웹사이트들과는 다르게 현 세대의 웹 페이지들은 대부분 페이지가 동적, 즉 `dynamic`하게 동작하고 있다는 점이 중요한 요소다.

예를 들어, React의 본고장인 Facebook을 살펴보도록 하자. Facebook의 포스팅에서 댓글을 작성하는 경우, 페이지가 refresh되지 않고 방금 작성한 댓글이 바로 뜨게 된다.

이런 식으로 페이지의 새로고침 없이 페이지의 내용 및 디자인이 변경되는 것을 바로 `dynamic loading`이라고 한다.

지금까지 대부분의 웹 개발자들은 이러한 작업을 기본적으로는 HTML로 페이지를 작성한 후, 네이티브 javascript 혹은 jQuery와 같은 라이브러리를 사용하여 페이지 내용을 변경해주었다.

자바스크립트, 혹은 jQuery를 사용하여 아래와 같이 페이지의 DOM Element를 검색하여 가져오고 컨텐츠를 수정하면서 페이지를 변경해주어야한다.

~~~html
<script>
	// state
	var counter = 0;
	// when addBtn button is clicked...
	$("#addBtn").click(function() {
		// add 1 to counter
		counter += 1;
		// update counter DOM element
		$("#counter").html(counter);
	});
</script>
<div id="counter">0</div>
<button id="addBtn">+</button>
~~~

한번이라도 jQuery를 사용하여 개발해보신 분들은 알거다. 이 과정이 편리하긴 하지만 코드가 상당히 난잡해질 수 밖에 없다는 것을...

dynamic하게 변경될 DOM Element가 몇개 없는 경우에는 사실 이런 방식을 사용해도 무방...아니, 오히려 효율적일 수 있다.

하지만 많은 것이 변경되어야 하고, 그에 관련된 State도 많이 있다면? 그것을 전부 관리해야 한다면...? 우선... 음... 

> X를 눌러 조의를 표하고 갑시다.

React의 경우, 이러한 state를 각각의 component 오브젝트에 묶어서 표현하고 각 state가 업데이트 될 때마다 해당 DOM Element를 업데이트 할 수 있도록 하였다. 아래와 같이 말이다:

~~~javascript
class Counter extends Component {

	state = {
		counter: 0
	};
	
	addCounter() {
		this.setState({counter: this.state.counter + 1});
	}
	
	render() {
		return (
			<div>
				<div id="counter">{this.state.counter}</div>
				<button onClick={this.addCounter}>+</button>
			</div>
		);
	}
	
}
~~~

아직 위의 코드를 이해할 필요는 없다. 다만 중요한 것은, 위와 같이 각 state와 컴포넌트를 클래스화 하여 합쳐두었다는 것이다.

짜잔!! 이제 각 컴포넌트의 관리를 쉽게 할 수 있게 되었다!!

## 마치며

다음 시간에는 React의 기본적인 설치 방법과 폴더 구조 등을 살펴볼 예정이다. 사실 이번 1강의 경우에는 굳이 알아도 되고 몰라도 되도록 만들어두었다. 실제 실습이 진행되면서 왠만한 중요 설명은 같이 할 예정이기 때문이다. 다만, 알고 시작하는것과 모르고 시작하는 것에는 매우 큰 차이가 있기 때문에 어느정도의 지식 정도만 익혀두면 좋을 것 같다.

*[프론트엔드]: 유저에게 보여지는 화면(UI)에 관련된 개발작업