## 3일차 마무리 UI
![[Pasted image 20241117023459.png]]

## 이미지
- 이미지를 통해 대체적인 디자인 설계 가능
- 이미지 변경법
	1. Image의 Is Variable을 켜서 Graph에서 부를 수 있도록 설정
	2. Image 변경법 (기본은 Set, Read Only Image의 경우 Set Brush 사용)
	![[Pasted image 20241117023635.png]]
	![[Pasted image 20241117023710.png]]

## 애니메이션
- Widget Blueprint 왼쪽 하단 Animation  클릭 후 Animation 추가. 애니메이션 적용하고자 하는 UI 요소 클릭 후 Add를 통해 추가. 핀을 통해 애니메이션 적용
- Graph에서 Play Animation 노드를 통해 애니메이션 재생. (무한 루프 필요 시 Loop 횟수에 0 기입)

## 프로그레스 바, 텍스트 실시간 변환
![[Pasted image 20241117024233.png]]

## 버튼 클릭 전환(Play <-> Pause)
- 다음과 같은 Set Visibility를 통해 클릭 시 전환되도록 구현
![[Pasted image 20241117024411.png]]
- 다음은 전환 사용 모습 및 Play/Pause 버튼 동작 구현
![[Pasted image 20241117024437.png]]

