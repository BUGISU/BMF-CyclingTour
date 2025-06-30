<div align="center">

# 🚴‍♀️ 보자마자 피트니스 - 사이클링 투어  
### Cycling Tour: 홈트레이닝 게임 콘텐츠

<img src="https://github.com/JISUSAMA/JISUSAMA/assets/38304918/3a3a499d-5812-4c60-ab45-724b8fd8ccfb" width="80%">

</div>

---

## 🎮 프로젝트 개요

**동작 인식 FIT-TAG 센서 기반 사이클링 피트니스 게임**

- 실내 자전거 + 센서 + Unity로 즐기는 인터랙티브 사이클링 투어
- Cinemachine 기반 카메라 연출, 미션형 지도 콘텐츠 제공
- 플레이어의 움직임을 반영해 실제 자전거 여행처럼 몰입 가능한 홈트 환경 구축
- 첫 여행지는 아시아! 소도시를 배경으로 한 힐링 운동 게임 콘텐츠

---

## ⏱️ 개발 기간

- 2022.08 ~ 2023.01 (총 6개월)

---

## 🛠️ 기술 스택

| 분야 | 사용 기술 |
|------|-----------|
| 엔진 | Unity3D |
| 카메라 | Unity Cinemachine |
| UI 시스템 | Unity UGUI, 커스텀 UI 매니저 |
| 통신 | BLE (FIT-TAG 센서 연동) |
| 멀티랭귀지 | 한국어 / 영어 버전 분리 |
| 플랫폼 | Android (Google Play 출시) |

---

## 📦 프로젝트 구조 (일부)

```

CYCLING\_TOUR/
├── AsiaMap/                # 게임 진행용 맵 기능 및 카메라 이동
├── Sensor/                 # FIT-TAG 센서 통신 및 캐릭터 연동
├── Lobby/                  # 시작 로비 및 사운드 설정
├── UIManager/              # 각종 UI 뷰 관리
├── GameFinish/             # 종료 후 결과 및 리워드 화면
├── Server/                 # 서버 연동 관련 관리 모듈
├── Scripts/
│   ├── FadeEffect.cs       # 씬 전환용 페이드 효과
│   ├── AspectRatioEnforcer.cs  # 화면 비율 고정
│   └── CSVReader.cs        # 설정용 CSV 데이터 파서

```

---

## 💡 주요 기능 설명

### 🎥 Cinemachine 기반 카메라 이동  
- 캐릭터 진행에 맞춰 카메라 자동 추적
- 지도 위 주요 포인트 진입 시 자동 연출 전환

### 🦵 FIT-TAG 센서 연동
- BLE 통신 기반 센서로 실제 자전거 페달 속도 추적
- 캐릭터 속도에 즉각 반영 → 몰입도 있는 운동 감각

### 🧭 아시아 맵 콘텐츠
- 마을/도시별 랜드마크 구성
- 콘텐츠 별 소도시 탐험 & 보상 수집 시스템 포함

---
## 📂 주요 소스 코드 설명

> FIT-TAG 센서 연동부터 캐릭터 이동, 카메라 전환까지 콘텐츠의 주요 시스템을 구성하는 핵심 스크립트입니다.

### 1. `L_ESP32BLEApp.cs` – 센서 연동 & 데이터 처리

- **역할:** ESP32 BLE 센서 장치와 연결 및 데이터 수신
- **주요 기능:**
  - 센서 장치 주소를 통한 연결 시도 및 상태별 처리
  - `SubscribeCharacteristicWithDeviceAddress()`를 이용해 센서 데이터(가속도, Quaternion)를 구독
  - 수신된 byte 배열 길이에 따라 분기 처리:
    - `12 bytes`: 3축 가속도(ax, ay, az)
    - `16 bytes`: Quaternion(qx, qy, qz, qw)
  - 수신된 값을 `Man_Move` 또는 `Woman_Move` 클래스에 전달

```csharp
Man_Move.instance.mpu_value[0] = ax;
Man_Move.instance.mpu_value[1] = ay;
````

---

### 2. `Man_Move.cs` – 캐릭터 이동 제어

* **역할:** BLE 센서 입력값에 따라 캐릭터 이동 구현
* **주요 기능:**

  * 수신된 MPU 데이터(`mpu_value[]`)를 통해 가속/감속 구현
  * 일정 임계값 이상일 경우 전방으로 이동 처리
  * 내부에서 속도 계산과 애니메이션 트리거 연결

---

### 3. `CM_VCamCtrl.cs` – Cinemachine 카메라 전환

* **역할:** 속도/트리거에 따른 가상 카메라 전환 제어
* **주요 기능:**

  * `AsiaMap_UIManager.instance.track_Course.m_Speed` 값에 따라 카메라 프리셋 전환
  * 맵 트리거(`Collider`)를 기반으로 구간별 연출 카메라 전환
  * 산악/자갈/모래/웅덩이 등 특수 지형에 맞춘 카메라 세팅 포함

```csharp
if (speed <= 5.0f)
    virtualCamera_1.Priority = 10;
else if (speed <= 10.0f)
    virtualCamera.Priority = 10;
```

---

### 4. `CameraFollowPlayer.cs` – 플레이어 추적 카메라

* **역할:** LateUpdate 기반의 부드러운 추적 카메라 구현
* **주요 기능:**

  * 목표 캐릭터 회전각/위치 보간
  * 거리 및 높이를 기준으로 자동 카메라 위치 조절
  * `Quaternion.Lerp`, `Mathf.LerpAngle` 등을 활용한 부드러운 움직임 구현

---

### 5. `CameraMoving.cs` – 대체형 카메라 무빙

* **역할:** 회전 중심형 카메라 구성
* **주요 기능:**

  * 타겟 기준으로 원형 회전하여 따라가는 뷰 연출
  * `LookAt()`을 통해 자연스럽게 대상 응시

---

## 🔧 기타 주요 컴포넌트

| 파일명                      | 설명                         |
| ------------------------ | -------------------------- |
| `AsiaMap_DataManager.cs` | 맵 상태 및 게임 흐름 데이터 관리        |
| `OBJCtrl.cs`             | 센서 객체 위치 보정                |
| `GameTime.cs`            | 시간 흐름 및 종료 조건 제어           |
| `AsiaMap_UIManager.cs`   | 트랙 상태 (산/자갈/물/모래) 판단 로직 포함 |

---

> 전체 프로젝트는 BLE 센서를 통해 받은 데이터를 게임 내 이동 및 시각적 연출에 자연스럽게 연결하는 데 중점을 두고 있으며, Cinemachine과 Unity 고유 기능을 적극 활용해 몰입감 있는 피트니스 콘텐츠를 구성합니다.


## 🙋‍♂️ 담당 업무 및 기여도

| 기간 | 기여 내용 |
|------|-----------|
| 2022.08 ~ | 소스 코드 분석 및 구조 파악<br>카메라 무빙 연출 이벤트 시스템 개발<br>랭킹 UI 및 버그 수정 |
| 2022.12 ~ | 영문 버전 UI 텍스트 대응<br>다국어 지원 구조 반영<br>영문 Google Play 버전 빌드 |

<p align="center">
  <img src="https://github.com/JISUSAMA/JISUSAMA/assets/38304918/e2f99466-a000-466b-8bb9-057464addb98" width="400">
</p>

---

## 🌐 Google Play 출시

- [📱 사이클링 투어 (영문 버전) Google Play Store](https://play.google.com/store/apps/details?id=com.gateways.cyclingtour_en&hl=ko&gl=US)

<p align="center">
  <img src="https://github.com/JISUSAMA/JISUSAMA/assets/38304918/f96b3ba1-fd64-4609-b1fc-e8a1d427da14" width="500">
</p>

---

## 🔧 FIT-TAG 센서란?

<details>
<summary>📷 센서 이미지 보기</summary>
<br>

<img src="https://github.com/JISUSAMA/JISUSAMA/assets/38304918/4b84d9a0-569c-4027-810c-6f1f1b34545c" width="45%">
<img src="https://github.com/JISUSAMA/JISUSAMA/assets/38304918/f4bcd9c6-b792-4473-a7ad-4d5238edf4ea" width="45%">
<img src="https://github.com/JISUSAMA/JISUSAMA/assets/38304918/94416305-db7d-4df0-9d3b-84c33f463936" width="45%">
<img src="https://github.com/JISUSAMA/JISUSAMA/assets/38304918/c04f962c-05e9-474a-b15e-67cdce735753" width="45%">

</details>

---

## 📺 유튜브 홍보 영상

[![보자마자 Play 리얼모션 시즌2 홍보영상](http://img.youtube.com/vi/45nUNQHXj1o/0.jpg)](https://www.youtube.com/watch?v=45nUNQHXj1o&t=5s)

