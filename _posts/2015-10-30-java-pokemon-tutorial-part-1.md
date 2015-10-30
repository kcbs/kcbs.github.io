---
layout: default
title: [JAVA Tutorial] 포켓몬 게임을 만들어보자!! Part 1
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

    Result:
    Hello, World!
Hello, World! 느님을 영접할수 있는걸 보니 프로젝트 셋업은 아주 완벽한듯 하다! 여기서 조금 더 나아가어 창을 하나 띄워서 거기에 Hello, World!를 띄워보도록 하자. 일단 윈도우를 띄우기 위해서 `Swing` 라이브러리를 사용하도록 한다. `Swing`은 기본으로 포함되어있는 라이브러리이므로 부담없이 사용하도록 하자.

사실 아직 swing의 어떤 부분을 중점적으로 사용할지 모르므로, 일단 아래오 같이 import해주기로 한다. eclipse와 같은 IDE들에서는 알아서 import해주는 경우가 많기 때문에 이부분은 넘어가도 된다.

    import javax.swing.*;
이렇게 import 해주므로써 swing의 모든 모듈을 전부 import해준것이 되었다. 물론 비효율적이므로 코드가 완성된 후에 필요한 부분만 import해주는 식으로 바꾸는 것을 추천한다.

일단 메인 윈도우를 만들기 위해서 JFrame 오브젝트를 만들고 띄워보자.

    JFrame frame = new JFrame();
    frame.setSize(400,400);
    frame.setvisible(true);
이렇게만 해주면 기본적인 윈도우 창 하나를 띄워줄 수 있다. 물론 안에는 아무것도 없이 그냥 기본적인 회색의 창만 뜰 것이다.
여기에 Label을 추가해보자.

    JFrame frame = new JFrame();
    JLabel label = new JLabel("Hello, World"); // NEW:"Hello, World!"라고 적힌 label을 생성.
    frame.add(label); // NEW: frame에 label을 추가.
    frame.setSize(400,400);
    frame.setvisible(true);
그리고 실행해보면 아름다운 `Hello, World!`가 적힌 창 하나가 우리를 기다릴 것이다.

이제 다음 단계로 넘어가보자. 포켓몬스터 레드의 경우에는 필드의 배치가 아래와 같다:

<img src="https://confessionsofagamergirldotorg.files.wordpress.com/2015/08/red.gif">

가로 10칸, 세로 9칸으로 구성되어있으며 플레이어는 좌측 상단을 기준으로 (5,5)의 위치에 존재한다. 우리는 타일 한칸을 40x40으로 정해둘 것이며, 따라서 총 윈도우의 크기는 400x360이 된다. 이에 따라서 코드를 수정하자.

     frame.setSize(400,360);
그리고 기본적인 panel을 보여주기 위해서 grid layout을 이용해서 칸을 10x9로 나눠주자.

    JFrame frame = new JFrame();
    JPanel panel = new JPanel(new GridLayout(10,9,0,0));
    frame.add(panel);
    frame.setSize(400,400);
    frame.setvisible(true);
