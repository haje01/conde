# conde

conde (콘드) 는 쿠버네티스 환경에서 Kafka Connect (카프카 커넥트) 를 설치하고, Connector (커넥터) 를 배포해주는 툴이다. 다음과 같은 기능을 한다.

- Connect 를 위한 K8S 리소스 생성
  - 필요시 외부 파일 다운로드 및 설치
- 새로운 Connector 를 등록
- 등록된 Connector 를 제거
- 등록된 Connector 의 설정을 바꾸어 새로 재등록
- 멱등적 (Idempotent) 으로 동작하기에, 조건이 변하지 않는 한 몇 번이고 실행해도 괜찮다.

### 관련 지식

- Connect 
  - Connector 를 배포하기 위한 인프라 (클러스터) 역할
  - Worker, Connector, Task 를 구성요소로 가짐
  - 수평적 스케일링 (Horizontal Scaling) 을 지원
  - Connector 위치, 변환, 에러 처리등에 관한 설정을 가짐
  - 분산 모드 (Distribute Mode)
    - 클러스터에 복수의 워커를 생성하여 수평적 스케일링
    - 워커가 실패하면 그곳의 Task 들은 다른 워커에 배정됨
    - 동시에 복수의 Task 를 실행하여 동시성 구현
- Connector
  - 작업을 위한 고수준 설정 및 로직 구현을 가짐 
  - 실제로 작업을 하는 것은 연관된 Task
  - Connector 가 시작/설정되면 Connect 가 Worker 에 하나 이상의 Task 를 생성
- Connect Worker 
  - Connect 클러스터의 멤버로 실행되는 개별 프로세스 
  - Connect 클러스터는 복수의 워커로 구성
  - Connector 및 Source/Sink Task 를 조율
  - 각 워커는 하나 이상의 커넥터 및 관련 태스크를 다룸
  - 워커들은 서로 통신하며 태스크 배정, 로드 밸런싱, 조율을 진행
  - K8S 환경에서 Worker 는 하나의 Pod 로 취급
- Connect Task
  - 실제 데이터 작업을 수행하는 Kafka Connect 의 가장 작은 단위
  - 데이터를 읽거나 (Source Task), 데이터를 저장 (Sink Task)
  - 각 태스크는 카프카 토픽내 하나의 파티션을 담당
  - K8S 환경에서 Worker Pod 당 하나 이상의 Task 가 배정

## 시작하기

conde 는 프로젝트 파일을 YAML 형식으로 기술한다. 다음은 간단한 예이다.

```yaml

```

## TODO
