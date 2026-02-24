## Emitter Spawn
## Properties
- GPU Sprite 변경법 : Sim Target을 CPUCompute로 변경 후, Calculate Bound Volume을 Fixed로 변경
## Emitter Update
- Emitter State : Emitter의 수명을 결정(System/Self)
- Beam Emitter Setup : Beam의 시작과 끝/ Tangent 설정
- Spawn Burst Instantaneous : 한 번에 모든 Particle을 생성
- Spawn Rate : Rate를 통해 Particle의 생성 속도를 설정
- Spawn Particles in Grid : 육면체 안에 Particle을 Spawn
## Particle Spawn
- Initialize Particle : Paricle의 수명, 색깔, 크기 등의 다양한 속성을 설정
- Add Velocity : Particle에 속도를 부여해 이동시킴
- Shape Location : Particle을 Spawn하는 모양을 설정. Particle은 해당 모양 내에서 랜덤하게 생성
- Spawn Beam : Spline을 따라 빔 형태의 이펙트를 만드는 역할. 정확도를 설정
- Beam Width : Curve로 빔의 모양을 설정
- Sprite Facing and Velocity : 스프라이트의 Facing과 Alignment를 설정. 이를 적용 시키기 위해선. Sprite Renderer에서 Custom으로 바꿔야함.
- Grid Location : Spawn Particles in Grid에 사용되는 Grid 관련 설정
- Sample Texture : Texture 가져오기
- Static Mesh Location : Static Mesh의 형상으로 Particles 생성
- Initialize Mesh Reproduction Sprite : 움직이는 Mesh의 Particle 추적
- Set parameter : parameter를 직접 설정
## Particle Update
- Particle State : Particle의 재생이 끝날 시 삭제 설정
- Sprite Rotation Rate : 스프라이트가 시간에 따라 회전하며 각도를 입력 받음
- Scale Sprite Size : Particle의 크기를 설정. Curve를 통해 다양한 크기 변화 가능
- Scale Color : Particle의 RGBA값을 설정. A값에 변화를 줘 Fade 효과 적용 가능
- Forces : Particle에 힘을 가함
	- Curl Noise Force : 무작위 성의 힘을 부여
	- Point Attraction Force : 한 쪽 점으로 끌어당김. 블랙홀
	- Drag : 이동 방향 반대로 끌어당기는 힘. 이동을 줄여줌
	- Aerodynamic Drag : Drag의 업그레이드 버전으로 더욱 상세한 조정이 가능
	- Vortex Force : 특정한 축을 기준으로 회전
	- Wind Force : 바람의 힘을 적용 가능
	- Update Mesh Orientation(Rotation Rate) : 랜덤한 회전을 부여
	- Gravity Force : 중력 효과를 적용
	- Acceleration Force : 가속도 효과를 적용
- Scale Velocity : 입자의 속도를 증가 또는 감소 시켜줌.
- Scale Mesh Size : Mesh용으로 Mesh의 크기를 조정
- Solve Forces and Velocity : 힘이나 속도 관련 모듈 추가 시 필요한 종속 모듈
- Dynamic Material Parameters : 다이나믹 파라미터 설정
- Color : Scale Color와 같이 색깔을 조정하는 모듈. 단, Scale Color와 Color중 하나만 적용됨.
- Collison : Niagara에 충격 효과를 생성
- Sub UV Animation : FlipBook Texture를 통한 UV Animation 적용 시 필요한 모듈
- Kill Particles in Volume : Particle이 사용자 정의 Volume안에 들어오면 삭제
- Update Mesh Reproduction Sprite : 움직이는 Mesh의 Particle 업데이트트
- Lerp Particle Attributes : Module간에 Lerp 동작을 가능하게 해줌. 작동하지 않을 시 모듈 간 순서 변경해보기(강의에서는 Update Mesh Reproduction과 Solve Forces and Velocity간의 Position, Velocity 보간)

## Event Handler(Stage에서 Handler 추가 시 생성)
- Event Handler Properties : 이벤트를 받는 속성을 설정
- Receive {} Event : 이벤트를 받음
## Render
- Sprite Renderer : 카메라를 향하는 Renderer
- Mesh Renderer : Mesh처럼 작동하는 Renderer
- Ribbon Renderer : 이동 발생 시 페이드되는 잔상을 남기는 효과(캐릭터 돌진, 총탄 궤적 등)
#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!
##### 7강 : 머터리얼 단축키 정리
- 단축키-표현식
	- A : Add
	- B : BumpOffset
	- C - Comment
	- D - Divide
	- E - Power
	- F - MaterialFunctionCall
	- I - If
	- L - LinearInterpolate
	- M - Multiply
	- N - Normalize
	- O - OneMinus
	- P - Panner
	- R - ReflectionVector
	- S - ScalarParameter
	- T - TextureSample
	- U - TexCoord
	- V - VectorParameter
	- 1 - Constant
	- 2 - Constant2Vector
	- 3 - Constant3Vector
	- 4 - Constant4Vector
	- Shift + C : ComponentMask
##### 9강 : 첫 번째 이미터 만들기
- Niagara Emitter : Particle을 생성하고 제어
- Niagara System : Emitter들을 저장하는 컨테이너
- Niagara Stage : System 생성 시 보이는 Module들의 집합. 이는 위에서 아래로 실행됨.
![[Pasted image 20241111172754.png]]
##### 10강 : 이미터 스테이지
- Stage in Niagara에서 각 Stage의 역할
![[Udemy ScreenShot 2024-11-11 17-36-49.jpeg]]
---
- Sprite : 카메라를 향하는 평면

##### 15강 : 첫 번째 VFX 머터리얼 만들기
- VFX 머터리얼 설정
	- Blend Mode : Additive/Translucent로 설정
		- Additive : Emissive Color가 0으로 가면 투명해짐
		- Translucent : Emissive Color가 0으로 가면 어두워짐. 즉, 어두운 색을 표현하고자 하면 이 모드 사용
	- Shading Model : Unlit
	- Two Sided 활성화
- Texture에 Particle Color를 곱하는 이유 : 나이아가라에서의 색 변화가 Texture에 영향을 끼치게 하기 위해

##### 16강 : 섹션 도전 과제 - 날아다니는 민들레 만들기
- View Port에서 변화를 보면서 값 조정을 하고 싶을 시 User Parameter로 만들어서 Detail에서 조정하기
![[Pasted image 20241111201928.png]]

##### 19강 : Sub UV Animation
- Sub UV Animation을 적용하는 과정
	1. Flip Book Texture : Flip Book Texture 준비
	2. Custom Material : 해당 Texture를 사용한 Material 생성
	3. SubUV Image Size : Niagara 생성 후 renderer에 할당. Texture의 프레임 수(가로x세로 배열 수)를 보고 Sub UV 크기를 설정
	![[Pasted image 20241111210601.png]]
	5. Animation Start/End Frame : Sub UV animation 모듈 추가 후 총 프레임 수(가로x세로)를 기준으로 프레임 시작과 끝을 설정하여 속도 조절
	![[Pasted image 20241111210611.png]]
#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!

##### 20강 : 화염 방사기 제작 시작하기 : 주 화염 만들기
- 특정 VFX를 봤을 때 이를 구현하기 위해서 필요한 질문 3가지
	1. 어떤 Renderer가 보이나요
	2. 어떤 Element가 보이나요
	3. 어떤 Forces/Material이 보이나요

#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!

##### 22강 : 섹션 도전 과제 : 푸른 화염 및 불티
- Niagara Emitter의 밝기 변화 구현법
	1. Color의 Alpha값을 시간에 따라 변하도록 Curve 설정
	2. Material에 Sin함수를 이용한 밝기 변화 구현
![[Pasted image 20241124124901.png]]

##### 23강 : 열 디스토션 생성하기
- Distortion Material 생성은 Translucent/Unlit으로 진행 다음은 구현 예시
![[Pasted image 20241124133957.png]]
- Niagara 값 편집 시 ViewPort에서 실시간 변화를 보면서 하고 싶으면, 변수 값을 UserParameter로 만든 후 Detail 창에서 변경.
- Material Input에서 Refraction이 보이지 않는다면 Detail 창에서 켜야함. 설정가능한 Refraction 설정은 다음과 같음.
	- Index Of Refraction : 굴절률을 기반으로 굴절 효과를 계산(기본)
	- Pixel Normal Offset : 픽셀 단위로 노멀 데이터를 오프셋하여 굴절 효과를 만듬(성능이 중요할 때 적합, 물리적 정확도가 낮음)
	- 2D Offset : 2D UV 좌표를 기반으로 굴절 효과를 계산, 게임 플레이 요소에 특화되었으며 화면 공간 왜곡이나 스타일화된 굴절 효과를 구현할 때 사용
	- None : 굴절 효과를 비활성화

##### 28강 : 커스텀 메시
- 커스텀 메시 : 나이아가라를 사용해 3D 모델링 소프트웨어에서 제작한 메시를 스폰 가능.
- 외부 툴에서 VFX 메시를 언리얼로 보낼 시 고려해야할 점
![[Udemy ScreenShot 2024-11-24 14-31-49.jpeg]]
##### 29강 : 언리얼에서 텍스쳐 굽기
- Texture에 필요한 것
	- Material : Texture의 패턴을 결정
	- Render Target : 컨테이너로 기능. 텍스처를 베이킹하거나 Runtime간에 특정 이벤트를 발생시키는데 사용.
	- Blueprint
![[Udemy ScreenShot 2024-11-24 14-54-09.jpeg]]
- Material 생성
	- 이때, RenderTarget에 넘어가는 정보는 Emissive Color/Opacity 뿐
- Render Target 생성
	- Material을 로드하기 전에 기본 설정 변경
	- X,Y 해상도 값 설정 / Render Target Format 변경(이번엔 RTF RGBA8 SRGB)

##### 30강 : 타깃 렌더링을 위한 머터리얼 드로잉
- Non-Static과 Static 함수의 차이 : Reference를 필요로 하는가
- Object Reference 사용 시 IsValid 노드를 통해 유효성 검사
![[Udemy ScreenShot 2024-11-24 16-02-23.jpeg]]
- 블루프린트 내 함수를 ViewPort의 Detail에서 실행할려면 Detail의 Call In Editor 활성화
- BakeTexture 함수 구현
- 'Draw Material To Render Target' 노드로 Render Target에 Material을 그림
- 'Render Target 2D Create Static Texture 2D Editor Only'로 Render Target으로 Texture 생성(Content Browser에서 Render Target 우클릭 후 Create Texture로도 가능.)
![[Pasted image 20241124161605.png]]
---
- Niagara의 Mesh Renderer에서 만든 Texture 사용법
	1. 만든 Texture를 새로운 Material Instance에 할당
	2. Niagara에서 Mesh 할당 후 Material 덧씌우기
	![[Pasted image 20241124162432.png]]
---
- Mesh Renderer의 Rotation 변화를 주고 싶으면 Mesh Renderer/Rotation 검색 후 값 변경

##### 32강 : 머터리얼 리프레셔 - UV 조작
- Texture Sample에 Noise Texture를 Add하면 왜곡
![[Pasted image 20241124180257.png]]
- Texture Sample에 Noise Texture를 Multiply하면 Dissolve
![[Pasted image 20241124180249.png]]
- 전체 사진
![[Pasted image 20241124180313.png]]

##### 34강 : 팬 디스토션 머터리얼 생성하기
- M_Ribbon_Additive 구현과정
	- Distort 부분
	![[Pasted image 20241124180354.png]]
	- Main Texture 부분
	![[Pasted image 20241124180407.png]]
	- Dissolve 부분
	![[Pasted image 20241124180423.png]]
	- Output 부분
	![[Pasted image 20241124180434.png]]

##### 35강 : 펄린 노이즈 생성하기
- Perlin Noise
![[Pasted image 20241124194206.png]]
- 펄린 노이즈 Material 생성(Opaque/Unlit)
![[Pasted image 20241124193539.png]]
![[Pasted image 20241124194224.png]]
- 여러 Content의 이름을 동시에 변경하는걸 도와주는 Script Action(강의 드롭다운에서 다운)
![[Pasted image 20241124193348.png]]
- 여러 Texture의 설정을 동시에 변경하고 싶을 시 Asset Action\Edit Selection Property Matrix 활용 
![[Pasted image 20241124193524.png]]

##### 37강 : 보로노이 노이즈의 베리에이션
- Caustics Noise
	![[Pasted image 20241124194649.png]]
	- Caustics Noise Material 생성(Opaque/Unlit)
	![[Pasted image 20241124194521.png]]
	![[Pasted image 20241124194633.png]]
---
- Clouds Noise
	![[Pasted image 20241124195329.png]]
	- Cloud Noise Material 생성(Opaque/Unlit)
	![[Pasted image 20241124195305.png]]
	![[Pasted image 20241124195349.png]]
---
- Marble Noise
![[Pasted image 20241124200053.png]]
	- MarbleNoise Material 생성(Opaque/Unlit) : 이전 Distort 작업과 유사. Noise로 Noise를 왜곡
![[Pasted image 20241124195929.png]]
	- 원본 Noise
	![[Pasted image 20241124200025.png]]
	- 왜곡 Noise
	![[Pasted image 20241124200040.png]]
#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!
##### 43강 : 포털 FX 시작 : 포털의 윤곽 만들기
- Vortex Velocity가 없을 시 대체 : Scale Velocity + Votex Force

##### 44강 : Depth Fade와 Sub UV 애니메이션
- 불투명한 객체와 투명한 객체 사이 상호작용 시 이음새를 없애는 법 -> Opacity에 Depth Fade 사용
![[Pasted image 20241125141427.png]]
#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!
##### 43강 : 메쉬 렌더러의 머터리얼 효과
- Texture 사용으로 인해 Material에 외곽 네모가 보일 시 해결법 : diamondGradient를 Mask로 사용
![[Pasted image 20241202133247.png]]

##### 51강 : 표면 충격 효과
- Texture의 Alpha 채널이 없는 경우도 존재. 이를 해결하기 위한 Master Material에 노드 추가
![[Pasted image 20241202170511.png]]
- Blueprint에서 Niagara 생성
![[Pasted image 20241202170614.png]]


#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!
##### 61강 : 레이저 코어 만들기
- 다른 Texture의 영향을 안받고 Niagara의 색 변화만 적용하고 싶을 시 추가 노드
- Sin함수를 이용해서 밝기 변화를 줄 때의 노드
![[Udemy ScreenShot 2024-12-04 19-35-39.jpeg]]
##### 62강 : 레이저 쉘
- Niagara에서 Scale Mesh Size 모듈이 작동하지 않을 시 Initialize Paricle에서 Mesh Scale Mode를  Unset에서 다른 것으로 바꾸면 됨.
#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!
##### 66강 : 위치 이벤트
- Sub UV Master Material에서 위 아래 Fade를 주는 노드
![[Pasted image 20241206145325.png]]
---
- 이벤트를 추가하는 과정
	1. 이벤트 생성 Emitter에서 Particle Update에 Generate {} Event를 추가.
	2. Properties에서 Requires Persistent IDs
	3. 이벤트를 받는 Emitter 생성 후 Stage 클릭 후 생성된 Event Handler Properties에서 source/Execution Mode/Spawn Number 설정
	4. Receive {} Event 모듈 생성

##### 67강 : 커스텀 로테이터
- Texture의 회전이 필요할 때는 Custom Rotator를 사용
![[Pasted image 20241206161227.png]]

##### 68강 : 다이내믹 파라미터
- 언리얼 요소 간 데이터 수정 가능
![[Udemy ScreenShot 2024-12-06 16-14-11.jpeg]]
- 다이나믹 파라미터 사용법
	1. Master Material에 Dynamic Parameter 설정
	![[Pasted image 20241206165817.png]]
	2. Niagara에 Dynamic Material Parameter Module 추가
	![[Pasted image 20241206165849.png]]
#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!

##### 75강 : 발사체 마스터 블루프린트
- Collison이 특정 객체와 부딪혔을 때만 이벤트가 발생하도록 설정
![[Pasted image 20241207161450.png]]

##### 76강 : 발사체 VFX 스포너
- Projectile Move Component에 이동을 줄려면 Set Velocity를 통해 속도 값 변경
![[Pasted image 20241207165611.png]]
- 이때, 값 적용에도 VFX가 이동하지 않을 시 Niagara system에서 Property/Local Space 활성화
---
- VFX가 제대로 스폰되지 않을 시, VFX 설정과 VFX 스폰 사이에 텀을 둬보기
![[Pasted image 20241207165713.png]]
---
- 블루프린트에서 User Parameter 설정하기
![[Pasted image 20241207172727.png]]

#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!

##### 86강 : 어트리뷰트 리더
- 다른 Emitter의 위치를 가져오는 NMS 노드.(Emitter Update)
![[Pasted image 20241208194659.png]]
##### 87강 : 리더 팔로우 고급
- Leader Emitter의 ID 가져오기
![[Pasted image 20241208211718.png]]
---
- Get Position by Index/ID 차이 : 
	- Index : Particle이 생성 되면 Index할당 없어지면 사라짐(고유하지 않음)
	- ID : Particle이 생성 되면 고유한 ID할당. 없어져도 유지
---
- NMS_UpdateFollowerVelocity 구현
![[Pasted image 20241208211806.png]]
	- 입력 값 : LeadingEmitter(Attribute), InLeaderID(NiagaraID), TargetPositionOffset(Vector), Positon(Particle), DeltaTIme
	- 함수 순서 : Get Position by ID, Direction and Length Safe

##### 88강 : 비 FX의 시작 : Fresnel
- Surface Normals
	![[Udemy ScreenShot 2024-12-08 21-47-34.jpeg]]
	- Face Normal : 면이 향하는 방향과 방향 정보를 알 수 있음
	- Vertex Normal : 각 정점의 방향 정보를 알 수 있음
	- Pixel Normal : 화면에 렌더링되는 픽셀의 노멀. 픽셀에는 방향 정보가 없음 노멀 맵이 있어야 작동. 
---
- Fresnel Calculation
![[Udemy ScreenShot 2024-12-08 21-51-16.jpeg]]
![[Pasted image 20241208215158.png]]

---
- Fresnel Example Material
![[Udemy ScreenShot 2024-12-08 21-59-34.jpeg]]
	- Fresnel Exponent를 올리면 중앙 회색 부분의 범위가 늘어나고
	- Fresnel Strength를 올리면 전체 밝기가 올라감
##### 89강 : 리퀴드 마스터 다이나믹 파라미터
- Rain Drop VFX 구현을 위해 필요한 Texture들
![[Udemy ScreenShot 2024-12-08 22-03-12.jpeg]]
- M_LiquidMaster_DynParam 구현
	- 입력 부분
	![[Pasted image 20241208223058.png]]
	- 구현 부분
	![[Pasted image 20241208223114.png]]

#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!

##### 91강 : 콜리즌 이벤트 생성
- Collision 발생 시 Particle 삭제하는법
![[Pasted image 20241209163802.png]]

##### 93강 : 물결
- Collision 후 Particle 생성 위치가 부정확하게 느껴질 시, Collision의 Radius 줄이기

##### 94강 : 콜리즌 노멀 확인
- Collision 발생 시 Normal을 확인하여 평면이면(>0.99) 유지. 아니면 삭제하는 Module Script
![[Pasted image 20241209172741.png]]
---
- Receive Event에서 설정값 변경(Apply -> Output)으로 특정 정보를 Parameter에 넘겨 사용 가능.
![[Pasted image 20241209172951.png]]
![[Pasted image 20241209173101.png]]
##### 95강 : 비 FX 마무리 : 커스텀 나이아가라 열거형
- Niagara에서 드롭다운 Enum 사용하기
	1. 사용할 Enumeration 생성(Niagara용은 앞에 ENiagaraCustom 붙이기)
	![[Pasted image 20241209194037.png]]
	2. Project Setting에 추가 후 재시작
	![[Pasted image 20241209194120.png]]
	3. NMS에 Static Switch 추가 후 Type을 Enum으로 설정, Niagara Parameter Map 추가
	![[Pasted image 20241209194412.png]]
	4. Mep set과 Output 사이에 연결 후 각 Mode 별 기능 구현
	![[Pasted image 20241209194606.png]]
	
#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!

##### 104강 : 나이아가라를 사용한 텍스쳐 샘플링
- Texture Sample 사용 예시
	1. Niagara에 Texture Sample 모듈 추가
	2. Spawn Particles in Grid 모듈 추가 및 모듈 크기 설정
	3. Grid Location에서 그리드 단위를 (1,1,1)로 설정
	4. Sample Texture에서 UV를 Grid의 noramlized Array Location으로 적용
	![[Pasted image 20241210211725.png]]
	5. Initialize Particles에서 Color Mode/Position Offset/Sprite size 설정
	![[Pasted image 20241210211804.png]]
---
- Kill Particle(Particle Spawn)에서 Alpha 채널로 생성되는 Particle 지우기(투명)
![[Pasted image 20241210211840.png]]

##### 105강 : 스태틱 메쉬 디졸브 시작 : 스태틱 메쉬 위치
- Static Mesh를 Niagara에 불러오기
	 1. Spawn Rate로 변경
	 2. Static Mesh Location 생성 및 SM 설정
	 3. Sprite Material을 해당 Mesh의 Material로 설정
	 4. Set Particles UV 사용자 모듈을 생성(해당 Material의 UV들을 Dynamic Parameter로 설정)
	 ![[Pasted image 20241210230107.png]]
	 5. 생성한 Set Particles UV에 SampledUV 할당
	 ![[Pasted image 20241210230207.png]]

##### 106강 : 디졸브 효과에 필요한 파티클 색상
- Particle 동그랗게 만들기, Fade 효과 만들기, Particle Color 연결
![[Pasted image 20241210232636.png]]
- 이때 Material의 Blend Mode를 Masked로 변경한 후, Opacity Mask에 연결하거나/ Translucent에 연결 후 Opacity에 연결하는 두 가지 방법 존재. 전자가 더 저렴함
- DitherTemporalAA는 다음과 같은 Mask를 추가해주는 노드
![[Udemy ScreenShot 2024-12-10 23-28-10.jpeg]]
---
- Static Mesh 사용하는 Niagara System에 Normal 정보 추가하기
	1. Sprite Renderer에서 Custom Facing Mode로 설정
	2. Sprite Facing And Alignmnet 모듈 추가 후 Sprite Facing을 Sampled Normal로 변경
	![[Pasted image 20241210232927.png]]

##### 107강 : 메쉬 재생성 스프라이트
- 움직이는 Mesh를 위한 모듈 2가지
	- Inintialize Mesh Reproduction Sprite : 움직이는 Mesh에 맞춰 Particles의 위치 추적
	- Update Mesh Reproduction Sprite : 움직이는 Mesh에 맞춰 Particles의 위치 업데이트
- Master_Material에 Niagara_MeshReproductionSpriteUVs 추가
![[Pasted image 20241210235816.png]]
	- UV는 모든 Texture UV에 연결
	- Normal은 모든 Normal 연결에 Multiply


#### Unreal Engine 5 : 강의 하나로 Niagara VFX 완벽 마스터하기!
##### 108강 : 선형보간 파티클 어트리뷰트
- Niagara에서 Material에 색변화를 주기 위해서는 보통 Particle Color 노드를 Muliply로 곱한 뒤 Emissive Color에 연결한다. 그러나, 가끔 Material의 기존 색을 덧씌워 버리는 경우가 존재하는데 이때는 Lerp를 통해 해결
![[Pasted image 20241211143730.png]]
- 해당 Alpha 값에 Curve를 줘서 자연스러운 색 전환 가능
![[Pasted image 20241211145229.png]]

##### 109강 : 디스턴스 필드
- Distance Field : 가장 가까운 Surface의 거리 정보를 저장
	- Mesh DF와 Globla DF 존재. Mesh가 더 높은 해상도/비싼 리소스
- Distance Field 구현 Material 노드
![[Pasted image 20241211151812.png]]
- Distance Field Example
![[Pasted image 20241211151829.png]]
- 이때, DF Material을 적용한 Mesh는 Detail에서 'Affect Distance Field Lighting' 비활성화

##### 110강 : 디졸브 효과에  디스턴스 필드 사용하기
- Scratch를 사용해서 Distance Field 사용하기
![[Pasted image 20241211155818.png]]
- 해당 Output 값으로 Dynamic Parameter와 Lerp의 Alpha값 변경

##### 111강 : BP로 머터리얼 디졸브 트리거하기
- Blueprint로 Material Intance의 값 변경하기(Dynamic Material Instance)
- [참고 URL](https://blueprintue.com/blueprint/tmedbitw/)
![[Pasted image 20241211171043.png]]
![[Pasted image 20241211171055.png]]
![[Pasted image 20241211171122.png]]

##### 112강 : 디졸브 효과를 위한  파티클 FX
- Particle FX를 Trigger하기
	1. Niagara로 이동 후 설정 변경(Once로 설정)
	2. Blueprint에서 Spawn System Attatched로 붙여서 소환
	![[Pasted image 20241211175952.png]]

##### 113강 : 노이즈 디졸브 머터리얼
- [구현 Material](https://blueprintue.com/blueprint/m9akh3l0/)
