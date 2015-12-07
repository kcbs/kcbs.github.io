---
layout: default
title: Git 사용법을 배워보자 - Branch 편
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
- Branch
- 브랜치
---
{% include tutorial-git.html %}

## Branch란?
Branch기능은 Git을 팀 프로젝트의 버전컨트롤 시스템의 대세로 만들어준 일등공신입니다. Branch란 같은 프로젝트 내에서 여러가지 세부 프로젝트들을 관리할 수 있게 해주는 시스템입니다. 간단히 말하면, repository를 두가지 이상으로 "복사"한 후에, 추후에 다시 합쳐줄 수 있는 기능입니다. 이 기능이 효과적으로 쓰일 수 있는 이유는 바로 여러 사람들이 각각의 기능을 제작하고, 그것을 다시 원래의 메인 Branch로 합칠 수 있다는 점이기 때문입니다. 아래의 그림을 한번 봅시다.

<img src="">

위의 이미지에서 Master라고 적혀있는 부분이 바로 이 Repository의 메인 저장소입니다. 그리고 A라고 적혀있는 부분은 바로 A라는 세부 프로젝트를 표현하죠. Master에서 A로 분리될때 기본적으로는 그대로 모든 코드를 복사해오게 됩니다. 그리고 A라는 공간에서 여러번 Commit이 일어나는군요. 그리고 마지막으로 A를 다시 Master로 합쳐주는군요. 그 사이에 Master에서도 몇번 Commit이 일어났었지만, 상관 없습니다. Git이 기본적으로는 Merge를 수행해주기도 하며, 프로그램상으로 Merge하기 힘든 경우, 유저에게 수동으로 Merge하도록 유도해줍니다.

## 기본 Git Repository 셋업
쉬운 설명을 위해, 간단한 repository를 만들어봅니다.
	git init
	echo "TEST" > test.txt
	git add test.txt
	git commit -m "initial commit"
이로서 test.txt파일 하나를 담고있는 Repository가 만들어졌군요. 이제 이 Repository를 이용해서 여러가지를 해볼겁니다.

## Branch 만들기
우선 시작하기 전에 현재 Repository의 Branch Tree를 확인하는 방법을 먼저 보고 넘어갑시다.

	git log --graph --oneline --decorate --date=relative --all

위의 커맨드를 입력하면 커맨드라인에서 Repository를 확인할수 있습니다. 앞으로 자주 사용하게 될 커맨드이니, 아래를 입력해서 `alias`를 만들어둡시다.
	
	alias git-graph ='git log --graph --oneline --decorate --date=relative --all'

이렇게 입력해두면, 앞으로 `git-graph`만 입력하면 현재 Repository의 Branch Tree를 확인할 수 있게 됩니다. 일단 현재 상태에서 그냥 그래프를 확인해봅시다.

	* 5064cd2 (HEAD -> master) initial commit

이렇게만 뜨는군요. HEAD는 간단하게 현재 어떤 Branch를 사용하는지를 나타내고 있는 것이라고 생각하시면 됩니다. 

자, 이제 본격적으로 Branch를 만들어보도록 합시다. 우리가 만들 Branch는 **"Test2"**라는 Branch이며, test2.txt를 만드는 프로젝트(?)입니다. 자, 일단은 Branch를 만들려면 아래의 커맨드를 입력하면 됩니다.
	
	git branch <BRANCH_NAME>

우리의 경우에는
	
	git branch Test2

라고 하면 되겠네요. 그럼 이제 `git-graph`로 현재의 그래프를 확인해봅시다.

	git-graph
	* 5064cd2 (HEAD -> master, Test2) initial commit

아직까지는 master와 Test2가 완전히 같기 떄문에 별다른게 보이지 않습니다. 확인해보시면 `HEAD -> master`라고 되어있기 때문에, 아직은 우리는 Test2가 아닌 master Branch에 있습니다. Test2를 만들기만 하고 이동을 하지 않았기 때문인데요, 한번 Test2로 이동을 해봅시다.

## Branch Checkout하기

	git checkout <BRANCH_NAME>

위의 커맨드를 입력하면 해당 Branch로 이동하게 됩니다. 한번 해볼까요?

	git checkout Test2

그래프를 확인해봅시다.

	git-graph
	* 5064cd2 (HEAD -> Test2, master) initial commit

이제 HEAD가 Test2로 이동했군요. 우리의 목적대로 `test2.txt`를 만들 수 있을 것 같습니다.

## Tets2 Branch에서 작업하기
지금까지 해왔던대로 Test2에 여러가지를 해봅시다. `test2.txt`를 만들고 그것을 commit할겁니다.

	echo "TESR2" > test2.txt
	git add test2.txt
	git commit -m "add test2.txt"

자, 이제 test2를 만들었군요. 아차, 확인해보니까 `test2.txt`에 오타가 있군요. `TESR2`라고 적혀있습니다. 이걸 고치기 위해서 한번 더 commit을 해보겠습니다.

	echo "TEST2" > test2.txt
	git add test2.txt
	git commit -m "fixed typo in test2.txt"

자, 이제 오타도 고쳐졌겠다, 그래프를 확인해봅시다.
	
	git-graph
	* 97300f2 (HEAD -> Test2) fixed typo in test2.txt
	* 63424e0 add test2.txt
	* 5064cd2 (master) initial commit

흠, 이제 `Test2`가 `master`보다 두개 commit 앞서있는 것을 볼 수 있습니다. 이 상태에서 다시 master가 가르키고 있는 `5064cd2`로 돌아가 봅시다. 단순하게 `master` branch를 체크아웃하면 되겠네요.
	
	git checkout master

그리고 파일을 확인해보면...
	
	ls -l
	total 8
	-rw-r--r--  1 KCBS  staff  5  6 Dec 00:20 test.txt

`test2.txt`가 없이 `test.txt`만 보이는군요. `test2.txt` 파일은 `master`에는 존재하지 않는 파일이니까요. 자, 여기서 `test.txt` 파일을 약간 수정하고 commit을 해봅시다. 이번에는 `Test2`가 아닌 `master`에서요. `Test2`는 `test2.txt`파일을 위한 branch이기 때문에 `test.txt`의 수정에는 적절하지 않으니까요.

	echo "NEW LINE" >> test.txt
	git add test.txt
	git commit -m "Fixed test.txt"

자, 그러면 이제 `master`와 `Test2`가 서로 각자의 노선을 가는군요. 두 branch는 같은 시점에서 분기되었지만, 서로가 다른 수정을 했습니다. 이제 이 두 branch의 그래프를 확인해볼까요?
	
	git-graph
	* cd2ad9b (HEAD -> master) Fixed test.txt
	| * 97300f2 (Test2) fixed typo in test2.txt
	| * 63424e0 add test2.txt
	|/  
	* 5064cd2 initial commit

오호, 이제 그래프가 조금 복잡해졌습니다. `5064cd2`, 즉, 두 Branch의 분기점을 기준으로 두개가 쫙 나뉘어버렸네요. 왼쪽은 `master`, 오른쪽은 `Test2`를 보여주고 있습니다.

## 브랜치 Merge
이제 각각의 Branch들이 할일을 다 했으니, 두개를 도로 합쳐야 할듯 합니다. 두개를 도로 합치기 위해서 우선 master로 갑시다.

	git checkout master

이 상태에서, 다른 브랜치를 합치려면 아래의 커맨드를 이용하면 됩니다.
	
	git merge <BRANCH_NAME> -m "<MESSAGE>"

우리의 경우에는

	git merge Test2 -m "Merging Test2"

가 되겠네요. 자, 이제 두개의 파일이 합쳐졌습니다. 현재의 폴더 상황과 파일의 내용물을 확인해보죠.

	ls -l
	-rw-r--r--  1 KCBS  staff  14  6 Dec 00:37 test.txt
	-rw-r--r--  1 KCBS  staff   6  6 Dec 00:40 test2.txt

	cat test.txt
	TEST
	NEW LINE

	cat test2.txt
	TEST2

보시다시피 `master`와 `Test2`의 변경내역이 모두 합쳐져 있군요! 성공입니다. 이제 이 상태의 그래프를 확인해봅시다.

	git-graph

	*   44535b8 (HEAD -> master) Merging Test2
	|\  
	| * 97300f2 (Test2) fixed typo in test2.txt
	| * 63424e0 add test2.txt
	* | cd2ad9b Fixed test.txt
	|/  
	* 5064cd2 initial commit

보시는대로 `44535b8`버전에서 `master` branch가 `Test2` branch를 흡수한 것이 보여집니다. 이로서 `Test2`라는 서브프로젝트는 끝이 났군요.

## 마치며
실제 개발 환경에서는 메인스트림이라고 불리우는 Branch들이 존재합니다. 이번 시간에는 `master`를 메인, `Test2`를 서브로만 두고 진행했지만, 실제 개발할떄는 대부분 `release`, `beta`, `alpha`, `dev` 등등을 두고 작업을 하고, `dev`를 `alpha`로 merge하고, 또 그걸 테스트 후에 `beta`로, 그리고 또 테스트 후에 `release`로 merge해가면서 진행하게 됩니다. 물론, 여러가지 프로젝트들도 나뉠수 있고요.

다음시간에는 Git 자체보다는 Github과의 연동에 대해서 조금 더 자세히 다뤄볼 예정입니다. Github이 개발자들의 성지가 되어가고 있는 만큼, 사용법을 알아두면 더 좋을 것 같습니다.