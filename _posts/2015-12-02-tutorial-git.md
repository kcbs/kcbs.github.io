---
layout: default
title: Git 사용법을 배워보자 - 기본편
category: Tutorial
tags:
- tutorial
- Git
- Github
keywords:
- Git
- howto
- Version Control
- 깃
- 짓
- 깃헙
- 버젼컨트롤
---
## Git이란?
얼마 전에 프로그래밍 커뮤니티에서 Git이 뭐냐고 물어보는 질문을 봤습니다. 꽤 많이 사용하고 있기 떄문에 답변을 하려 했는데 막상 하려니 어떻게 설명할지 미묘하더군요. 그래서 조금 길게라도 설명하고, 사용법을 설명해보려고 합니다.

Git은 여러 버젼컨트롤 시스템중 하나입니다. 다른 유명한 버전컨트롤은 SVN, CVS등이 있죠. 조금 흥미로운 점은... Git의 개발자는 바로 리눅스 개발로 유명한 리누스 토발즈입니다. 그의 말에 의하면 Git의 개발이 가장 쉬웠다고 하더군요. 버전 컨트롤이란 말그대로 코드의 버전 관리를 해주는 프로그램입니다. 코드가 변경될때마다 버전을 매기게 되고, 필요에 따라서 이전 버전으로 쉽게 되돌릴 수 있습니다.

단순히 버전을 되돌리는 것이 아니라, 팀 단위의 프로젝트도 지원하는데, 바로 "Branch"라는 기능으로 지원됩니다. Branch의 설명은 다음 시간으로 넘기고 우선은 기본적인 버전컨트롤 방법부터 살펴보도록 합시다.

## 설치하기
### Windows
윈도우에서의 Git 설치는 <a href="https://git-scm.com/download/win">여기</a>서 설치파일을 받을 수 있습니다. 설치중에 Command line 사용에 체크해주세요.

### Linux
보편적인 apt-get 서비스로 보면
	sudo apt-get install git
을 실행하면 됩니다.

다른 패키지 관리 툴에서도 "git"을 설치하시면 됩니다.

### OS X
제일 무난한 방법은 `XCode`의 command line tools를 설치하면 됩니다. `XCode`가 설치되어 있는 상태에서 아래 커맨드를 입력해 주세요.
	XCode-select --install

## 저장소 만들기
지금부터는 기본적으로 Unix 기반 운영체제를 기반으로 설명합니다. Git 커맨드들은 어디서나 동일하지만, Windows 유저분들은 그 외의 커맨드들을 알맞게 변형해서 사용해주시면 됩니다.

우선 아무 폴더나 만들어 봅시다. 여기서는 편의상 `~/git-test` 폴더를 만들겠습니다.

	mkdir ~/git-test
	mv ~/git-test

이제 이 폴더를 Git 저장소로 사용하게 될겁니다. Git 초기화 커맨드를 실행해서 만들어봅시다.
	
	git init

이제 이 폴더는 git 저장소로 활용되게 됩니다. git 저장소는 기본적으로 `.git` 폴더가 숨김 폴더로 존재하게 됩니다. 이 폴더는 여러 버전들의 정보를 가지고 있으며, git 시스템의 전부이기 때문에 삭제하시면 안됩니다.

## 파일을 Git에 추가하기
우선 파일을 만들어봅시다.

	echo "Hello Git" > test.txt

그 후, `test.txt` 파일을 Git에 추가합니다.

	git add test.txt

이제 test.txt파일은 다음 commit때 추가되게 됩니다.

만약 폴더 내의 모든 파일을 추가하고 싶다면 아래의 커맨드를 부르면 됩니다. 하위 폴더의 파일들까지 모조리 추가하며, 만약 파일이 이전 commit 시점부터 편하지 않았다면 무시됩니다.
	
	git add -A

## Commit
Commit은 이제 코드의 수정을 마치고 현재 상태를 저장할떄 사용합니다. 이전 commit시점부터 지금까지 add된 파일들만이 commit되게 되며, 간단한 메시지를 넣어야 합니다.
	
	git commit -m "Initial Commit"

"Initial Commit"부분은 아무렇게나 쓰셔도 되며, 지금은 최초로 commit하는 것이기 때문에 저렇게 써보겠습니다.

이제 코드가 저장되고 버전이 매겨졌습니다. 현재 Git 저장소의 버전은 아래의 커맨드로 확인할 수 있습니다.

	gitk


	* 5e7608e (HEAD -> master) Initial Commit

이라고 나오는군요. 제대로 commit되었나봅니다. 5e7608e는 Commit ID를 나타내며, 각각의 Commit, 즉 버전의 이름이 됩니다. 여러개의 Commit이 존재할 경우에는 `HEAD`라고 되어있는 버전이 바로 현재 버전을 가르킵니다.

## 파일 수정하기/되돌리기
그럼 파일을 수정해봅시다. `test.txt`파일을 수정해봅시다.

	echo " new part" >> test.txt

수정 후, 위에서 한 절차를 따라서 한번 더 commit해줍니다.
	
	git add test.txt
	git commit -m "second commit"

그러면 test.txt파일이 수정된 상태로 Git 저장소에 저장되게 됩니다. 이 상태에서 이제 현재 git 저장소를 보게 되면, 

	* 0d34691 (HEAD -> master) second commit
	* 5e7608e Initial Commit

이렇게 나오는군요. 아까와는 버전이 달라져있습니다. 이제 어떻게 이전 버전으로 돌아갈까요? 바로 `git checkout` 커맨드를 이용합니다. 기본적으로 특정 버전으로 돌아갈떄 사용하는 커맨드로, 아래와 같이 사용합니다.

	git checkout <tag/branch/commit id>

즉, 우리의 경우에는

	git checkout 5e7608e

라고 하면 `5e7608e`, 그러니까 "Initial Commit"으로 돌아갈 수 있게 되겠군요. 여기서 다시 "Second Commit"으로 돌아가려면

	git checkout 0d34691

라고 해주시면 됩니다.

### 끝내며
간단한 Git의 사용법을 둘러봤습니다. Init / Commit / checkout등을 살펴봤는데, 아직은 설명하지 않고 대충 넘어간 부분이 많군요. 다음에는 Branch에 대해서 설명할 예정입니다. Branch는 아무래도 Git의 제일 중요한 요소라서 별도의 포스팅에서 다루려 하는 것이니까 다음편도 꼭 봐주시면 좋겠네요 :)
 