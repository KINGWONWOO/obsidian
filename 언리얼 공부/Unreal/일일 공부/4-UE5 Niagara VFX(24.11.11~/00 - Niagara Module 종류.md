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