---
layout: default
title: JAVA Tutorial: 포켓몬 게임을 만들어보자!! Part 1
tags:
- Java
- Pokeon
- Game
---
<img src="http://vignette4.wikia.nocookie.net/pokemon/images/1/1d/RedBox(J).jpg/revision/latest?cb=20110309010330">
## Introduction
전설의 게임, 포켓몬스터 적/녹 버전이 출시된지 거의 20년이 다 되어간다.
게임보이의 기기 한계상 복잡하고 화려한 그래픽을 연출할수는 없었지만 그 특유의 게임 시스템만큼은 지금까지도 유지되고 있다. 아직까지도 적/녹 버전을 플레이하는 유저들은 상당수 보이고 있으며, 본 버전에 나온 151마리의 포켓몬들은 아직까지도 현역으로 인기를 유지하고 있을 정도이다.

필자는 이 게임에서 주목할만한 점은 바로 OOP를 배우는데 특화되어있는 것이라고 생각한다. 플레이어, 맵의 오브젝트, 포켓몬, 기술, 아이템들이 전부 오브젝트로 나뉘어있고, 따라서 OOP기법으로 간단하게 재현해낼수 있다. 물론, OOP를 최대한으로 활용하는 JAVA를 배우는데도 당연히 좋은 튜토리얼이라고 생각된다.

**...애초에, 만들면서 재미있을 것 같다...**

## > 시작하기
IDE등은 알아서 골라오자. 아무것이나 써도 불편한것은 없으며, 필자는 그냥 서브라임이나 Vim이나 이클립스를 그때그때 끌리는걸 사용하고 있다.

일단은 크게 두 파트로 코드를 나눈다. 그래픽을들을 다루는 View부분과 게임 뒤쪽의 시스템을 다루는 System으로 나눈다. 따라서, 아래와같이 두개의 package를 만들어 주었다:

    1. com.kcbs.pokemonr.system
    2. com.kcbs.pokemonr.view

그리고 system에 Main.java 파일을 만들고, 아래와같이 main 메소드를 적어서 Hello, World! 느님을 영접해보자:
{% highlight java %}
    package com.kcbs.pokemonr.system;
    
    public class Main {
            public static void main(String[] args) {
                    System.out.println("Hello, World!");
            }
    }
{% endhighlight %}
