# 볼링 게임 점수판
## 진행 방법
* 볼링 게임 점수판 요구사항을 파악한다.
* 요구사항에 대한 구현을 완료한 후 자신의 github 아이디에 해당하는 브랜치에 Pull Request(이하 PR)를 통해 코드 리뷰 요청을 한다.
* 코드 리뷰 피드백에 대한 개선 작업을 하고 다시 PUSH한다.
* 모든 피드백을 완료하면 다음 단계를 도전하고 앞의 과정을 반복한다.

## 온라인 코드 리뷰 과정
* [텍스트와 이미지로 살펴보는 온라인 코드 리뷰 과정](https://github.com/next-step/nextstep-docs/tree/master/codereview)

## 기능 정의
* 점수 계산을 제외한 볼링 게임 점수판을 출력할 수 있다.
* 각 프레임이 스트라이크이면 "X", 스페어이면 "9 | /", 미스이면 "8 | 1", 과 같이 출력하도록 구현한다.
* 4가지 점수 모드를 제공한다. 
    * 스트라이크(strike) : 프레임의 첫번째 투구에서 모든 핀(10개)을 쓰러트린 상태
    * 스페어(spare) : 프레임의 두번재 투구에서 모든 핀(10개)을 쓰러트린 상태
    * 미스(miss) : 프레임의 두번재 투구에서도 모든 핀이 쓰러지지 않은 상태
    * 거터(gutter) : 핀을 하나도 쓰러트리지 못한 상태. 거터는 "-"로 표시
* 10 프레임은 스트라이크이거나 스페어이면 한 번을 더 투구할 수 있다.
    * 출력 할 수 있는 자리 하나가 더 필요하다.
    * 스트라이크이거나 스페어가 아니라면 세번째 칸은 "-"로 표시한다.
* 사용자에게 매 프레임마다 몇 개의 핀이 쓰러 졌는지 입력 받는다.

## Top Down 1차 설계
* 참여자
    * 이름
* 핀
    * 넘어진 핀 갯수
* Frames
    * Frame 일급 컬렉션
* Frame
    * NormalFrame
        * 1~9 프레임
    * FinalFrame
        * 10 프레임
        * 'Strike', 'Spare'인 경우 세 번째 투구 활성화
        * 아닌 경우 세 번째 투구는 gutter
* InputView
    * 사용자 입력을 받음
* OutputView
    * 화면에 볼링 현황을 출력
* ScoreType
    * Strike
    * Spare
    * Miss
    * None

## 프로그래밍 요구사항
* 규칙 1: 한 메서드에 오직 한 단계의 들여쓰기만 한다.
* 규칙 2: else 예약어를 쓰지 않는다.
* 규칙 3: 모든 원시값과 문자열을 포장한다.
* 규칙 4: 한 줄에 점을 하나만 찍는다.
* 규칙 5: 줄여쓰지 않는다(축약 금지).
* 규칙 6: 모든 엔티티를 작게 유지한다.
* 규칙 7: 3개 이상의 인스턴스 변수를 가진 클래스를 쓰지 않는다.
* 규칙 8: 일급 콜렉션을 쓴다.
* 규칙 9: 게터/세터/프로퍼티를 쓰지 않는다.