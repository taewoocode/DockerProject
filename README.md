## 분산 시스템 로그 및 메트릭 수집, 저장, 시각화 시스템 구축

**1. 프로젝트 개요**

이 프로젝트는 분산 시스템에서 발생하는 로그 및 메트릭 데이터를 효율적으로 수집, 저장하고 시각화하는 시스템을 구축하는 것을 목표로 합니다. 이 시스템은 Docker Swarm을 기반으로 하여 ELK Stack와 MariaDB를 통합하여 구성됩니다.

**2. 프로젝트 목표**

- 로그 및 메트릭 데이터의 실시간 수집 및 저장
- 데이터의 시각적인 분석과 모니터링을 위한 대시보드 구축
- 시스템의 안정성과 확장성 확보

**3. 프로젝트 구성 요소**

- Docker Swarm: 5개의 노드로 구성된 분산 환경 구성
- ELK Stack: Elasticsearch, Logstash, Kibana를 통한 로그 수집, 분석 및 시각화
- Grafana 및 Prometheus: 메트릭 수집 및 대시보드 시각화
- MariaDB: 데이터베이스로서 Worker 3에 저장되는 데이터 관리

**4. 주요 기능**

- Manager 역할을 하는 Worker 0을 통해 클러스터 관리 및 Worker 역할 변경 관리
- Worker 1과 Worker 2에서는 Elasticsearch 및 Metricbeat를 sidecar로 사용하여 데이터 수집
- Worker 3에서는 Worker 1과 2에서 수집한 데이터를 MariaDB에 저장
- Manager에서는 Worker 3의 MariaDB 데이터를 Kibana를 통해 시각화

**5. 예상 결과물**

- 실시간으로 로그 및 메트릭 데이터를 수집하고 저장하는 분산 시스템
- 데이터를 시각적으로 분석하고 모니터링할 수 있는 대시보드 제공
- 시스템의 성능, 안정성 및 확장성에 대한 실시간 모니터링 및 관리 기능

**6. 예상 일정 ### 주를 일 단위로 변경**

- 요구 사항 분석 및 설계: 1주
- 환경 설정 및 구성: 2주
- 기능 구현 및 테스트: 4주
- 시스템 통합 및 최적화: 2주
- 문서 작성 및 최종 검토: 1주

**7. 프로젝트 팀 구성 ### 삭제 예정**

- 프로젝트 매니저: 프로젝트 일정 및 리소스 관리 담당
- 시스템 아키텍트: 시스템 구조 및 설계 담당
- 개발자 및 운영팀: 각 기능의 구현 및 시스템 운영 담당

**8. 기대 효과**

- 분산 시스템 운영 및 모니터링에 대한 기술 역량 강화
- 실시간으로 데이터를 수집, 분석하고 시각화하는 능력 향상
- 협업과 문제 해결 능력 향상을 통한 팀의 역량 향상

**9. 참고 자료 ### 수정**

- Docker, ELK Stack, Grafana, Prometheus 등의 공식 문서 및 자료
- 관련 온라인 코스 및 튜토리얼을 통한 기술 습득


</aside>

## Worker 1 (nginx + filebeat)

### Access Log (접속 로그)
- IP 주소 및 사용자 에이전트
- 시간 및 날짜
- HTTP 메서드 및 요청 URL
- HTTP 응답 코드

### Error Log (에러 로그)
- 에러 메시지
- 시간 및 날짜
- 에러 레벨

### 기타
- 연결 시간과 응답 시간
- 서버 상태 코드
- 전송된 데이터 양
- 보안 로그

---

## Worker 2 (nginx + metricbeat)

### 현재 연결 수 (Active Connections)
- 현재 활성화된 연결 수

### 요청 수 (Requests)
- 현재까지의 총 요청 수

### 응답 상태 코드별 횟수
- 각 HTTP 응답 상태 코드에 따른 횟수

### 시스템 메트릭
- ex. 요청 수가 많아지면 CPU 사용량이 커진다 등등 알 수 있게

---

## Worker 3 (mariadb + wordpress)

### 기능
- Wordpress에서의 가입, 접속, 글쓰기 등등의 정보를 MariaDB에 저장함

