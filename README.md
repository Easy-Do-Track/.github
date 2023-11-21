# Public Readme

# 🐱 Easy Do Track 🐱

### 저가 풀 바디 트래킹 기술 개발

2021년 기준으로 버추얼 스트리머는 약 16,000명, VR·AR 기기 시장은 약 986만 대를 기록하고 있으나 현재 출시된 풀 바디 트래커는 30~600만 원대로, 가볍게 구입하기에는 부담스러운 가격대를 형성하고 있다.
따라서, VR 콘텐츠를 체험하거나 즐기고 싶어하지만 비용에 민감한 사람들을 위해 사용자 친화적이고 높은 접근성을 제공하는 저가 풀 바디 트래커를 개발하였다.

3D 프린팅과 라즈베리 파이 및 가속도, 자이로 센서를 사용해서 본체 및 트래커를 제작하였으며, Go 언어로 작성된 데이터 처리 서버, JavaScript와 React, Three.js 라이브러리를 활용하여 웹 환경에서 사용 가능한 뷰어를 개발하였다. 트래커와 뷰어 간 데이터 통신에는 Wi-Fi를 이용한 UDP 통신을 하였고, 트래커 본체는 I2C(Inter-Integrated Circuit) 통신을 이용해 센서 데이터를 취합한다.
또한, 게임과 영상에서 사용되는 쿼터니언 연산을 통해 센서로부터 받은 데이터를 토대로 모델링의 포즈 렌더링을 진행한다.

## 🛠️ Tech Stack 🛠️

[https://img.shields.io/badge/-Raspberry--Pi--pico-yellow?style=for-the-badge](https://img.shields.io/badge/-Raspberry--Pi--pico-yellow?style=for-the-badge)

[https://img.shields.io/badge/-C--language-brightgreen?style=for-the-badge](https://img.shields.io/badge/-C--language-brightgreen?style=for-the-badge)

![Untitled](Public%20Readme%205e0b84b563d14ee9a12dcf72f82f8d7f/Untitled.png)

[https://img.shields.io/badge/-Go-blue?style=for-the-badge](https://img.shields.io/badge/-Go-blue?style=for-the-badge)

[https://img.shields.io/badge/-Javascript-orange?style=for-the-badge](https://img.shields.io/badge/-Javascript-orange?style=for-the-badge)

[https://img.shields.io/badge/-React.js-purple?style=for-the-badge](https://img.shields.io/badge/-React.js-purple?style=for-the-badge)

[https://img.shields.io/badge/-three.js-cyan?style=for-the-badge](https://img.shields.io/badge/-three.js-cyan?style=for-the-badge)

## ⚙️ 시스템 구성 ⚙️

![Untitled](Public%20Readme%205e0b84b563d14ee9a12dcf72f82f8d7f/Untitled%201.png)

### 📺 Easy-Do-Viewer 📺

| 기능명 | 사용 라이브러리 | 설명 |
| --- | --- | --- |
| 프로필 관리 | react.js | 사용자 프로필을 생성하고 제거할 수 있는 기능
프로필 선택 시 뷰어 페이지로 이동 |
| 트래커 정보 출력 | react.js | Easy-Do-Driver로부터 수신한 트래커 연결 정보 출력 |
| 3D 모델 출력 | Three.js, ammo.js | Easy-Do-Driver로부터 수신한 데이터를 이용하여 사용자의 움직임에 따라 포즈가 바뀌도록 3D 모델 출력 |
| 3D 모델 변경 | Three.js, ammo.js | 3D 모델 출력 시 보이는 3D 모델을 변경하는 기능 |
| 배경 색상 변경 | Three.js, ammo.js | 원하는 배경 색으로 변경
크로마키 기능을 제공하기 위해 추가된 기능 |
| 웹 성능 모니터링 | Three.js, ammo.js | FPS, 메모리 등의 정보 출력 |

### 💪 Easy-Do-Tracker 🦵

| 기능명 | 센서 | 통신 | 사용 라이브러리 | 설명 |
| --- | --- | --- | --- | --- |
| 각도 측정 | IMU (MPU6050) | I2C | i2cdevlib | 신체 부위들의 각도를 측정 |
|  | I2C-Multiplexer | I2C | pico-sdk | 동일한 I2C 주소를 가지는 IMU들을 제어 |
| 초기화 | 스위치 | GPIO | pico-sdk | 트래커 초기화 |
| 센서 정보 전송 |  | UDP | pico-sdk | 측정한 원시 센서 데이터를 데이터 처리 서버로 전송 |

### **🪛** Easy-Do-Driver **🪛**

| 기능명 | 사용 라이브러리 | 설명 |
| --- | --- | --- |
| 트래커 센서 정보 수신 | net | UDP로 센서 데이터 수신 |
| 센서 데이터 처리 |  | 수신한 센서 데이터에 쿼터니언 연산을 적용 |
| HTTP API | net/http
encoding/json
github.com/gorilla/handlers
github.com/gorilla/mux | 연결된 포트 정보 등 통계 정보 전송 |
| WebSocket API | github.com/gorilla/websocket | 처리 완료된 각도 데이터를 뷰어로 스트리밍 |

## 빌드 방법

| 동작 | 명령어 |
| --- | --- |
| Easy-Do-Track | mkdir build && cd build && cmake .. && make . |
| Easy-Do-Driver | go mod install && go build |
| Easy-Do-Viewer | npm init |

## 실행 방법

| 동작 | 명령어 |
| --- | --- |
| Easy-Do-Driver | ./easy-do-driver |
| Easy-Do-Viewer | npm start |

©️ 2023 금오공과대학교 창의설계프로젝트 4분반 1조 - Easy Do Track