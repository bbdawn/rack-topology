# Rack Topology

데이터센터 물리/가상 인프라 구조를 시각화하는 Rack Topology 기능 설계 및 개발 프로젝트입니다.

## 주요 기능

### 랙 구성도
데이터센터 랙에 탑재된 자원을 등록하고 구성을 시각화합니다.
- Server, Storage, Switch 등 물리 자원 등록 및 관리
- 랙 단위 자원 배치 구성도

### 물리 네트워크 토폴로지
물리 호스트와 스위치 간의 연결 구조를 포트 단위로 시각화합니다.
- 서버 ↔ 스위치 포트 연결 매핑
- IPMI / SNMP 수집 데이터를 가공하여 토폴로지 구성(데이터 엔지니어와 협업) 

### 가상 네트워크 구성도
OpenStack 네트워크(VLAN) 기준으로 가상 인프라 연결 구조를 시각화합니다.
- VLAN별 연결된 Instance 매핑

### 멀티 공급자(Multi-Provider) 자원 공유
Provider > Datacenter > Rack > Resource 계층 구조에서 공급자 간 자원 중복 등록 문제를 해결합니다.
- Switch를 한 번만 등록하면 다른 공급자에서 불러오기로 재사용 가능
- Switch 중복 등록 시 발생하는 SNMP 과부하 방지
- 공급자 활성화 / 비활성화 / 삭제 관리
- 공급자 비활성화 → 활성화 시 하위 Datacenter ~ Resource 전체 상태 일괄 복구
- 비활성화 상태의 공급자는 SNMP/IPMI 데이터 수집에서 제외되도록 DB 설계

## 기술 스택
- Backend: Java, Spring Boot, JPA
- Database: MySQL
- 인프라: OpenStack
- 프로토콜: IPMI, SNMP (데이터 수집 파이프라인 연동)
