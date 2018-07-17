---
layout: default
title: 더블 버퍼링(Double Buffering)이란?
category: Tips
tags:
- tip
- double buffering
- triple buffering
- buffering
- graphics
- c++
---

## 랜더링 과정을 살펴보자...
그래픽 관련 랜더링을 진행하다 보면 자주 화면 깜빡임 현상 (flickering)에 마주하는 경우가 생긴다. 대부분의 프로그램에서는 `DC`라고 불리는 `Drawing Context` 오브젝트를 이용해서 화면에 그림을 직접 그리게 된다. 이 때 프로그램은 대부분 아래와 같은 과정을 반복하게 된다.

1. 화면 클리어 (대부분 화면 크기의 배경 색 Rectangle을 그림)
2. 오브젝트 다시 그리기
3. 다시 1번으로...

이 과정은 실제로는 매우 빠른 속도로 돌아가기 때문에 실제로는 거의 오브젝트가 계속 표시되는 것 처럼 보일 것 같지만, 사실은 그렇지 않다.

화면을 지우고 새로 그리는 과정이 반복되다보면 화면에는 필연적으로 하얀 배경 화면만 보이는 `frame`이 간간히 보여지게 될 것이다.

이러한 `flicker`를 막기 위해서 고안된 방법이 바로 이중 버퍼링 기술이다.

## 더블 버퍼링이 무엇인가요?
더블 버퍼링은 말 그대로 두개의 `buffer`, 즉 두개의 `DC`를 가지고 화면 그리기를 진행한다.

우선 첫번째 메인 DC는 만들기만 하고 아무런 역할을 하지 않는다. 이 메인 DC는 실제 모니터 화면에 띄우게 하는 직접적인 권한을 가지게 한다.

그리고 두번째, 메모리 DC는 화면에는 띄우지 않지만, 내부적인 Bitmap 버퍼를 만들어서 거기에 그림이 그려지도록 한다.

그 후에 메모리 DC를 이용하여 내부적으로 완성된 하나의 프레임을 메인 DC에 그대로 이미지를 복사해준다.

이렇게 하면 실제 화면에서 중간중간 오브젝트가 사라져 보이는 일이 없어지고, 화면은 부드럽게 진행될 수 있게 된다.

## 예시를 보여주세요.
우선 예시는 간단한 `MFC` `C++`로 진행한다.
```cpp
// CDlg의 paint 메소드
void CMainDlg::paint() {
    CPaintDC    dc(this);  
    CDC         *mainDC;        // 화면에 접근하는 DC
    CDC         memDC;          // 임시 메모리 DC

    CRect rect;
    this->GetClientRect(&rect);

    CBitmap *oldBitmap;
    CBitmap tempBitmap;

    mainDC = this->GetDC();

    // 메인 DC를 사용하여 memCD 초기화
    memDC.CreateCompatibleDC(mainDC);
    // 현재 그리기 영역 사이즈의 임시 Bitmap 생성
    tempBitmap.CreateCompatibleBitmap(mainDC, rect.right, rect.bottom);
        
    // 새로운 Bitmap 선택
    oldBitmap = memDC.SelectObject(tempBitmap);

    // 메모리 DC에 하얀 배경 출력
    memDC.PatBlt(0, 0, rect.right, rect.bottom, WHITENESS);

    // 메모리 DC 10,10 위치부터 20,20까지 사각형 그리기
    memDC.Rectangle(10,10,20,20);

    // 메모리 DC의 비트맵을 메인 DC에 옮겨 그려준다.
    mainDC->BitBlt(0, 0, rect,right, rect.bottom, &memDC, 0, 0, SRCCOPY);

    // 클린업
    memDC.SelectObject(oldBitmap);
    memDC.DeleteDC();

}
```
위 코드를 보면 알겠지만, 화면 만큼의 Bitmap을 만들어두고 거기에 모든 그래픽 작업을 진행하게 된다. 그 후, 화면에 연결된 메인 DC에 그대로 붙여넣기를 하게 된다.

## 참고 자료
<https://ko.wikipedia.org/wiki/%EB%8B%A4%EC%A4%91_%EB%B2%84%ED%8D%BC%EB%A7%81>
<https://en.wikipedia.org/wiki/Multiple_buffering>



