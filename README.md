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

