---
layout: tutorial
title: Github Pages로 개인용 블로그 만들기 - 기초편
category: Tutorial
tags:
- Tutorial
- Jekyll
- Github
---

{% include github-page.html %}

## Github Pages란?
<a href="https://github.com">Github</a>은 다양한 서비스를 제공하고 있다. 가장 기본적인 Git 서버부터 시작해서 코드 Snippet 서비스인 Gist까지. 빠르고 안정적인 서비스들을 제공하며 오픈소스의 선두주자로 우뚝 나아가고 있다. Github이 제공하는 사이트들 중에는 상당히 눈여겨볼만한게 한가지 있는데, 그것이 바로 Github Pages이다.

Github Pages는 깃헙에서 제공하는 무료 웹 호스팅이라고 볼수 있다. 물론 무료이니만큼 상당한 제약이 걸리게 되는데, 눈여겨볼만한것들은

1. 소스코드가 전부 공개된다.
2. **정적 웹사이트만 만들수 있다.** (서버 언어 사용 불가능)

상당히 제한적이기 때문에 상호간의 소통을 요구하는 게시판 등의 웹사이트를 돌리는 것은 원천적으로 불가능하지만, **블로그**와 같은 개인용 사이트는 충분히 만들어낼 수 있다.

[[ad]]

## 시작하기

> 여기서는 일단 **Github 아이디가 존재**하고 **Git command line이 사용 가능**하다는 가정 하에 설명합니다.
> 
> 아래 예시들은 모두 Bash shell을 이용합니다. 윈도우 사용자분들은 Cygwin을 사용하시거나 아래의 코드들을 자체적으로 윈도우 cmd 코드로 변환해서 적용해주세요. Git 커맨드들은 윈도우/리눅스 공용이므로 그대로 적용시켜도 됩니다.

우선 깃헙 메인 페이지에서 New Repository를 클릭하여 새로운 Repository를 만들어야 한다. 여기서 주의할 점이 있는데, **Repository의 이름이 무조건 USERNAME.github.io의 형식**이여야 한다는 것이다. 따라서, **한 계정당 Repository는 하나**만 만들 수 있다.

    올바른 예시:
    Github ID: kcbs
    Repository name: kcbs.github.io
    
    잘못된 예시
    Github ID: kcbs
    Repository name: myawesomeblog.github.io

Repository를 만들었으면 기본적인 세팅은 사실 끝이다. Command line을 이용해서 기본적인 파일 하나를 업로드해보자.

    
## Hello, World!

우선 디렉토리를 하나 만들어야 하는데, 원하는 곳에 원하는 이름으로 만들자. 여기서는 임의로 **~/USERNAME.github.io/**라는 디렉토리를 만들고 이곳을 git 저장소로 사용한다.

    mkdir ~/USERNAME.github.io
    cd ~/USERNAME.github.io

그 후, 간단한 html파일을 만들어보자. 파일 이름은 index.html이 될 것이다.

    <!DOCTYPE html>
    <html>
        <head>
            <title>Hello, World!<head>
        <head>
        <body>
            <h1>Hello, World!<h1>
        </body>
    </html>

이제 방금 만든 파일을 업로드 해보자. 마찬가지로 git을 사용할 것이며, 아래의 Github 주소는 각자의 Github 주소로 치환하면 된다.

    git init
    git add index.html
    git commit -m "initial commit"
    git remote add origin "https://github.com/USERNAME/USERNAME.github.io.git"
    git push -u origin master

여기까지 끝내고 다시 웹사이트로 돌아가보면 아래와 같이 index.html이 push되어 있는 것을 확인할 수 있다.

이제 `USERNAME.github.io`로 접속해서 실제로 잘 작동하는지 확인해보자.

Hello, World가 뜨는걸 확인하면서 Github Pages가 제대로 확인중이라는것을 확인할 수 있다. github.io는 기본적으로 html과 함께 Markdown 파일( .md 파일)도 지원한다. 이 파일은 Github에서 README.md에서 사용하는 마크다운과 같으며, html을 잘 모르는 사람들도 쉽게 문서를 꾸밀 수 있도록 되어있다.

## 다음 단계는?

사실 html, css, js, 이미지파일 등을 업로드하고 호스팅되는 시점에서 기본적으로는 누구나 간단한 정적 페이지를 만들 수 있게 된다. 하지만 Github Pages는 거기서 한층 더 나아가서 Jekyll이라는 컴파일형 정적 사이트 생성기를 지원한다. 이것을 통해서 반쯤은 동적인 사이트를 만들 수 있게 되며, 간단한 카테고리 시스템, 템플릿 등을 사용할 수 있게 된다.

이 Jekyll을 이용하는 방법은 <a href="/tutorial/2015/11/24/Github-Pages-Jekyll">다음 포스팅</a>에서 설명한다.