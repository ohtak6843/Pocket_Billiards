# 🎱 Pocket Billiards

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)
![pico2d](https://img.shields.io/badge/Library-pico2d-green)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey)
![Status](https://img.shields.io/badge/Status-Completed-success)

> Python과 `pico2d` 라이브러리로 제작한 2D 포켓볼 게임. 2D Game Programming 강좌의 텀 프로젝트로 개발되었습니다.


## 📖 프로젝트 소개

**Pocket Billiards** 는 마우스 조작만으로 즐길 수 있는 캐주얼 2D 포켓볼 게임입니다. 실제 당구의 물리적 충돌(공–공, 공–벽 반사, 마찰 감속)을 직접 구현하였으며, 여기에 **플러스/마이너스 홀**, **연속 득점 더블 스코어**, **체력(HP) 시스템** 등 아케이드 요소를 더해 단순한 시뮬레이션 이상의 재미를 제공합니다.

플레이어는 세 개의 스테이지를 거치며 모든 공을 포켓에 넣어 다음 단계로 진출해야 합니다. 무작위로 지정되는 두 개의 특수 홀(보너스/페널티)을 어떻게 활용하느냐에 따라 점수와 잔여 체력이 크게 달라지므로, 단순한 정확도 외에도 전략적 판단이 요구됩니다.

**해결하고자 한 문제**

- 복잡한 외부 물리 엔진 없이, 기초 벡터/삼각함수만으로 자연스러운 당구 물리를 직접 구현
- 단순 반복적인 당구 게임에 RPG 풍의 체력·점수 시스템을 결합하여 플레이 동기 강화
- 상태 머신(state machine) 기반의 큐대 조작으로 직관적인 마우스 컨트롤 제공


## 👤 개발자

| 이름 | 역할 | 연락처 |
| --- | --- | --- |
| ohtak6843 | 기획 · 프로그래밍 · 리소스 통합 | [GitHub](https://github.com/ohtak6843) · ohtak6843@gmail.com |

> 개인 텀 프로젝트로, 단독 개발되었습니다.


## 📅 개발 기간

- **시작일**: 2023년 10월
- **종료일**: 2023년 12월

### 주요 마일스톤

| 일자 | 마일스톤 |
| --- | --- |
| 2023-10 | 프로젝트 기획 · 게임 구조 설계 · 초기 프로토타이핑 |
| 2023-11 | 공 충돌 물리 구현 · 마찰력 시스템 · 홀(Hole) 클래스 · 큐대 리팩토링 |
| 2023-12 초 | 통과(Pass) / 실패(Fail) 모드 추가, Plus/Minus 상태 도입 |
| 2023-12 중 | 타이틀 모드, 점수 표시, 다단계 스테이지, 배경 음악, 세이브 기능 |
| 2023-12 말 | 도움말 모드, 보조선 시스템, 원형 충돌 판정으로 개선, 빌드 완료 |


## 🛠 개발 환경

| 항목 | 내용 |
| --- | --- |
| **OS** | Windows |
| **IDE** | JetBrains PyCharm |
| **언어 / SDK** | Python 3.11 |
| **그래픽 라이브러리** | pico2d (SDL2 기반) |
| **빌드 도구** | PyInstaller |
| **버전 관리** | Git · GitHub |


## 🧰 기술 스택

### 게임 / 그래픽

| 분류 | 사용 기술 |
| --- | --- |
| 게임 라이브러리 | `pico2d` (이미지 · 사운드 · 입력 처리) |
| 사운드 | `pico2d` 의 `load_wav`, `load_music` (MP3 · WAV) |
| 폰트 | `ENCR10B.TTF` (커스텀 비트맵 폰트) |

### Python 표준 / 외부 모듈

| 분류 | 사용 기술 |
| --- | --- |
| 데이터 직렬화 | `pickle` (게임 세이브) · `tomllib` (스테이지/리소스 설정) |
| 수학 / 물리 | `math` (벡터 정규화, 충돌 반사각 계산) |
| 시스템 | `time`, `os`, `shutil`, `random`, `importlib` |
| 배포 | `PyInstaller`, `sdl2dll` |


## ✨ 주요 기능

- **물리 기반 공 충돌 시뮬레이션**
  벡터 내적·정규화를 이용해 공–공, 공–벽 충돌 후의 속도·진행각을 직접 계산합니다. 마찰력에 의해 시간이 지날수록 공이 자연스럽게 감속합니다.

- **상태 머신 기반 큐대 조작**
  큐대는 `Idle → Pull → Push → Hide` 의 4단계 상태로 동작하며, 마우스 좌클릭을 길게 누르면 파워가 차오르고, 떼는 순간 흰 공을 가격합니다.

- **3단계 스테이지 진행**
  Stage 1(공 3개) → Stage 2(공 6개) → Stage 3(공 10개) 로 난이도가 점진적으로 상승합니다. 모든 공을 포켓에 넣으면 다음 스테이지로 진출합니다.

- **Plus / Minus 홀 시스템**
  매 턴마다 6개 포켓 중 두 곳이 무작위로 보너스(노란색) 홀과 페널티(빨간색) 홀로 지정됩니다. 노란 홀에 넣으면 **3배 점수 + 보조선 표시**, 빨간 홀에 넣으면 **턴 실패** 처리됩니다.

- **체력(HP) · 점수(Score) 시스템**
  하트 6개로 시작하며, 흰 공이 포켓에 빠지면 –2, 페널티 시 –1, 공을 정상 포켓팅하면 +1까지 회복됩니다. 연속 성공 시 **doubleS** 배율이 올라가며 점수가 누적 증가합니다.

- **세이브 / 로드 기능**
  `pickle` 로 게임 월드 전체(객체·충돌쌍)를 직렬화하여, 흰 공이 빠지는 등 실패가 발생했을 때 직전 상태로 복원합니다.

- **여러 게임 모드**
  타이틀(Title), 도움말(Help), 스테이지(Stage 1–3), 통과(Pass), 실패(Fail), 결과(Result) 모드를 모드 스택 기반으로 전환합니다.

- **자동 빌드 스크립트**
  `run_pyinstaller.py` 와 `pyinstaller_settings.toml` 을 이용해 데이터 파일/폴더·SDL DLL을 자동 복사하여 실행 파일을 생성합니다.


## 📂 폴더 구조

```
Pocket_Billiards/
├── PPTs/                       # 1차·2차·최종 발표 자료 및 영상
├── TermProject/                # 게임 본체
│   ├── main.py                 # 진입점 (캔버스 오픈 → game_framework 실행)
│   ├── game_framework.py       # 모드 스택 · 프레임 루프
│   ├── game_world.py           # 객체 레이어 · 충돌쌍 등록 · 세이브/로드
│   ├── server.py               # 전역 게임 상태 (공, 큐대, 체력, 점수 등)
│   ├── define.py               # 윈도우 크기 · 픽셀/미터 변환 · 벡터 함수
│   │
│   ├── ball.py                 # 공 클래스 · 충돌 처리 · 마찰
│   ├── stick.py                # 큐대 · 상태 머신 · 파워 게이지
│   ├── hole.py                 # 홀 · Plus/Minus 상태
│   ├── wall.py                 # 벽 반사 처리
│   ├── table.py                # 당구대 배경
│   ├── heart.py                # 체력 표시
│   ├── score.py                # 점수 표시 · 더블 배율
│   │
│   ├── title_mode.py           # 타이틀 화면
│   ├── help_mode.py            # 도움말 화면
│   ├── stage1.py / stage2.py / stage3.py
│   ├── stage1_UI.py / stage2_UI.py / stage3_UI.py
│   ├── pass_mode.py            # 턴 성공 연출
│   ├── fail_mode.py            # 턴 실패 연출
│   ├── result_mode.py          # 최종 결과
│   │
│   ├── init_data.toml          # 벽·홀·공 초기 좌표
│   ├── pyinstaller_settings.toml
│   ├── run_pyinstaller.py      # 자동 빌드 스크립트
│   ├── saved_data.pickle       # 게임 세이브 파일
│   │
│   └── (이미지 · 사운드 · 폰트 리소스)
└── README.md
```


<!-- TODO: 라이선스가 정해지면 LICENSE 섹션을 추가하세요. -->
