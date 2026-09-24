# Kim KwanHee (김관희) — Robotics Portfolio

> **사람들이 일상에서 쉽고 편하게 쓰는 로봇을, 실제로 끝까지 동작하게 만드는 엔지니어**

기계공학부 4년제를 졸업했으며, 센서 신호가 제어 동작으로 이어지는 로봇 시스템 등 다양한 프로젝트를 진행해 왔습니다.
전공 수업에서 아두이노로 모터를 제어해 라인트레이서를 만든 일에서 시작해, 무인모빌리티 자율주행 대회 팀장을 거쳐 ROS2(로봇 프로그램 간 통신 프레임워크) 기반 협동로봇·AMR(자율이동로봇) 프로젝트에서 상태관리, 안전 게이트, 인지-모션 통합을 맡았습니다.
각 카드에는 제가 맡은 부분과 팀원들과 함께 한 부분을 나눠 적었고, 프로젝트에서 구현한 기술 전체는 카드 아래 접힌 목록에 정리했습니다.

📫 gwanhuig01@gmail.com · 🐙 [github.com/gwanhuiGIM](https://github.com/gwanhuiGIM)

| | |
|:--|:--|
| 🎓 학력 | 서천고등학교(충남) 졸업 (2017~2020.02) · 충남대학교 기계공학부 학사 졸업 (2020.02~2026.08) |
| 🤖 교육 | 두산로보틱스 ROKEY 부트캠프 8기 — 지능형 로보틱스 엔지니어 (26.02~26.08) |
| 🏆 수상 | 교내 우수캡스톤디자인 경진대회 우수상 (24.11) · 교내 설계경진대회 우수상 (25.08) |
| 📜 자격·어학 | SOLIDWORKS CSWP (Design Professional) · OPIc IH |
| 🛠️ 스킬 | `ROS·ROS2` `Python` `C++` `Ubuntu` `SolidWorks` `Arduino` `OpenCV` |

### 🧭 성장 흐름
**아두이노 임베디드**(졸업프로젝트 · 모터 차동 제어) → **ROS2, 센서 활용 차량 자율주행 대회**(ERP42 · 팀장) → **협동로봇·AMR을 활용한 부트캠프 프로젝트 진행 - 계획·설계·구현·통합·결과보고**(ROKEY 4개 프로젝트) → **예외처리 설계·논문/오픈소스 분석 기반 설계·구동 중 장애물 실기 테스트·개발 기록 문서화**(VLA Pick & Place)

### 📑 목차
- 대표 프로젝트: [🦾 VLA(Vision-Language-Action) 자연어 Pick & Place](#vla) · [🚗 자율주행 ERP42](#erp42)
- 그 외 프로젝트(진행 순): [🛟 열감지 추적 구명보트](#lifeboat) · [🩺 수술도구 전달 시뮬레이션](#surgical) · [🚨 산업안전 AMR 관제](#amr) · [☕ 핸드드립 커피 자동화](#coffee)
- [💡 What I bring](#bring) · [🗂️ 저장소 모음](#repos)

<!-- ponytail: 대표작 2개는 풀 카드, 나머지는 진행 기간 순 압축 카드(사용자 지정 순서 유지). 팀 기술 전체는 <details>로 접어 첫 화면 가독성 확보. -->

---

## 🔖 대표 프로젝트

<a id="vla"></a>
### 🦾 VLA 기반 자연어 Pick & Place — 협동로봇 구동 중 장애물 감지 시 정지 후 경로 수정 로직 구현
**판단(LLM)과 안전(상태머신)의 제어 권한을 하나로 모으고, 구동 중 장애물이 경로를 막으면 멈춘 뒤 새 경로로 이어 가게 했습니다**

Doosan M0609 + RG2 그리퍼 + RealSense D435i · 5인 팀 · ROKEY 4차 (26.07.30~26.08.12)
**본인 담당:** 판단 계층·안전 계층 통합, 구동 중 정지 후 재계획 연결
**팀원들과 함께:** 인지 실패 감지 게이트

- **개요:** "사과 바구니에 담아줘" 같은 자연어 지시를 LLM(대규모 언어모델)이 해석하면, 협동로봇이 물체를 인식해 집어 옮기는 시스템입니다.
- **이 프로젝트의 위치:** ERP42에서 시작한 ROS2 경험이 부트캠프 앞선 3개 ROS2 프로젝트를 거쳐, 판단·인식·모션·안전의 여러 로봇 시스템을 하나로 통합하는 단계까지 깊어진 마지막 프로젝트입니다.
- **문제 ① 제어 주체가 둘:** 판단 LLM 계층과 안전 계층(pick FSM(Finite State Machine) — 로봇의 상태를 단계별로 구분해 모니터링하고, 중단 시 해당 단계부터 다시 수행할 수 있도록 설계한 상태머신)이 각자 로봇에 명령을 보낼 수 있는 구조였습니다. 저는 로봇 제어 권한을 안전 계층 하나로 좁히고, 판단 계층은 "무엇을 어디로" 옮길지만 넘기도록 통합했습니다.
- **문제 ② 에러 없는 실패 (팀원들과 함께):** 장애물 인식 모듈이 멈춰도 경로 계획은 "장애물 없는 세상" 기준으로 정상 성공했습니다. 팀원들과 함께 원인 후보를 ① 인식 서비스 미기동 ② 설정 오류 ③ 최신 장애물 반영 지연으로 나누고, 로봇을 움직이지 않은 채 계획만 1회 실행해 설정 오류 케이스를 재현했습니다. 이를 근거로 **인식 서비스가 없으면 이동을 거부하는 게이트**와, 경로를 바꿀 때마다 실제로 반영된 장애물 수를 기록하는 확인을 두 겹으로 넣었습니다. 서비스는 떠 있지만 설정이 틀린 경우는 첫 계획을 미리 실행하는 점검 모드로 드러나게 했습니다.
- **문제 ③ 구동 중 장애물:** 로봇이 움직이는 도중 새 장애물이 경로를 막으면 멈추고, 장애물이 사라지기를 기다리지 않고 새 경로가 나오면 그 경로로 이어 가야 했습니다. 저는 이 루프를 상태머신에 중복 구현하지 않고 MoveIt(`move_group`)에 내장된 실행 중 재계획을 쓰도록 pick FSM을 연결했고, 상태머신은 재계획마저 실패했을 때의 재시도만 맡게 했습니다. 기본 플래너(OMPL) 경로에서는 정지 후 새 경로로 이어 가는 동작이 됐지만, GPU 플래너(cuMotion) 경로에서는 실행 중 장애물을 그대로 밀고 가는 것을 실기로 확인했습니다. cuMotion은 계획을 요청하는 순간에만 장애물 정보를 읽기 때문에, 실행 중 MoveIt의 감시에는 그 정보가 공유되지 않는 것이 원인이라는 가설을 세웠고, 이 문제로 실행 중 반응형 회피가 가능한 대안(RMPflow)을 검토했습니다.
- **결과·한계:** OMPL 경로에서 구동 중 장애물이 들어왔을 때 멈춘 뒤 새 경로로 이어 가는 동작과, 출발 전 투입한 장애물을 반영한 우회를 실기로 확인했습니다. cuMotion 경로의 실행 중 회피와 전체 pick-to-place 실물 검증은 다음 단계로 남아 있습니다.
- **회고:** "동작이 성공했다"는 신호와 "안전하게 동작했다"는 신호는 다른 층에서 따로 검증해야 한다는 것을 배웠습니다.

<!-- <p align="center"><img src="./assets/vla-pick-demo.gif" alt="VLA Pick & Place 시연" width="720"></p> -->

<details>
<summary><b>프로젝트 기술 전체 · 코드 근거</b></summary>

- **판단 계층(VLM):** 규칙으로 처리 가능한 지시는 LLM 없이(Tier 1), 나머지는 GPT-5-mini + 카메라 사진 대화(Tier 2)로 무엇을·몇 개를·어디로 옮길지 결정. 손가락 가리키기 선택, 다중 물체 순차 처리, "컵은 담지 마" 같은 규칙 기억, "멈춰" 즉시 정지
- **인식·파지:** 거치형 RealSense(eye-to-hand 캘리브레이션) + YOLO 물체 인식 → GraspGenX 파지 후보 생성
- **모션플래닝:** MoveIt `move_group` 실행 중 재계획(OMPL 경로, 정지 후 새 경로), nvblox ESDF(장애물 표면까지의 거리를 담은 3D 거리장) 기반 cuMotion(cuRobo) GPU 계획, RMPflow 제안 검토(설치된 cuRobo에는 없어 MPC의 ROS 래핑 가능성을 별도 검토). 실기 중 cuMotion 경로 교체 문제를 발견해 팀원의 3Hz 재계획 루프로 임의 테스트(설계·실험 단계에서 종료)
- **안전 계층:** deterministic pick FSM이 모션 취소·그리퍼 개폐·물체 보유·충돌 씬을 전담, 판단 계층과는 JSON 3채널로만 연결
- **기록:** 설계·실측 제약·실험 로그를 문서로 관리
- **코드 근거:** [24개 동작 상태 pick FSM — `states.py`](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/src/pick_fsm/pick_fsm/states.py#L20-L44) · [구동 중 정지 후 재계획 — `moveit_bridge.py`](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/src/pick_fsm/pick_fsm/moveit_bridge.py#L218-L224) · [이동 전 ESDF 게이트(팀원들과 함께) — `arm.py`](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/src/cumotion/cumotion/arm.py#L361-L372) · [실측 제약 문서 — `constraints.md`](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/docs/fsm/context/constraints.md)

</details>

🔗 팀 최종 코드: [Rokey_cobot2](https://github.com/gwanhuiGIM/Rokey_cobot2) · 개인 개발본: [Personal_cobot2_ws](https://github.com/gwanhuiGIM/Personal_cobot2_ws)

---

<a id="erp42"></a>
### 🚗 자율주행 ERP42 — 2025 대학생 창작 모빌리티 경진대회 (무인모빌리티 부문)
**인지 모듈 일부가 빠져도 측위와 경로추종을 유지하는 최소 주행 기반을 팀원들과 만들고, 팀을 이끌어 실차 대회를 완주했습니다**

ERP42 4륜 전기차 플랫폼 · 팀 MTP(충남대), 실개발 2~3인 · **팀장** (24.08~25.11)
**본인 담당:** 팀장(개발 일정 수립·공유, 실습 환경 구성, 인수인계 문서화) · waypoint 경로추종 · 명령 중재 판단 노드
**팀원들과 함께:** 센서 bring-up, EKF 센서퓨전 측위, 실차 테스트·튜닝

- **개요:** 예선 10분·본선 15분의 단일 자율주행 주행으로 차선 유지·GPS 음영구간·교차로·주차 미션을 통과해야 하는 대회입니다.
- **센서부터 차량까지:** 팀원들과 함께 LiDAR(Velodyne VLP-16)·카메라·IMU·RTK-GPS(보정 신호로 cm급 위치를 얻는 GPS)를 하나씩 붙이며 bring-up했고, 휠 인코더 기반 오도메트리(바퀴 회전량 기반 위치 추정)를 구현했습니다. 이 오도메트리를 IMU·GPS와 EKF(여러 센서 값을 신뢰도에 따라 합쳐 위치를 추정하는 필터)로 융합해, 120m 안팎의 GPS 음영구간에 대응하는 측위를 만들었습니다.
- **경로추종 (본인):** Pure Pursuit·Stanley 등 추종 기법을 학습·검토했고, 곡선에서 조향이 급격히 튀지 않도록 연구계획서의 설계대로 heading error(목표 방향과 현재 방향의 차이) 비례 조향에 직전 스텝과의 저역통과 blending을 더해 구현했습니다.
- **명령 중재 (본인):** 여러 인지 모듈이 제각각 제어 명령을 내면 오래된 명령이나 동시 명령을 통제할 지점이 없었습니다. 차선/경로 채널을 우선순위와 유효시간으로 중재하고, 유효한 입력이 없으면 full-brake하는 판단 노드를 prototype으로 설계했습니다.
- **실차에서 드러난 문제:** 시뮬레이션과 달리 실차에서는 카메라 frame drop, 전력 유지(보조배터리 추가), 주행 진동에 따른 카메라 각도·IMU 자세 영향, brake oil 누유, GNSS·ROS2 연결 끊김이 나왔습니다. 팀원들과 함께 튜닝 → 테스트 주행 → rosbag 로깅 → 분석을 반복하며 카메라·IMU 포트·RTK 접속·속도·brake 값을 실차에 맞춰 조정했습니다.
- **결과·한계:** 인지 모듈 일부가 빠져도 측위와 경로추종이 기본값으로 계속 동작해 팀 회고 기준으로 완주했습니다. 대회 순위와 정량 지표는 로그가 남아 있지 않아 적지 않았습니다.
- **회고:** 화려한 인지 기능보다 "무엇이 없어도 버티는가"를 먼저 설계해야 한다는 것, 그리고 성능 개발은 알고리즘보다 튜닝·테스트·로깅 반복에서 시작된다는 것을 배웠습니다.

<!-- <p align="center"><img src="./assets/erp42-demo.gif" alt="ERP42 실차 주행" width="720"></p> -->

<details>
<summary><b>프로젝트 기술 전체</b></summary>

- **측위:** 휠 오도메트리 + IMU + GPS(u-blox ZED-F9P, NTRIP RTK)를 GPS covariance 가중 EKF로 융합, pymap3d로 geodetic→ENU 변환. 보고서의 UKF와 달리 최종 코드는 EKF
- **경로계획·추종:** Bézier 곡선 경로계획 학습, OSM/JOSM 도로 경로 → UTM waypoint 생성, heading error P 조향 + 저역통과(`alpha=0.65`) blending
- **판단:** lane/path 2채널 우선순위·freshness timeout 중재, 입력 부재 시 full-brake (20Hz, source-level prototype)
- **인지:** 카메라 차선 인식(YOLO·HSV), LiDAR 장애물 인식(2D gap-following 설계 → 3D PCL/DBSCAN clustering 실험)
- **차량 I/O:** ERP42 40Hz serial packet 송수신, 경로추종·판단·통신을 역할별 ROS2 노드로 분리

</details>

🔗 개인 개발본: [Erp42_ws](https://github.com/gwanhuiGIM/Erp42_ws)

---

## 🧩 그 외 프로젝트 (진행 순)

<a id="lifeboat"></a>
### 🛟 열감지 추적 구명보트 전달장치 및 발사장치 — 학사 졸업프로젝트
**비싼 구조장비 대신, 제약 안에서 꼭 필요한 기능부터 골라 1/10 비용으로 만들었습니다**

Arduino Uno · 3인 팀 · 충남대 기계공학부 캡스톤디자인 (24.08~25.08) · 심화종합설계 PM
**본인 담당:** 좌우 DC 모터 차동 제어 · 아두이노 회로 구성 · 설계보고서 문서화
**팀원들과 함께:** 열화상 센서 처리, 센서·RC·모터 코드 통합, 보트 형상 설계

- **개요:** 상용 구조장비(500만~700만 원대)는 비싸고 조작이 어렵습니다. 비전문가가 바로 쓸 수 있도록 익수자에게 스스로 다가가 구명튜브를 전달하는 휴대형 구조 보트를 만들었습니다.
- **핵심 행동:** 착수 충격에 방향키가 부러질 위험과 고성능 모터의 제어 난이도를 근거로, 좌우 DC 모터 2개의 출력 차이로 방향을 트는 방식을 택하고 PWM(모터 속도를 조절하는 전기 신호) 차동 제어를 구현했습니다. 팀원들과 함께 열화상 센서(AMG8833, 8×8 온도 격자) 처리도 맡았습니다. 8비트 보드에서 64개 온도값을 매 루프 처리하기 어려워, 조향에는 좌우 정보만 필요하다는 점에 착안해 열별 최고 온도만 남겨 8칸으로 줄이고 가장 뜨거운 열의 위치로 방향을 정했습니다.
- **결과:** 총 제작비 약 51만 원(상용 대비 약 1/10), 교내 우수캡스톤 우수상·설계경진대회 우수상. 개회로 제어를 폐회로로 바꾸는 것은 다음 과제로 남겼습니다.

<!-- <p align="center"><img src="./assets/lifeboat.jpg" alt="구명보트와 발사장치" width="600"></p> -->

<details>
<summary><b>프로젝트 기술 전체</b></summary>

- **제어·임베디드:** Arduino Uno에서 AMG8833 열화상(8×8)을 열별 최고 온도로 1×8 축소해 열원 방향 판정 → L298N으로 좌우 DC 모터 차동 구동. RC 3채널 신호 유무로 수동/자율 자동 전환, 구명튜브 팽창 모터(수동식) 시퀀스
- **기구·해석:** SolidWorks 3D 모델 기반 3D 프린팅(PLA 선체, 착수 충격용 TPU) + 실리콘 방수 실링. ANSYS Fluent CFD(유동 해석)로 선체 항력계수 0.131→0.096 개선, SimSolid로 착수 하중(45° 착수·200N) 구조해석
- **발사장치:** 공기저항을 고려한 2차원 포물선 운동방정식으로 필요 힘을 산정해 스프링 선정, 컴파운드 석궁 방식 트리거·금속 몸체 제작(밀링, 용접 등). 발사거리 실측 9m(해석 14m)

</details>

🔗 프로젝트 기록: [Grad_proj](https://github.com/gwanhuiGIM/Grad_proj) (원본 코드 유실 — 논문 수록 코드로 재구성, 컴파일만 확인)

---

<a id="surgical"></a>
### 🩺 VLA 기반 수술도구 집도의 전달 시뮬레이션 (Isaac Sim)
**두 로봇의 상태와 수술도구 재고를 한 화면에서 보고 바로 조작하게 만들었습니다**

Dual Doosan M0609 · NVIDIA Isaac Sim · 팀 프로젝트 · ROKEY 1차 (26.06.17~26.06.30)
**본인 담당:** 웹 대시보드 UI·상호작용

- **개요:** 집도의가 손 동작·음성으로 이중 협동로봇을 조작해 수술도구 6종을 전달하는 시뮬레이션입니다.
- **핵심 행동:** 트레이별 재고 아이콘과 로봇 점유 상태를 SVG(벡터 그래픽)로 직접 그리고, 트레이를 클릭해 도구를 집거나 반납하는 상호작용을 구현했습니다. 트레이와 로봇 맵은 관련 상태가 바뀔 때만 다시 그리도록 해 화면 떨림을 막았습니다.

<!-- <p align="center"><img src="./assets/surgical-dashboard.png" alt="웹 대시보드 화면" width="720"></p> -->

<details>
<summary><b>프로젝트 기술 전체 · 코드 근거</b></summary>

- **손 동작 텔레오퍼레이션:** MediaPipe로 양손 위치·회전·제스처를 추적해 로봇 끝단 목표로 변환, FOLLOW/PLACE/WAITING 제스처 모드
- **음성 명령:** Whisper STT → Gemini가 도구 6종으로 분류, 가장 가까운 로봇이 해당 트레이로 이동해 전달·반납
- **비전:** Isaac Sim 카메라 영상에서 YOLOv8로 트레이별 도구/빈칸 인식, 로봇 보유 상태와 융합해 MISSING 판정, 도구 무작위 배치로 검증
- **작업 관리:** 두 로봇 작업 분배(가까운 로봇 우선), 교체·반납·PICK 도중 취소·중복 요청 방지
- **웹 대시보드:** FastAPI + WebSocket으로 손추적 영상·트레이 상태·로봇 상태·음성/명령 로그·Robot Map 실시간 표시
- **코드 근거:** [SVG 아이콘 — `index.html`](https://github.com/gwanhuiGIM/Rokey_cobot3/blob/main/dashboard/static/index.html#L167-L186) · [트레이 클릭 pick/return](https://github.com/gwanhuiGIM/Rokey_cobot3/blob/main/dashboard/static/index.html#L263-L291) · [상태 변경 시에만 재렌더링](https://github.com/gwanhuiGIM/Rokey_cobot3/blob/main/dashboard/static/index.html#L275-L280)

</details>

🔗 팀 최종 코드: [Rokey_cobot3](https://github.com/gwanhuiGIM/Rokey_cobot3) · 개인 개발본: [Personal_cobot3_ws](https://github.com/gwanhuiGIM/Personal_cobot3_ws)

---

<a id="amr"></a>
### 🚨 제조업 공장 산업안전 AMR 순찰로봇 및 관제 시스템
**에러 메시지 없이 로봇을 헛걸음시킬 수 있던 신호 흔들림을, 단계별로 쪼개 잡았습니다**

AMR 2대 · 천장 웹캠 2대 · 3인 팀 · ROKEY 2차 (26.07.01~26.07.14)
**본인 담당:** 관제 FSM(우선순위 선점)·쓰러짐 판정 규칙·메시지 전달 정책 설계와 디버깅

- **개요:** 천장 웹캠이 쓰러짐·안전모 미착용·무단침입을 감지하면 가장 가까운 AMR을 골라 출동시키는 안전관제 시스템입니다.
- **핵심 행동:** 응급 > 안전모 > 순찰 순으로 현재 작업을 선점하는 관제 상태머신을 설계했습니다. 쓰러지는 순간 응급 발동·해제 신호가 1초 사이 5번 뒤집히던 문제(코드 디버깅 기록)는, 발동은 그대로 두고 해제 방향에만 지연 조건을 걸어 응급 반응 속도를 지키면서 막았습니다. 새 출동 명령이 이전 작업을 취소할 때 "이동 끝"으로 오인해 재배정이 반복되던 문제는 "취소 중" 상태를 따로 구분해 해결했습니다. 쓰러짐 판정은 "누우면 머리가 발 위에 있다"는 가정이 깨지는 머리 높이 신호 대신, 몸통 각도를 주지표로 삼고 다리가 서 있으면 거부하는 방식으로 바꿨습니다.
- **회고:** 에러 없이 조용히 틀리는 문제일수록 신호를 단계별로 쪼개 원인을 좁혀야 한다는 것을 배웠습니다.

<!-- <p align="center"><img src="./assets/amr-control.png" alt="AMR 관제 화면" width="720"></p> -->

<details>
<summary><b>프로젝트 기술 전체 · 코드 근거</b></summary>

- **감지(천장 웹캠 2대):** YOLO11-pose 자세 추정 + YOLOv8 안전모 검출(Roboflow 라벨링 → 학습), 호모그래피·Z 캘리브레이션(DLT 투영행렬)으로 map 좌표 변환, 두 카메라 간 동일 인물 통합(Re-ID)
- **관제:** `fleet_fsm`이 최근접 로봇 선정·접근점 계산·큐 관리·상황 상태머신(NORMAL↔EMERGENCY) 수행, rosbridge 웹 관제 화면(출동 근거·이벤트 주입)
- **메시지 정책:** 상태 라벨·좌표 명령·영상의 QoS(메시지 전달 보장 정책)를 의미별로 분리, timestamp 기준 30초를 넘긴 명령은 버려 오래된 명령의 재출동 위험 감소
- **로봇 실행부:** TurtleBot4 Nav2/AMCL 주행·순찰·도킹, OAK-D 카메라로 소화기 ArUco 마커 인식
- **점검 DB:** ArUco 인식 결과로 소화기 점검 이력 갱신, SQLite + Flask 웹 조회
- **코드 근거:** [해제 방향 디바운스 — `ros_bridge.py`](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/1_vision_pc3/safety_lib/ros_bridge.py#L473-L499) · [의미별 QoS](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/1_vision_pc3/safety_lib/ros_bridge.py#L75-L126) · [`CANCELING` 처리 — `fleet_fsm.py`](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/2_ros2_packages/fp_amr_fsm/fp_amr_fsm/fleet_fsm.py#L565-L574) · [쓰러짐 판정 — `safety_logic.py`](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/1_vision_pc3/safety_lib/safety_logic.py#L230-L275) · [30초 stale 필터](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/2_ros2_packages/fp_amr_fsm/fp_amr_fsm/amr_patrol_emer_helmet.py#L385-L403)

</details>

🔗 팀 최종 코드: [Rokey_intelli1](https://github.com/gwanhuiGIM/Rokey_intelli1)

---

<a id="coffee"></a>
### ☕ 협동로봇 핸드드립 커피 자동화
**카메라 없이 힘·접점 신호만으로, "잡았는지 모르는" 순간을 따로 분리해 안전하게 멈췄습니다**

Doosan M0609 + OnRobot RG2 · 5인 팀 · ROKEY 3차 (26.07.15~26.07.29)
**본인 담당:** 그리퍼 예외 상황 처리 및 정상 공정 복귀 알고리즘(팀 README 역할표 기준)

- **개요:** 비전 센서 없이 원두 계량부터 나선형 드립까지 5단계 추출 공정을 로봇 제어만으로 자동화했습니다.
- **핵심 행동:** 파지 성공 신호(grip 비트)가 안 떠도 관절 힘·위치에 접촉 흔적이 있으면 "판정 불가"로 따로 분류해, 물체를 문 채 다시 잡으러 가는 사고를 막았습니다. 공정 중 그리퍼 신호가 1초 넘게 끊기면 감시 루프(watchdog)가 정지를 요청하고, 실패한 단계만 다시 할지 멈출지는 작업자가 고르게 했습니다. 반복 파지 중 공정 전체가 죽던 로거 버그는 ROS2 내부 동작까지 추적해 해결했습니다.
- **회고:** 애매한 신호를 성공/실패 둘로 뭉개지 않고 별도 상태로 다뤄야 안전하다는 것을 배웠습니다.

<!-- <p align="center"><img src="./assets/coffee-demo.gif" alt="나선 드립 시연" width="600"></p> -->

<details>
<summary><b>프로젝트 기술 전체 · 코드 근거</b></summary>

- **5단계 공정:** 원두 계량 → 그라인딩 → 드리퍼 투입 → 나선 드립 → 컵에 붓기, 공정 1단계 = 파일 1개로 분리하고 `RobotContext`로 모션 API·포즈·감시자 주입
- **힘·순응 제어:** 순응 제어 상태에서 원호 모션으로 그라인딩(크랭크 회전 수 = 분쇄 굵기), 드리퍼 투입 단계는 기준 대비 4.0 N 이상 외력으로 병 두드림 감지
- **나선 드립 궤적:** 위치는 삼각함수, 자세는 회전행렬로 6D 경유점 직접 생성 → 유량 편차를 줄이도록 호길이 기준 등간격 100개 경유점으로 재표본화, 5차 smoothstep으로 기울기 blend
- **예외처리·UI:** 20Hz fail-closed watchdog의 `MoveStop` 요청, 단계 복구 FSM, 버튼(DI) 기반 원두·굵기 선택, FastAPI 기반 공정 진행·단계 테스트·관리자 웹 화면
- **구현 위치:** watchdog·복구 FSM은 팀 제출본, 3값 파지 판정·로거 수정·pytest 7종은 병행 개발본(비공개)
- **코드 근거:** [watchdog — `grip_monitor.py`](https://github.com/gwanhuiGIM/Rokey_cobot1/blob/main/src/rokey/rokey/coffee/grip_monitor.py#L253-L322) · [단계 복구 — `recovery.py`](https://github.com/gwanhuiGIM/Rokey_cobot1/blob/main/src/rokey/rokey/coffee/recovery.py#L346-L414)

</details>

🔗 팀 최종 코드: [Rokey_cobot1](https://github.com/gwanhuiGIM/Rokey_cobot1) · 개인 개발본: [Personal_cobot1_ws](https://github.com/gwanhuiGIM/Personal_cobot1_ws)

---

<a id="bring"></a>
## 💡 What I bring

1. **조용한 실패를 신호 단계로 쪼개 잡습니다** — 에러 없이 "성공처럼 보이는" 문제를 원인 후보로 나누고 재현해 좁혀 왔습니다(VLA 인지 게이트, AMR 신호 흔들림, 커피 파지 판정).
2. **판단과 안전을 분리해 통합합니다** — 여러 모듈이 로봇에 명령하는 구조에서 제어 권한을 한 곳으로 모으고, 명령이 없거나 낡았을 때 멈추는 쪽으로 설계합니다(VLA 계층 통합, ERP42 판단 노드 prototype).
3. **실기로 확인하고 기록으로 남깁니다** — 기능이 실제 장치에서 동작하는지 실기로 확인하고, 실측 제약과 실패를 기록해 다음 실험과 인수인계의 근거로 남깁니다(VLA 실측 제약 문서, ERP42 실차 테스트·인수인계).

센서·통신·제어가 실제 장치에서 끝까지 동작하는 로봇 시스템을 만드는 데 이 습관을 쓰겠습니다.
**김관희** · 📫 gwanhuig01@gmail.com · 🐙 [github.com/gwanhuiGIM](https://github.com/gwanhuiGIM)

---

<a id="repos"></a>
## 🗂️ 저장소 모음

| 프로젝트 | 팀 최종 제출본 | 개인 개발본 |
|:--|:--|:--|
| 🛟 열감지 추적 구명보트 (졸업프로젝트) | — | [Grad_proj](https://github.com/gwanhuiGIM/Grad_proj) |
| 🚗 자율주행 ERP42 | — | [Erp42_ws](https://github.com/gwanhuiGIM/Erp42_ws) |
| 🩺 수술도구 전달 시뮬레이션 | [Rokey_cobot3](https://github.com/gwanhuiGIM/Rokey_cobot3) | [Personal_cobot3_ws](https://github.com/gwanhuiGIM/Personal_cobot3_ws) |
| 🚨 산업안전 AMR 관제 | [Rokey_intelli1](https://github.com/gwanhuiGIM/Rokey_intelli1) | — |
| ☕ 핸드드립 커피 자동화 | [Rokey_cobot1](https://github.com/gwanhuiGIM/Rokey_cobot1) | [Personal_cobot1_ws](https://github.com/gwanhuiGIM/Personal_cobot1_ws) |
| 🦾 VLA Pick & Place | [Rokey_cobot2](https://github.com/gwanhuiGIM/Rokey_cobot2) | [Personal_cobot2_ws](https://github.com/gwanhuiGIM/Personal_cobot2_ws) |

<sub>팀 최종 제출본은 발표·제출 시점 코드이고, 개인 개발본은 프로젝트 중·후에 개인적으로 실험하고 정리한 작업본입니다(미완성 패키지 포함).</sub>
