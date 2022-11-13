# Introduction to Operating System



### 운영체제의 범위

- 협의의 운영체제 (커널) : 운영체제의 핵심부분으로 메모리에 상주하는 부분
- 광의의 운영체제 : 커널 + 각종 주변 시스템 유틸리티



### 운영체제 분류

- 동시 작업 가능 여부
  - 단일작업 (Single Tasking) : MS-DOS
  - 다중작업 (Multi Tasking) : UNIX, MS Windows
- 사용자의 수
  - 단일 : MS-DOS, MS Windows
  - 다중 : UNIX, NT Server
- 처리방식
  - 일괄처리 (batch processing) : 일정량 모아서 일괄 처리, 초기 Punch Card 처리 시스템
  - 시분할 (time sharing) : UNIX, interactive, 짧은 응답시간
  - 실시간 (realtime OS) : **정해진 시간** 안에 어떤 일이 반드시 종료됨이 보장 ex) 원자로/공장 제어
    - 경성 실시간 시스템
    - 연성 실시간 시스템



### 용어정리

멀티태스킹 / 멀티 프로그래밍 (메모리 강조) / 타임셰어링 (CPU 강조) / 멀티 프로세스

**멀티 프로세서** : 다중 CPU



### OS 종류

- UNIX
  - 대형 컴퓨터용
  - C언어 개발
  - 소스코드 공개 (학술 및 개발에 용이)
  - 높은 이식성
  - 최소한의 커널 구조 (높은 확장성)
  - System V, FreeBSD, SunOS, Solaris
  - Linux (서버, PC 모두)
- DOS
  - PC용 (싱글 태스킹 + 단일 사용자)
- MS Windows



### 운영체제의 구조

CPU <=> Memory <=> DISK 혹은 I/O Device