---
layout: default
title: Github Pages로 개인용 블로그 만들기 - Jekyll편
category: Tutorial
tags:
- Tutorial
- Jekyll
- Github
---

{% include github-page.html %}

## 시작하며

지난 시간에는 기본중의 기본인 github pages 저장소만 만들어봤다. USERNAME.github.io로 이름지어진 이 페이지는 Github이 알아서 해당 주소로 사이트를 올려주게 된다. 근본적으로는 `static site`이기 때문에 서버사이드 코드는 전혀 사용할 수 없으며, 이 특성때문에 사실은 블로그로 활용하기 애매해진다.

이 단점을 극복할 수 있는 방법이 있는데 바로 `Jekyll`이다. <a href="http://jekyllrb.com/">`Jekyll`</a>이란 루비를 사용한 "컴파일형" static website 제작 라이브러리이다. 웹사이트의 component들을 따로따로 만든 후에 컴파일을 해서 스태틱 웹사이트를 만들어주는 방식이다.

예를들어, Navigation Bar부분의 html코드를 따로 만들고, Footer부분을 따로 만들고, 본문 부분을 따로 만들어보자. 그리고 Jekyll을 이용해서 저 세개를 하나로 이어붙여주는 방식을 취하게 되는 것이다.

여느 Template 시스템들과 같이 `include`, `filter`등을 다 지원하며, 당연하게도 DB 지원은 하지 않는다. 그럼 일단 아주 간단한 웹사이트를 하나 만들어보자.

## Jekyll 기본 설정

### _config.yaml
우선 이전 시간에 만든 repository의 루트에 `_config.yaml`이라는 파일을 만들어보자. 이 파일은 Jekyll의 컴파일 설정을 담게 되며, 나중에 소스코드를 업로드하면 Github Pages측에서 알아서 이 파일을 참조해서 컴파일을 실행하게 된다.

우선은 안에는 별다른 내용은 넣지 말고 이정도만 넣어주자:

    name: [WEBSITE NAME]
    description: [WEBSITE DESCRIPTION]
    markdown: redcarpet

### _layouts
그다음은 layout이다. 간단히 그냥 블로그 페이지의 html 코드를 만든다고 생각하면 된다. 포스팅별로 달라지는 것은 단순히 본문의 글과 제목 뿐이며, 따라서 베이스가 되는 html코드는 하나 뿐이라고 보면 된다. 우선 샘플로 아래와 같은 html코드가 있다고 생각하자.

	<html>
		<head>
			<title>[WEBSITE NAME]</title>
		</head>
		<body>
			<div class="navbar">NAVBAR</div>
			<div class="post">
				<div class="post-title">[POST TITLE]</div>
				<div class="post-body">
					[POST BODY]
				</div>
			</div>
			<div class="footer">FOOTER</div>
		</body>
	</html>

이 html 코드에서 몇몇부분은 Jekyll의 변수로 대체할수 있는데, 우선 `[PAGE TITLE]` 부분은 우리가 _config.yaml에서 설정했기 때문에 `{{ site.title }}`로 바꿔줄수 있고, `[POST TITLE]`은 `{{ page.title }}`, 그리고 마지막으로 `[POST BODY]`는 `{{ content }}` 로 적어줄 수 있다. 이렇게 하면 추후에 Jekyll이 컴파일하면서 알아서 각각의 변수들을 상황에 맞게 변화해서 저장해주게 된다. 이러한 식으로 변화시킨 다음에 `_layouts` 폴더를 만들고 그 안에 넣어주면 된다. 해당 layout의 이름은 `default`로 정하도록 한다.

	<html>
		<head>
			<title>{{ site.title }}</title>
		</head>
		<body>
			<div class="navbar">NAVBAR</div>
			<div class="post">
				<div class="post-title">{{ page.title }}</div>
				<div class="post-body">
					{{ content }}
				</div>
			</div>
			<div class="footer">FOOTER</div>
		</body>
	</html>

	/_layouts/default.html

### _includes

위의 html코드를 보면 사실은 `<div class="post">`의 윗부분과 아랫부분은 사실 **어떤 페이지에서도 동일하다**는것을 알 수 있다. POST부분은 각 페이지에 따라서 조금씩 달라질 수도 있지만 네비게이션 바와 Footer는 변할 이유가 없기 때문이다. 따라서 저 두 부분을 따로 빼둘 수 있게 된다.

우선 _includes 폴더를 만들고, 그 안에 아래와 같은 두 파일을 만들어서 넣어보자.

	<html>
		<head>
			<title>{{ site.title }}</title>
		</head>
		<body>
			<div class="navbar">NAVBAR</div>
	
	/_includes/header.html

	<div class="footer">FOOTER</div>
		</body>
	</html>
	
	/_includes/footer.html

그리고 아래와 `_layouts/default.html`을 아래와 같이 변형시켜주자.

	{% raw %}{% include header.html %}{% endraw %}
	<div class="post">
		<div class="post-title">[POST TITLE]</div>
		<div class="post-body">
			[POST BODY]
		</div>
	</div>
	{% raw %}{% include footer.html %}{% endraw %}

	/_layouts/default.html

이렇게 하면 알아서 header와 footer를 Jekyll이 이어붙여주게 된다.

### _posts

이제 기본적인 Layout은 끝났다. 실제로 포스팅을 써볼 차례이다. 포스팅을 쓰는 방법은 간단한데, 우선 `_posts` 폴더를 만들면 된다. 그리고 그 안에 html, md등의 포맷으로 글을 쓰면 된다. 물론, html파일의 경우, "헤더/footer를 제외한 **본문만**" 써야 한다.

주의해야 할 점은 포스팅 파일의 맨 위에는 **무조건** 아래와 같은 부분이 존재해야 한다.

	---
	layout: default
	title: Github Pages로 개인용 블로그 만들기 - Jekyll편
	---

layout 파일을 위에서 만든 default로 정해준다는 의미이고, 현재 페이지의 타이틀을 저렇게 지정해준다는 의미리다. 페이지의 타이틀이 지정되어있지 않은 경우에는 **파일의 이름**이 자동으로 페이지의 타이틀이 설정된다.

이 부분이 존재하지 않으면 제대로 컴파일이 되지 않으니 주의하자. 물론 layout이나 title을 특정하지 않아도 상관은 없지만, 그런 경우에도 무조건 아래와 같은 형식으로나마 저 부분이 존재해야 한다.

	---
	---

HTML이던 MD던 블로그 포스팅을 하는데는 큰 상관이 없지만, 개인적으로는 MD를 추천한다. MD파일은 `Markdown`파일로, 제일 보편적으로 사용되는 곳은 다름아닌 Github이다. Github Repository를 돌아다니다 보면 `README.md`파일로 간단히 해당 repository 설명이 적혀있는 것을 볼 수 있다. md파일은 파일을 최소한의 문법으로 decoration할수 있게 해주는 일종의 "Markup Language"로, 자세한 설명은 추후의 포스팅에서 다루도록 한다.

Jekyll은 어떤 타입이던 다 받기 때문에 더 편한 쪽을 사용하면 된다.

### 마무리

이렇게 하고 나면 기본적인 블로그 세팅은 끝이다. 나머지는 header/footer부분에 자신이 원하는 디자인을 추가하는 것 뿐이다. `kcbs.github.io`의 경우에는 기본적으로 `Bootstrap`을 이용한 베이스에 필자의 조잡한 미술감각을 곁들여서 만들어졌다. 이 글을 일고계실 독자분들은 적어도 이 블로그보다는 훌륭한 디자인을 만들어낼 수 있으리라 믿는다(...)