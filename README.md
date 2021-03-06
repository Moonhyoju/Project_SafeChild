통학 차량 어린이 사고 방지시스템
-----------------------------------------
통학차량 안에 탑승한 어린이들을 보호하기 위해 고안된 프로젝트 입니다.

**WorkFlow**
-----------------------------------------
1. 차량 안에 어린이가 탑승하는 것을 감지 및 카운트합니다.
2. 차량 내 온도, 습도, 운전자의 탑승여부를 감지합니다.
3. 차량 내 일어날 수 있는 상황을 감지해서 학부모 또는 유치원(하원)에 경고 메세지를 보냅니다.
4. 위험 감지 패턴
+ 운전자가 탑승하지 않은 상태
  + 차량 내부 아이들이 있고, 온도가 높을 때, 경고가 울립니다.
  + 차량 내부 아이들이 몇 명만 남아있을 떄, 알림이 전달됩니다.
+ 운전자가 탑승한 상태
  + 온도 판단만 합니다.

라즈베리파이(Respberry pi)
-----------------------------------------
차량 내부에 센서를 이용해서 감지하고, 데이터를 서버로 전달합니다. 이동중인 차량에서 데이터를 전송하기 위해 통신 망을 에그로 사용했습니다.

각 센서들에 대한 정보는 서버로 전송되고 MySQL DB에 지역적으로 저장하여 관리합니다.


**기술 스택**
+ Ubuntu
+ Python

**소스코드 간략 설명**
+ Count.py
  + 아이들의 탑승을 적외선 세선를 이용하여 감지하는 파일
+ Button.py
  + 운전자가 탑승하는 것을 감지하는 파일
+ GPS.py
  + GPS 모듈과 연동된 파일
+ Temper.py
  + 온습도를 측정하는 파일


서버 (Server)
-----------------------------------------
라즈베리파이 또는 안드로이드 앱에서 전송되는 정보들을 서버에서 처리합니다. 먼저 라즈베리파이에서 쏘는 데이터 정보(온도, 습도, 위치, 탑승여부 등)를 MySQL DB에서 관리합니다.

**기술 스택**
+ AWS(EC2/ubuntu)
+ PHP 7

**Firebase 토큰 알림 처리**

안드로이드에서 토큰을 받아 저장된 회원들에게 알림을 보냅니다.

안드로이드
-----------------------------------------
회원, 관리자들에게 제공되는 앱으로 차량 안에 아이들의 수, 차량 내부 환경정보들을 확인할 수 있다.
아이들이 위험상황에 처할 경우 푸시알림 메세지를 받게된다.

**기술 스택**
+ Java
+ FCM
