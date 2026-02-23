## UI 전환
1. UI를 표시할 Blueprint Actor에 Widget 변경을 위한 Switch To Widget 구현
![[Pasted image 20241116002425.png]]
2. Widget Blueprint로 가서 해당 BlueprintActor와 이동할 UI WIdget Blueprint의 Reference를 위한 변수 생성
![[Pasted image 20241116002622.png]]
3. Event Pre Construct 노드에 Get Actor Of Class를 통해 변수 초기화
![[Pasted image 20241116002651.png]]
4. Create Widget과 미리 만들어 놓은 SwitchTo Widget을 통해 UI간 전환을 구현
![[Pasted image 20241116002729.png]]

## UI 크기 문제(Play시 UI가 커지는 문제)
- 기존 VR Template Menu에서 해당 노드 삭제
![[Pasted image 20241116002922.png]]

## Level간 Actor 교환법(A -> B)
1. A에서 Window/Level Menu를 킨 후 Levels/Add Existing을 통해 B를 추가
2. A에서 이동하고자 하는 Actor 선택 후 B를 우클릭/Move Selected Actor To Level로 이동