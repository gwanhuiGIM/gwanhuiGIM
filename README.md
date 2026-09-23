# Kim KwanHee (김관희) — Robotics Portfolio

센서 신호가 제어 동작으로 이어지는 로봇 시스템을 만들어 왔습니다.
학부 때 아두이노로 모터를 제어하는 일에서 시작해, 자율주행 대회 팀장을 거쳐 ROS2 기반 협동로봇·AMR 프로젝트에서 상태관리, 안전 게이트, 인지-모션 통합을 맡았습니다.
각 카드에는 프로젝트에서 구현한 기술을 모두 적고, 그중 역할 분담상 제가 맡은 부분을 따로 표시했습니다.

📫 wook9980@gmail.com

| | |
|:--|:--|
| 🎓 학력 | 충남대학교 기계공학부 학사 졸업 (2026.08) |
| 🤖 교육 | 두산로보틱스 ROKEY 부트캠프 8기 — 지능형 로보틱스 엔지니어 (26.02~26.08) |
| 🏆 수상 | 교내 우수캡스톤디자인 경진대회 우수상 (24.11) · 교내 설계경진대회 우수상 (25.08) · 한국기계학회 설계경진대회 본선 진출 (25.08) |
| 📜 자격·어학 | SOLIDWORKS CSWP (Design Professional) · OPIc IH |
| 🛠️ 스킬 | `ROS2 Humble` `Python` `C++` `Ubuntu` `MoveIt` `Nav2` `Arduino` `SolidWorks` |

### 🧭 성장 흐름
**아두이노 임베디드**(졸업프로젝트 · 모터 차동 제어) → **ROS2, 센서 활용 차량 자율주행 대회**(ERP42 · 팀장) → **협동로봇·AMR을 활용한 부트캠프 프로젝트 진행 - 계획·설계·구현·통합·결과보고**(ROKEY 4개 프로젝트) → **예외처리 설계·논문/오픈소스 분석 기반 설계·기준환경 대조 실기 테스트·개발 기록 문서화**(VLA Pick & Place)

<!-- ponytail: 본문 카드는 프로젝트 진행 기간 순(사용자 지정). 강약 조절은 순서 대신 상단 '대표 프로젝트' pin으로 처리. -->

> ### 🔖 대표 프로젝트
> 🦾 **VLA 기반 자연어 Pick & Place - 협동로봇 장애물 감지 및 경로 수정 로직 구현** — 판단·안전 계층 통합 + 대조군 A/B로 재계획 로직 검증 · 부트캠프 앞선 3개 프로젝트 경험을 모은 마지막 작업 · `FSM` `안전 게이트` `LLM function calling`
> 🚗 **자율주행 ERP42** — 3인 팀장, 센서퓨전 측위·waypoint 경로추종을 ROS2로 통합해 실차 대회 주행 + lane/path 판단 노드 prototype 구현 · `EKF` `Waypoint Pathtracking` `ROS2`

---

## 🎓 학부 프로젝트

### 🛟 열감지 추적 구명보트 전달장치 및 발사장치 (학사 졸업프로젝트)
Arduino Uno · 3인 팀 · 충남대 기계공학부 캡스톤 (24.08~25.08)
**주요 담당:** 좌우 DC 모터 차동 제어 · 아두이노 회로 구성 · 설계보고서 문서화 (심화종합설계 PM)
`Arduino` `PWM 차동 제어` `AMG8833 열화상` `SolidWorks` `3D 프린팅` `CFD` `구조해석`

- **목적:** 상용 구조장비는 500만~700만 원대로 비싸고 숙련된 조작이 필요합니다. 비전문가가 바로 쓸 수 있도록, 익수자에게 스스로 다가가 구명튜브를 전달하는 휴대형 구조 보트를 만들었습니다.
- **프로젝트 기술:**
  - **제어·임베디드:** Arduino Uno 단일 보드에서 AMG8833 열화상(8×8)을 열별 최고 온도로 1×8 축소해 열원 방향 판정 → L298N으로 좌우 DC 모터 차동 구동. RC 3채널 신호 유무로 수동/자율 자동 전환, 구명튜브 팽창 모터(수동식) 시퀀스
  - **기구·해석:** SolidWorks 3D 모델 기반 3D 프린팅(PLA 선체, 착수 충격용 TPU) + 실리콘 방수 실링. ANSYS Fluent CFD로 선체 항력계수 0.131→0.096 개선, SimSolid로 착수 하중(45° 착수·200N) 구조해석
  - **발사장치:** 공기저항을 고려한 2차원 포물선 운동방정식으로 필요 힘을 산정해 스프링 선정, 컴파운드 석궁 방식 트리거·금속 몸체 제작
- **본인 담당:** 착수 충격(방향키 파손 위험)과 아두이노 제어 난이도(BLDC)를 근거로 좌우 DC 모터 2개의 출력 차이로 방향을 트는 방식을 택하고, 열원 방향에 따라 좌우 모터에 서로 다른 PWM을 주는 차동 제어를 구현했습니다. 열화상 처리와 센서·RC·모터 코드 통합은 팀원과 함께 진행했고, 회로 구성과 설계보고서 문서화를 맡았습니다.
- **결과·상태:** 총 제작비 약 51만 원(상용 대비 약 1/10), 발사거리 실측 9m(해석 14m). 교내 우수캡스톤 우수상·설계경진대회 우수상. 제어는 개회로(open-loop) PWM이라 폐회로 제어 전환을 과제로 남겼습니다.

🔗 공개 repository 없음 (원본 코드 유실 — 논문 수록 코드로 재구성, 컴파일만 확인)

---

### 🚗 자율주행 ERP42 (2025 대학생 창작 모빌리티 경진대회 · 무인모빌리티 부문)
ERP42 4륜 전기차 플랫폼 · 팀 MTP(충남대), 실개발 2~3인 · **팀장** (24.08~25.11)
**주요 담당:** Waypoint pathtracking · lane/path 판단 노드(Controller) · 팀장(개발 일정 수립·공유, 실습 환경 구성, 인수인계 문서화)
`ROS2 Humble` `EKF 센서퓨전` `Waypoint Pathtracking` `Velodyne LiDAR` `RTK-GPS` `YOLO`

- **목적:** 예선 10분·본선 15분의 단일 자율주행 run으로 차선 유지·GPS 음영구간·교차로·주차 미션을 통과해야 하는 대회.
- **프로젝트 기술:**
  - **측위:** 휠 오도메트리 + IMU + GPS(u-blox ZED-F9P, NTRIP RTK)를 GPS covariance 가중 EKF로 융합, pymap3d로 geodetic→ENU 변환 — 120m 안팎 GPS 음영구간 대응
  - **경로추종·판단:** waypoint pathtracking, lane/path 명령 중재 Controller 노드
  - **인지:** 카메라 차선 인식(YOLO·HSV), Velodyne VLP-16 LiDAR 장애물 인식(2D gap-following 설계 → 3D PCL/DBSCAN clustering 실험)
  - **차량 I/O:** ERP42 40Hz serial packet 송수신, 역할별 ROS2 노드 분리
- **본인 담당:** 곡선에서 조향이 급격히 튀지 않도록, Pure Pursuit·Stanley를 검토한 뒤 heading error 비례 조향에 직전 스텝과의 저역통과 blending(`alpha=0.65`)을 적용한 waypoint pathtracking을 구현했습니다. 여러 인지 모듈이 제각각 제어 명령을 내는 문제는, lane/path 채널을 우선순위와 freshness timeout으로 중재하고 유효 입력이 없으면 full-brake하는 20Hz 판단 노드(Controller)로 정리했습니다(source-level prototype).
  팀장으로서 개발 일정을 세워 공유하고, 팀원이 바로 개발에 들어가도록 실습 환경을 구성했으며, 작업 이력을 인수인계 자료로 남겼습니다.
- **결과·상태:** 인지 모듈 일부가 빠져도 측위와 경로추종이 기본값으로 계속 동작해 팀 회고 기준으로 완주했습니다. 대회 순위와 정량 지표는 로그가 남아 있지 않아 적지 않았습니다. 보고서(UKF)와 최종 코드(EKF)가 다른 부분은 코드 기준으로 정리했습니다.

<!-- TODO: 대표 gif/이미지 삽입 — 실차 주행 또는 LiDAR 클러스터링 시각화 (경로: assets/erp42-demo.gif) -->
<!-- ![ERP42 자율주행 데모](assets/erp42-demo.gif) -->

🔗 상세 case study 정리 중 · 현재 공개 repository 없음

---

## 🤖 ROKEY 부트캠프 프로젝트 *(팀 제출 완료작)*
*두산로보틱스 지능형 로보틱스 엔지니어 과정 (26.02~26.08, 비대면 4개월 + 대면 프로젝트 2개월) — ROS2 · Doosan M0609 협동로봇 · AMR.* 진행 순서대로 적었습니다.

### 🩺 VLA 기반 수술도구 집도의 전달 시뮬레이션 (Isaac Sim)
Dual Doosan M0609 · NVIDIA Isaac Sim · 팀 프로젝트 · 1차 (26.06.17~26.06.30)
**주요 담당:** 웹 대시보드 UI·상호작용
`Isaac Sim` `MediaPipe` `Whisper` `Gemini` `YOLOv8` `FastAPI/WebSocket` `SVG`

- **목적:** 집도의가 손 동작·음성으로 이중 협동로봇을 조작해 수술도구 6종을 전달하는 시뮬레이션.
- **프로젝트 기술:**
  - **손 동작 텔레오퍼레이션:** MediaPipe로 양손 위치·회전·제스처를 추적해 EE 목표로 변환, FOLLOW/PLACE/WAITING 제스처 모드
  - **음성 명령:** Whisper STT → Gemini가 도구 6종으로 분류, 가장 가까운 로봇이 해당 트레이로 이동해 전달·반납
  - **비전:** Isaac Sim 카메라 영상에서 YOLOv8로 트레이별 도구/빈칸 인식, 로봇 보유 상태와 융합해 MISSING 판정, 도구 무작위 배치로 검증
  - **작업 관리:** 두 로봇 작업 분배(가까운 로봇 우선), 교체·반납·PICK 도중 취소·중복 요청 방지
  - **웹 대시보드:** FastAPI + WebSocket으로 손추적 영상·트레이 상태·로봇 상태·음성/명령 로그·Robot Map 실시간 표시
- **본인 담당:** 웹 대시보드 UI·상호작용. 트레이별 재고 아이콘과 로봇 점유 상태를 SVG로 직접 렌더링하고, 트레이를 클릭해 도구를 집거나 반납하는 상호작용을 구현했습니다. 트레이와 로봇 맵은 관련 상태가 바뀔 때만 다시 그리도록 렌더링도 최적화했습니다.
- **코드 근거:** [SVG 아이콘 — `index.html`](https://github.com/gwanhuiGIM/Rokey_cobot3/blob/main/dashboard/static/index.html#L167-L186) · [트레이 클릭 pick/return](https://github.com/gwanhuiGIM/Rokey_cobot3/blob/main/dashboard/static/index.html#L263-L291) · [상태 변경 시에만 재렌더링](https://github.com/gwanhuiGIM/Rokey_cobot3/blob/main/dashboard/static/index.html#L275-L280)

🔗 팀 최종 코드: [Rokey_cobot3](https://github.com/gwanhuiGIM/Rokey_cobot3)

---

### 🚨 제조업 공장 산업안전 AMR 순찰로봇 및 관제 시스템
AMR 2대 · 천장 웹캠 2대 · 3인 팀 · 2차 (26.07.01~26.07.14)
**주요 담당:** 우선순위 선점 FSM · 쓰러짐 판정 규칙 · 메시지 의미별 QoS 설계
`YOLO11-pose` `YOLOv8` `Nav2/AMCL` `TurtleBot4` `우선순위 선점 FSM` `QoS 분리` `SQLite/Flask`

- **목적:** 천장 웹캠이 쓰러짐·안전모 미착용·무단침입을 감지하면 가장 가까운 AMR을 골라 출동시키는 안전관제 시스템.
- **프로젝트 기술:**
  - **감지(천장 웹캠 2대):** YOLO11-pose 자세 추정 + YOLOv8 안전모 검출(Roboflow 라벨링 → 학습), 호모그래피·Z 캘리브레이션(DLT 투영행렬)으로 map 좌표 변환, 두 카메라 간 동일 인물 통합(Re-ID)
  - **관제:** `fleet_fsm`이 최근접 로봇 선정·접근점 계산·큐 관리·상황 상태머신(NORMAL↔EMERGENCY) 수행, rosbridge 웹 관제 화면(출동 근거·이벤트 주입)
  - **로봇 실행부:** TurtleBot4 Nav2/AMCL 주행·순찰·도킹, OAK-D 카메라로 소화기 ArUco 마커 인식
  - **점검 DB:** ArUco 인식 결과로 소화기 점검 이력 갱신, SQLite + Flask 웹 조회
- **본인 담당:** 응급 > 안전모 > 순찰 순으로 현재 작업을 선점하는 FSM을 설계했습니다. 쓰러진 직후 1초 사이 응급 발동·해제가 0.1초 간격으로 5번 뒤집히던 채터링(코드 디버깅 기록)에 대응해, 발동 방향은 그대로 두고 해제 방향에만 1.5초 디바운스를 걸었습니다. 새 goal이 이전 작업을 취소할 때 Nav2 상태가 잠깐 "종료"로 보여 재배정이 반복되던 문제는 `CANCELING`을 진행 중으로 분류해 해결했습니다. 쓰러짐 판정은 머리 높이 단일 신호("누우면 머리가 발 위에 있다"는 가정이 깨짐)에서 몸통 각도 주지표 + 다리 거부권 방식으로 바꿨습니다. 상태 라벨·좌표 명령·영상의 QoS를 의미별로 나누고, timestamp 기준 30초를 넘긴 명령은 버리도록 해 오래된 명령이 재출동을 일으킬 위험을 줄였습니다.
- **코드 근거:** [해제 방향 디바운스 — `ros_bridge.py`](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/1_vision_pc3/safety_lib/ros_bridge.py#L473-L499) · [의미별 QoS](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/1_vision_pc3/safety_lib/ros_bridge.py#L75-L126) · [`CANCELING` 처리 — `fleet_fsm.py`](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/2_ros2_packages/fp_amr_fsm/fp_amr_fsm/fleet_fsm.py#L565-L574) · [쓰러짐 판정 — `safety_logic.py`](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/1_vision_pc3/safety_lib/safety_logic.py#L230-L275) · [30초 stale 필터](https://github.com/gwanhuiGIM/Rokey_intelli1/blob/main/src/2_ros2_packages/fp_amr_fsm/fp_amr_fsm/amr_patrol_emer_helmet.py#L385-L403)

🔗 팀 최종 코드: [Rokey_intelli1](https://github.com/gwanhuiGIM/Rokey_intelli1)

---

### ☕ 협동로봇 핸드드립 커피 자동화
Doosan M0609 + OnRobot RG2 · 5인 팀 · 3차 (26.07.15~26.07.29)
**주요 담당:** 그리퍼 파지 판정 · 통신 watchdog · 단계별 복구 FSM
`ROS2` `DSR API` `순응/힘 제어` `movesx 궤적` `FastAPI 웹` `fail-closed watchdog` `복구 FSM`

- **목적:** 비전 센서 없이 원두 계량부터 나선형 드립까지 5단계 추출 공정을 로봇 제어만으로 자동화.
- **프로젝트 기술:**
  - **5단계 공정:** 원두 계량 → 그라인딩 → 드리퍼 투입 → 나선 드립 → 컵에 붓기, 공정 1단계 = 파일 1개로 분리하고 `RobotContext`로 모션 API·포즈·감시자 주입
  - **힘·순응 제어:** 순응 제어 상태에서 원호 모션으로 그라인딩(크랭크 회전 수 = 분쇄 굵기), 드리퍼 투입 단계는 기준 대비 4.0 N 이상 외력으로 병 두드림 감지
  - **나선 드립 궤적:** 위치는 삼각함수, 자세는 회전행렬로 6D 경유점 직접 생성 → 유량 편차를 줄이도록 호길이 기준 등간격 100개 경유점으로 재표본화, 5차 smoothstep으로 기울기 blend
  - **예외처리·UI:** 그리퍼 감시·단계 복구, 버튼(DI) 기반 원두·굵기 선택, FastAPI 기반 공정 진행·단계 테스트·관리자 웹 화면
- **본인 담당:** 카메라가 없어 성공·실패를 힘·접점·통신 신호로만 판정해야 했습니다. grip 비트가 안 떠도 effort/position에 접촉 흔적이 있으면 "판정 불가"로 따로 분류하는 3값 파지 판정과 단계별 복구 FSM을 만들었습니다. 공정 단계 실행 중 그리퍼 상태가 1초 넘게 수신되지 않으면 20Hz fail-closed watchdog이 `MoveStop`을 요청하고, 재시도·중단은 작업자가 고릅니다. 반복 파지 중 rclpy 로거 severity 캐시 때문에 공정 전체가 죽던 문제는 프레임워크 내부까지 추적해, 로그 호출을 분기별로 나눠 해결했습니다.
- **구현 범위·상태:** 팀 제출 완료작(팀 README 기여표상 본인 역할: "그리퍼 예외 상황 처리 및 정상 공정 복귀 알고리즘"). watchdog·복구 FSM은 제출본에 있고, 3값 파지 판정·로거 수정·pytest 7종은 병행 개발본(비공개)에 있습니다.
- **코드 근거:** [watchdog — `grip_monitor.py`](https://github.com/gwanhuiGIM/Rokey_cobot1/blob/main/src/rokey/rokey/coffee/grip_monitor.py#L253-L322) · [단계 복구 — `recovery.py`](https://github.com/gwanhuiGIM/Rokey_cobot1/blob/main/src/rokey/rokey/coffee/recovery.py#L346-L414)

🔗 팀 최종 코드: [Rokey_cobot1](https://github.com/gwanhuiGIM/Rokey_cobot1) · 개인 개발본: [Personal_cobot1_ws](https://github.com/gwanhuiGIM/Personal_cobot1_ws)

---

### 🦾 VLA 기반 자연어 Pick & Place — 환경 인식 및 정적 장애물 회피
Doosan M0609 + RG2 + RealSense D435i · 5인 팀 · 4차 (26.07.30~26.08.12)
**주요 담당:** 판단 계층·안전 계층 통합, 인지 실패 감지 게이트
`GPT-5-mini function calling` `YOLO` `GraspGenX` `cuMotion/cuRobo` `nvblox` `MoveIt` `FSM`

- **목적:** "빨간 컵을 상자로 옮겨줘" 같은 자연어 지시를 로봇이 수행.
- **프로젝트 기술:**
  - **판단 계층(VLM):** 규칙으로 처리 가능한 지시는 LLM 없이(Tier 1), 나머지는 GPT-5-mini + 카메라 사진 대화(Tier 2)로 무엇을·몇 개를·어디로 옮길지 결정. 손가락 가리키기 선택, 다중 물체 순차 처리, "컵은 담지 마" 같은 규칙 기억, "멈춰" 즉시 정지
  - **인식·파지:** 거치형 RealSense(eye-to-hand 캘리브레이션) + YOLO 물체 인식 → GraspGenX 파지 후보 생성
  - **재계획 모션:** nvblox ESDF(장애물 표면까지의 거리를 담은 3D 거리장) 기반 cuMotion(cuRobo) 3Hz 재계획 로직 구현·실험 — 출발 전 장애물 반영 우회는 확인, 실행 중 회피는 검증 미완료
  - **안전 계층:** deterministic pick FSM이 모션 취소·그리퍼 개폐·물체 보유·충돌 씬을 전담, 판단 계층과는 JSON 3채널로만 연결
- **본인 담당:** 판단 LLM 계층과 안전 계층(pick FSM)이 각자 로봇을 직접 제어하던 구조를 통합해, 제어 권한을 안전 계층 하나로 좁혔습니다. 인지 파이프라인 상태를 모션 계획 성공 여부와 따로 확인하는 게이트를 넣어 "인식은 죽었는데 계획만 성공"하는 조용한 실패를 잡도록 했습니다. 재계획 로직은 같은 노드에서 재계획 OFF(대조군)와 ON을 실기로 비교했습니다. OFF는 7.7초 만에 도착했지만 3Hz 무조건 교체는 궤적을 155번 갈아끼우다 60초 타임아웃으로 실패해, 같은 경로일 때는 교체를 건너뛰도록 고쳤습니다. 실행 경로(MoveIt 실행관리자 vs JTC 직접 실행)도 실험군/대조군 파일로 분리해 비교했습니다.
- **구현 범위·상태:** 판단 계층 설계는 팀, 통합·안전 게이트는 본인 담당(재계획 실행 코드는 팀 계보). 설계·실측 제약·실험 기록을 문서로 남겼습니다. 출발 전 투입한 장애물을 반영한 우회는 실기로 확인했고, 실행 중 장애물 회피와 전체 pick-to-place 실물 검증은 마치지 못했습니다.
- **코드 근거:** [24개 동작 상태 pick FSM — `states.py`](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/src/pick_fsm/pick_fsm/states.py#L20-L44) · [이동 전 ESDF 게이트 — `arm.py`](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/src/cumotion/cumotion/arm.py#L361-L372) · [동일 경로 교체 생략 — `_same_path`](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/src/cumotion/cumotion/arm.py#L757-L794) · [A/B 실측 기록](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/docs/fsm/cumotion-experiment-log.md?plain=1#L594-L606) · [실측 제약 문서 — `constraints.md`](https://github.com/gwanhuiGIM/Rokey_cobot2/blob/main/docs/fsm/context/constraints.md)

<!-- TODO: 대표 gif/이미지 삽입 — 자연어 지시 → pick-to-place 데모 또는 안전 게이트 flow diagram (경로: assets/vla-pick-demo.gif) -->
<!-- ![VLA Pick & Place 데모](assets/vla-pick-demo.gif) -->

🔗 팀 최종 코드: [Rokey_cobot2](https://github.com/gwanhuiGIM/Rokey_cobot2) · 개인 개발본: [Personal_cobot2_ws](https://github.com/gwanhuiGIM/Personal_cobot2_ws)

---

## 🗂️ 저장소 모음

| 프로젝트 | 팀 최종 제출본 | 개인 개발본 |
|:--|:--|:--|
| 🩺 수술도구 전달 시뮬레이션 | [Rokey_cobot3](https://github.com/gwanhuiGIM/Rokey_cobot3) | [Personal_cobot3_ws](https://github.com/gwanhuiGIM/Personal_cobot3_ws) |
| 🚨 산업안전 AMR 관제 | [Rokey_intelli1](https://github.com/gwanhuiGIM/Rokey_intelli1) | — |
| ☕ 핸드드립 커피 자동화 | [Rokey_cobot1](https://github.com/gwanhuiGIM/Rokey_cobot1) | [Personal_cobot1_ws](https://github.com/gwanhuiGIM/Personal_cobot1_ws) |
| 🦾 VLA Pick & Place | [Rokey_cobot2](https://github.com/gwanhuiGIM/Rokey_cobot2) | [Personal_cobot2_ws](https://github.com/gwanhuiGIM/Personal_cobot2_ws) |

<sub>팀 최종 제출본은 발표·제출 시점 코드이고, 개인 개발본은 프로젝트 중·후에 개인적으로 실험하고 정리한 작업본입니다(미완성 패키지 포함). ERP42 상세 case study는 정리되는 대로 링크를 추가합니다.</sub>
