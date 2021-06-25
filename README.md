## IOT 화장품 냉방 관리 기구

 2019년도 로봇공학과에 있을 당시 진행했던 프로젝트입니다. 로봇공학과이기 때문에 전자회로, 디지털논리회로, 기구, 프로그래밍 등을 톻합적으로 배웠습니다. 이렇게 배운것들을 기반으로 기구, 전자회로, 프로그래밍 등이 결합된 IOT 화장품 냉방관리 기구 프로젝트입니다. 팀원은 김현명, 노재상, 엄준태, 박재윤, 강승현이고 저는 그 중 팀장과 프로그래머의 역할을 맡았습니다. 개인적으로는 기억에 많이 남는 프로젝트입니다.

## 프로젝트 개요

 화장품[로션,스킨]들을 냉방으로 관리하고 터치스크린을 통해 관리 및 자동배출 하는 기구입니다.
또한 인터넷과 연동되어 화장품들의 잔량 상태, 기구내 온도,습도를 서버에 저장하고 확인이 가능합니다. 터치스크린 기반의 GUI를 제작했고 이를 통해 화장품들을 확인하고 모션인식센서를 기반으로 손을 인식하면 자동으로 선택한 화장품이 배출되도록 하였습니다. 이 과정들을 중앙에서 라즈베리파이라는 일종의 작은 cpu가 관리, 제어합니다.

라즈베리파이와 터치스크린, 여러센서, 그리고 인터넷 서버를 연동시켜서 만든 IOT 화장품 냉방 관리 기구입니다.


## 진행 기간
2019-01-01 ~ 2019-06-20


## 프로젝트 구성

 이 프로젝트는 IOT 기구를 만드는 프로젝트이다 보니 기구,회로,프로그램 등등이 고려가 되어야 합니다. 다만 이 곳에서는 전체적인 (프로그램) 시스템 구성도와 프로그램 관련된 부분만을 정리하겠습니다.

## (프로그램) 시스템 구성도
![image](https://user-images.githubusercontent.com/44837403/116768816-889f4680-aa74-11eb-87b2-4d75c8a1bc03.png)

우선 입력 센서들로부터 여러 입력 값들을 디지털 값으로 받게 되고 라즈베리파이 내에서 사용하게 되있습니다. 또 라즈베리파이는 이 데이터들 중 일부를 Firebase 로 보내 데이터베이스화하고 이 데이터들은 스마트폰과 연동해서 사용을 할 수 있습니다. 기본적으로 라즈베리파이는 와이파이를 기반으로 해서 인터넷 통신을 하게끔 되있고 스마트폰 역시 와이파이와 더불어 데이터 통신을 통해 통신을 할 수 있습니다. 또, 터치스크린 부분은 라즈베리파이 내 tkinter 프로그램을 사용해서(위의 qypt5가 아닌 tkinter 프로그램을 사용하였습니다.) GUI를 구성해서 사용하게끔 하였습니다.

## 라즈베리파이 - 터치스크린 GUI

![image](https://user-images.githubusercontent.com/44837403/116769554-04e75900-aa78-11eb-8745-b0d4bd0a8851.png)

터치스크린의 MAIN page입니다. 이곳에서 원하는 화장품들을 고를 수 있고 각 화장품들을 누르면 해당 화장품이 일정량 배출하게 됩니다.

![image](https://user-images.githubusercontent.com/44837403/116769555-07e24980-aa78-11eb-8019-2b29d4131c09.png)

화장품들의 설정 page입니다. 각 화장품들의 화장품 배출량을 설정할 수 있고 잔여량 역시 확인할 수 있습니다. 기구의 냉방 온도를 설정할 수 있고 현재 온도에 대해서 확인할 수 있습니다. 이 때 이 정보들은 저장을 누를 경우 라즈베리파이 -> firebase의 데이터베이스에 저장이 되게 됩니다. 그 후 다시 라즈베리파이로 불러와서 보여주는 식인데, 이렇게 하면 기구 정보들을 서버의 데이터베이스에 저장하고 사용할 수 있게 됩니다.

![image](https://user-images.githubusercontent.com/44837403/116769560-0f095780-aa78-11eb-8b32-025cb757cdb7.png)

추가 배출 기능을 위한 page입니다. 추가 배출을 원할 경우 이 page에서 추가 배출을 할 수 있습니다.


## 라즈베리파이 - Firebase 연동 환경 구성

우선 구글 계정으로 현재 우리가 앱 - 라즈베리파이 - 파이어베이스에서 사용할 데이터
3가지 (화장품 잔여량, 배출량, 기준 온도 설정량)들로 구성된 데이터 베이스를
제작하였습니다. 이렇게 firebase를 사용하면 좋은 점은, 실시간으로 어느 한곳에서 데이터를 바꾸어 firebase 로 전송한다면 데이터 upgrade가 가능하고 체계적으로 데이터를 관리할 수 있을뿐더러, 앱에서도 사용할 수 있게 됩니다.

![image](https://user-images.githubusercontent.com/44837403/116769316-192a5680-aa76-11eb-9283-a50c67701be7.png)


출처 - 네이버 블로그
위는 라즈베리파이에 firebase를 설치하는 코드인데, 라즈베리파이b3 는 저렇게 하면 안되고, pip3 install 형식으로 해주어야 합니다.


## 라즈베리파이에서 온도센서, 모션센서, 스텝모터, dc모터, 릴레이모듈 사용을 위한 기본 구성
![image](https://user-images.githubusercontent.com/44837403/116769193-4d514780-aa75-11eb-9c17-15150aed7403.png)

 GPIO.setwarnings를 넣어주어야 GPIO 관련해서 생기는 오류들을 막을 수 있습니다.
또 온도센서는 전용 라이브러리를 다운받아서 사용해야 합니다. 파이썬에는 다양한 라이브러리들이 존재하는데, 이를 사용하면 다양한 센서들을 손쉽게 제어 할 수 있습니다.

## 라즈베리파이 화장품 배출을 위한 기능 순서도

![image](https://user-images.githubusercontent.com/44837403/116769287-e2ecd700-aa75-11eb-904d-9b10a8359e0d.png)

라즈베리파이에서 화장품 배출 기능을 구현하기 전에 만든 기능 순서도 입니다. 위 과정에 따라서 프로그램을 구현하였습니다.


#### 라즈베리파이 화장품 배출 기능

- 화장품 배출 Auto 작동 기능
 화장품 배출을 자동화 기능입니다. 자동화 버튼을 클릭하면 지정해둔 화장품 순서에 따라서 자동으로 배출을 하는 기능입니다.

- 화장품 배출 Manual 작동 기능
화장품 배출을 일일히 원하는 화장품을 선택해서 수동으로 배출할 수 있는 기능입니다.
 
#### 손동작 인식 기능

손동작이 화장품 배출구 쪽에서 인식이 되면 화장품이 배출되록 하는 기능입니다.

#### 냉방 온도 제어 기능

 우리 기구에서, 냉방을 유지하려면 현재 온도를 읽고, 기준 온도까지 냉방 소자를 돌려야합니다.
 그러려면, 프로그램 내에서 온도를 읽고 기준온도와 비교하는 과정을 계속해서 해야하는데 while true 문으로 계속해서 돌리기보다 thread 구문을 사용해서 3초에 한번씩 비교해서 릴레이 보드를 작동, 냉방소자를 제어하기로 하였습니다. 3초에 한번씩 해서 프로그램 데이터 충돌이 잦아져 60초에 한번 씩으로 사용하게 되었습니다.

#### App Inverntor를 통한 스마트폰 연동 기능

이때 당시 모바일 앱개발에 대한 지식이 없어서 앱 인벤터를 활용해서 스마트폰과 이 기구를 연동하도록 하였습니다. 이 부분은 강승현 팀원이 맡아서 진행하였습니다.


## 주요 프로그램 기능 설명 영상
https://www.youtube.com/watch?v=PofEzpXMSug


## 결과물 및 시연영상

![image](https://user-images.githubusercontent.com/44837403/116770053-b3d96400-aa7b-11eb-907a-e9ee162de318.png)

https://www.youtube.com/watch?v=TWAgs8BrAZU

## 느낀점

 그동안 로봇공학과에서 배운 전자,기구,프로그램등을 통합적으로 활용해볼 수 있는 프로젝트였습니다.
 
 사실 당시에는 편입공부도 동시에 진행을 했는데 하다보니까 프로젝트 개발에 좀 더 몰두 했었습니다. 그래서 프로젝트 개발은 진행을 하면서 편입공부도 신경쓰느라 여러모로 불안해하던 시기였습니다. 그래도 제가 팀장이였고 많은 팀원들과 같이 일을 진행하고 있었기 때문에 책임감을 가지고 진행을 했었습니다.
 
 프로젝트는 성공적으로 마무리 되었고 이 과정에서 배운점은 막상 만들기 어려워보이고 할 수 있을까? 하는 제품이 있더라도 꾸준하게 그리고 다같이 열심히 만들다면 해낼 수 있다는 것이였습니다. 이 때 당시의 프로젝트 경험은 이후 제가 진행한 프로젝트들에서 일종의 믿음을 주게 되었습니다. 열심히 진행한다면, 좋은 방향으로 나아간다면 해낼 수 있다는 믿음. 편입공부를 같이 진행하느라 힘들었지만 그만큼 배우는 점도 많았고 성장할 수 있었습니다.
