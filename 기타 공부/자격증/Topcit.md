### 1영역 소프트웨어
![[Pasted image 20241004210641.png]]
- 응집도는 높을 수록 좋음 (기능 -> 우연)
- 결합도는 낮을 수록 좋음(자료 -> 내용)
- ![[Pasted image 20241004210923.png]]
- 파이썬은 recursion 횟수를 1000회로 제한 이에 재귀호출이 반복되면 stack overflow 발생
![[Pasted image 20241004211244.png]]
![[Pasted image 20241004211302.png]]

### 2영역 데이터
- View는 기본 테이블로부터 유도한 논리적 가상 테이블
- 다이어그램에서 '#'은 protected, +는 public
- 외부 스키마 : 사용자 관점
- 개념 스키마 : 통합(다합침)
- 내부 스키마 : 저장 관점
- 맵리듀스
![[Pasted image 20241004205830.png]]
![[Pasted image 20241004205924.png]]
![[Pasted image 20241004205931.png]]
-정규화 과정(원부이결다조)

1) 1NF : 모든 도메인이 원자 값

2) 2NF : 부분적 함수 종속을 제거

3) 3NF : 이행적 함수 종속 관계(A->B, B->C일 때 A->를 만족)
### 3영역 시스템아키텍쳐
- 
![[Pasted image 20241004201337.png]]
![[Pasted image 20241004201437.png]]
- 병렬 컴퓨팅 아키텍쳐(프로세서) 모델 분류
![[Pasted image 20241004201526.png]]
![[Pasted image 20241004201543.png]]
![[Pasted image 20241004201809.png]]
- 하둡 : 대량의 자료를 처리할 수 있는 큰 컴퓨터 클러스터에서 동작하는 분산 소프트웨어 플랫폼
![[Pasted image 20241004204951.png]]
![[Pasted image 20241004204957.png]]
- RPO(Recovery Point Objectives) : 재해 발생 시 감내할 수 있는 데이터 손실의 대한 지표, 롤백
- RTO(Recovery Time Objectives) : 재해,장애 발생 시 원상태로 복원되는데 시간
- ![[Pasted image 20241004205236.png]]
- 
### 4영역 정보보안
- PKI : 공인인증서 같은거
![[Pasted image 20241004200330.png]]
- 네크워크 공격 유형
	- APT : 침추, 검색, 수집 및 유출 단계
	- 파밍 : 가짜 사이트 유도하여 정보 탈취
	- DBD : 악의적 웹 사이트 접속 시 악성코드 감염
	- Fileless : OS에 기본탑재
![[Pasted image 20241004200557.png]]
- 망분리 : 공공기관이나 기업에서 인터넷과 완전히 격리된 환경을 위해 네트워크를 분리하는 기술(논리적-물리적)
- name.replaceAll("\","")
### 5영역 비즈니스

- CPDN(Contents, Platform, Network, Device)
- IaaS(다해야함), Paas(기술만), Saas(다해줌)
- IT 비즈니스 순환적 관리 : PDCA(Plan-Do-Check-Action)
- ISP : 정보 시스템 비전과 전략을 수집하는 과정(중장기)
- MECE : 어떤 사항을 중복X, 누락X 전체 파악하는 사고방식
- BCG 매트릭스 : 사업의 포트폴리오 수립 도구 (가로 : 점유율, 세로 : 성장율)
- 7S 분석 : 내부적
- SWOT : 강점, 약점, 기회, 위협
- 롱테일 현상
![[Pasted image 20241004195832.png]]
- 네트워크 효과 : 특정 상품에 대한 어떤 사람의 수요가 다른 사람들의 수요에 영향을 받음
- SPI = EV / PV (1보다 작으면 일정지연)
- CPI = EV / AC (1보다 작으면 원가 초과)
- ROI = 영업이익 / 투자비용 * 100
- PP = 투자비용 / 연간이익
- S/W 품질평가관련 국제 표준 = ISO 25000
- 3점 추정(PERT) : 일정 추정방식으로 평균치 = (낙관치 + 4x최빈치 + 비관치) / 6

# DDL
## CREATE

![[Pasted image 20241018171557.png]]
![[Pasted image 20241018171550.png]]
![[Pasted image 20241018171540.png]]
![[Pasted image 20241018171610.png]]
![[Pasted image 20241018171617.png]]
## ALTER
![[Pasted image 20241018171630.png]]
## DROP
![[Pasted image 20241018171659.png]]

# DCL
---
![[Pasted image 20241018171756.png]]

## DML
---
![[Pasted image 20241018171904.png]]
![[Pasted image 20241018171910.png]]
![[Pasted image 20241018171923.png]]
![[Pasted image 20241018171930.png]]
![[Pasted image 20241018171959.png]]
![[Pasted image 20241018172024.png]]
![[Pasted image 20241018172045.png]]
![[Pasted image 20241018172100.png]]
![[Pasted image 20241018172106.png]]![[Pasted image 20241018172127.png]]
![[Pasted image 20241018172135.png]]
![[Pasted image 20241018172215.png]]
