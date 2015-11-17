---
title: Java로 포켓몬을 만들어보자. Part 1
layout: default
tags:
- Java
- Tutorial
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


## 캔버스 세팅!

우선 `view` 패키지 안에 Surface.java를 만들었다. 이부분에거 기본적으로 화면에 보여지는 부분을 담당하게 되며, 우선은 그냥 필드부분만 처리하도록 만들어주자. 나중에 배틀뷰같은게 추가되면 그 역할을 하는 또다른 Surface를 만들어주면 된다. Surface.java는 기본적으로 JPanel을 extend하며, paintComponent(Graphics g) 메소드를 override해준다.

    public class Surface extends JPanel {
        private void doDrawing(Graphics g) {
            Graphics2D g2d = (Graphics2D) g;
            g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            for(int x = 0 ; x < 10 ; x++) {
                for(int y = 0 ; y < 9 ; y++) {
                    g2d.drawRect(x*40,y*40, 40,40);
                }
            }
        }
        @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            doDrawing(g);
        }
    }
위와 같이 해주면 JPanel의 Graphics2D를 이용해서 10x9의 사각형을 잔뜩 배치해줄수 있게 된다. 이제 `Main.java`로 돌아가서 위의 Surface를 생성하고 JFrame에 등록해보자.

    public class Main {
        public static void main(String[] args) throws InterruptedException {
            JFrame frame = new JFrame();
            Surface panel = new Surface();
            frame.setSize(400,383);
            frame.add(panel);
            frame.setVisible(true);
        }
    }
이걸로 JFrame이 생성되고 거기에 우리가 만든 custom JPanel인 Surface가 추가되게 된다. 실행해보면 예상한대로 정사각형 90개가 화면에 배치되는데, 이 하나하나의 칸이 포켓몬스터에서 맵 한칸 한칸이 될 것이다. 포켓몬스터 레드의 경우에는 필드의 배치가 아래와 같다:

<img src="https://confessionsofagamergirldotorg.files.wordpress.com/2015/08/red.gif">

가로 10칸, 세로 9칸으로 구성되어있으며 플레이어는 좌측 상단을 기준으로 (4,4)의 위치에 존재한다. 우리는 타일 한칸을 40x40으로 정해두었고 10x9의 패널을 이미 만들어놨다. 그럼 이제 해야할것을 무엇일까? 바로 **캐릭터의 배치**이다. 포켓몬스터 레드 버전의 캐릭터의 위티인 (4,4)에 이미지를 넣어보자. 이미지의 입출력은 다음 포스팅에서 다룰 예정이며, 지금은 단순하게 검게 채워져있는 원 하나를 캐릭터라고 가정하도록 한다.


## 캐릭터 생성!

우선 캐릭터 클래스를 만들어야 한다. 캐릭터는 System에 속하기 때문에 system 패키지 안에 Character 클래스를 만들자. 캐릭터가 가지고 있어야 할 기본적인 요소가 무엇일까? 바로 현재 "위치"이다. 이 "위치"를 표현하는 방법은 다양하지만, 우리는 일단 현재 플레이어의 위치를 맵 상에서 10,10의 위치에 존재하도록 배치해보도록 한다.

    public class Character {
        private int posX, posY;
        public Character() {
            // TODO Auto-generated constructor stub
            this.posX = 10;
            this.posY = 10;
        }
    }
그리고 캐릭터를 상하좌우으로 움직일 수 있어야 한다. 이를 위해서 `moveUp`, `moveDown` 등의 메서드를 추가해주자. 또한, 외부에서 Character의 현재 위치를 알수 있어야 하기 떄문에 posX과 posY의 getter를 만들어주도록 하자.

    public class Character {
        private int posX, posY;
        public Character() {
            // TODO Auto-generated constructor stub
            this.posX = 10;
            this.posY = 10;
        }
        public void moveUp() {
            posY += 1;
        }
        public void moveDown() {
            posY += 1;
        }
        public void moveLeft() {
            posX -= 1;
        }
        public void moveRight() {
            posX += 1;
        }
        public int getPosX() { return posX; }
        public int getPosY() { return posY; }
    }
이로서 기본적인 캐릭터 시스템은 만들어졌다. 상하좌우로 움직일수 있으며, 외부에서 플레이어의 현재 움직임을 알수 있게 되었다. 이제 이 캐릭터를 화면에 배치해야 하는데, 여기서 약간 복잡한 개념이 나오게 된다.

우리가 캐릭터를 이동할떄, 우리는 캐릭터가 움직인다고 인식을 하지만 실제로 그래픽상에서는 그렇지 않다. 캐릭터는 항상 그 자리에 있으며, 주변 맵이 움직이면서 캐릭터가 움직이는것처럼 착각을 하게 만드는 것이다. 즉, 우리가 아무리 캐릭터를 움직이고 캐릭터의 위치를 변환시켜도, 그래픽쪽에서는 캐릭터를 전혀 움직일 필요가 없고, 그냥 계속 한 장소에 두어도 무방하다. 우리가 만든 맵 시스템에서 이 키 위치는 (4,4), 즉 캔버스상의 픽셀위치는 (200,200)이 된다.

다시 `Surface.java`로 돌아가보자. 여기에 일단 가볍게 플레이어가 항상 있는 위치, 즉 (160,160)에 검은 원을 그려서 플레이어를 표시해주자.

## 맵의 위치는?

<img src="/image/basic.png">

위와 같은 13x13의 맵이 존재하고, 플레이어가 (7,6)의 위치에 서있다고 가정해보자. 플레이어의 위치는 언제나 카메라의 중앙인 (4,4)가 되기 떄문에 위릐 빨간 사각형이 카메라가 실제로 표시하는 부분이 된다. 그렇다면 위의 빨간 오각형의 위치는 어떻게 될까? 이 빨간 오각형의 위치는 실제 맵상에서는 (4,3)이지만, 실제로 표시되어야하는 위치는 그와는 다르다. 빨간 카메라를 기준으로 봤을 경우에 위치는 (1,1)이 되며, 플레이어를 기준으로 봤을때는 (-3, -4)가 된다. 여러가지의 위치 기준이 제시되고 있기 떄문에 이쯤에서 한번 용어 정리를 하고 넘어가자. 머리아프다.

* MapPos: 맵에서의 실제 위치
* DisplayPos: 실제로 보여지는 그래픽상 위치. (빨간 사각형 내에서의 위치)
* PRPos: Player-Relative Pos. 플레이어의 현재 위치를 (0,0)라고 가정했을때의 위치.

이중에서 `DisplayPos`와 `PRPos`는 사실상 플레이어 캐릭터의 현재 위치를 기반으로 하는 위치 표기법이다. 따라서 플레이어가 한번 움직일떄마다 새로 계산해주어야만 한다.
