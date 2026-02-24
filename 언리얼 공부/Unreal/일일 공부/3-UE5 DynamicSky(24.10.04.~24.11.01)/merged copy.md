#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!
##### 8강 : 환경 조명 믹서
- 시작 조명 설정은 Window-Light Mixer로 손쉽게 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241004151007.png">
- Post Volume 추가 후 Infinite Extent 설정, Dynamic Sky 연출 시 Min/Max EV100에 동일한 값을 줘서 노출이 일정하게 유지해야 편함
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241004151103.png">
 - SkyLight RealTimeCapture 활성화

##### 9강 : BP_DynamicSky 액터
- Blueprint를 통해 간단한 드래그 앤 드롭 DynamicSky 시스템 생성 가능
	1. BP_DynamicSky 생성(Actor)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241004151910.png">
	2. 컴포넌트 추가(cloud는 이후 생성)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241004152005.png">
	3. 이때 각 컴포넌트 세부설정 완료
		+ DirectionalLight : Forward Shading Priority 변경(이를 통해 오류 제거)
		 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241004152113.png">
		 - SkyLight : Real TIme Capture 활성화
		 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241004152205.png">
		 - PostVolume : Max/Min Ev100 설정
- 태양 각도 변경 필요 시 DirectionalLight의 yaw값 변경(pitch-yaw-roll)

##### 10강 : Construction Script
- Constrcution Script의 3가지 특성
	1. BP Object가 생성되거나 업데이트 될 때 실행
	2. runtime 이전에 실행(runtime 도중에는 실행 X)
	3. non instance editable 변수는 변경할 수 없음
 - 변수 instance editable 활성화 방법 : 맨 오른쪽 눈 표시 활성화
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241004153827.png">
 - 화면에 String이 보이지 않을 시 Show Stat 확인
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241004153851.png">
##### 11강 : 시간대
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 11강 : 시간대
- 태양 각도(Pitch)는 0도:일출, -90도:정오, -180도:일몰
- 시간대 설정을 위해 변수 및 함수 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005213854.png">
- 이때 변수의 Detail 패널에서 Category를 통해 분류, Range 설정을 통해 가능한 값 범위 조정 가능(사진은 TimeOfDay의 설정)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005213928.png">
- HandleSunMoonRotation 함수 작성(Map Range Unclamped 함수 사용 주목)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005214644.png">
- 이를 통해 Construction Script 작성(Sequence 0은 다음 강의에)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005214700.png">

##### 12강 : 달 회전 처리
- Directional Light를 하나 더 생성하여 달로 사용(Intensity는 낮춰야함)
- 달의 경우 After Dusk/Before Dawn으로 2번 나뉘어 블루프린트 계산실행
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005220146.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005220158.png">
- 그러나 Directional Light가 2개 이상 존재하여, 하늘의 대기층이 이를 인식하지 못함.
- --> 다음 강의에서 하나씩 숨기는 과정 진행

##### 13강 : BluePrint 매크로

|특성|함수|매크로|이벤트|
|------|---|---|---|
|Return Value|Yes|Yes|No|
|class 밖에서 호출|Yes|No|Yes|
|Timeline/Delay|No|No|Yes|
- 또한, Macro는 내부에 여러 실행 핀(Out)을 가질 수 있음.
- 낮과 밤을 확인하는 Macro 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005222007.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005222037.png">
- 이를 통해 Sun/Moon Directional Light의 Visibililty를 설정하는 HandleVisibility 함수 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005222215.png">

<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241005222301.png">

##### 15강 : 밤하늘
- 밤하늘 만들기 옵션 변경
	- Directional Light
		- Intensity 낮추기(1~2정도)
		- Temperature 높이기(차갑게)
		- Source Angle 낮추기(0)
		- Light Color 어둡게
	- SkyAtmosphere0 
		- MultiScattering 값 낮추기 (0.5정도)
		- Rayleigh Scattering 색 바꾸기(어두운 파란색 정도)
		- Ground Albedo(지평선 색) 색 바꾸기(대기색이랑 비슷하게)
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 16강 : 블루프린트 속성 조절
- 15강에서 변경한 Detail 속성값들을 블루프린트로 구현
- HandleNightSettings 함수 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006200628.png">

<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006200513.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006200521.png">
- SkyAtmosphere의 경우 낮,밤 둘 다 공유하므로 Branch를 통해 각 시간마다 초기화 필요
- 이후 생성한 함수를 Construction Script Sequence Node에 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006200615.png">

##### 17강 : 하늘 구체
- 하늘 돔(별하늘 등)을 구현할려면 Engine 폴더에서 Sky Sphere(Static Mesh)가 필요
- 검색해서 안나올 시 Content Browser 우측 위 Setting에서 Show Engine/Plugin Content가 활성화 되있는지 확인
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006201150.png">
- 해당 BP 우클릭 후 Show In Folder View를 해서 들어간 뒤 SM_SkySphere 찾기->해당 SM 사용자 폴더로 복사 이동
- 해당 SM_SkySphere 들어가서 Element0 초기화 후 BP_DynamicSky에 StaticMesh 추가해서 할당(이때 크기는 맵을 덮을 만큼 키우기 대략 100,000)
- 이후 SM에 할당할 Material 생성
	1. Shading Model -> Unlit으로 변경
	2. Is Sky 활성화
	3. Emissive Color 노드 연결
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006202529.png">
	4. Material Instance 생성

##### 19강 : 밤하늘의 별
- Material Node들을 이용해서 Star Texture 구현
- UV의 사용과 TimeWithSpeedVariable 사용에 주목
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006205834.png"><img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006205509.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006205515.png">

##### 20강 : 버텍스 노멀(Vertex Normal)
- Node 색깔로 특성 구분 가능
	- 빨간색 : 외부 데이터
	- 초록색 : HSLS 내부 정의 함수
	- 하늘색 : 외부 함수
- 지평선 주변에도 별이 생기는 문제 발생 - >  Vertex Normal 이용해서 마스크 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006211522.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241006211804.png">
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 21강 : 채널 마스크 매개변수
- Star의 Tiling을 깨기 위해 강의자가 제공한 Noise Texture 활용
- 이때 Channel을 선택할 수 있는 Parameter를 추가해주는 ChannelMaskParameter 노드 주목
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007212201.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007212305.png">

##### 22강 : 별 가시성
- 별이 낮에도 떠있는 문제 해결 시도 -> TimeOfDay는 Blueprint고 Star Material은 밖에 있는데 어떻게 Communication하지? -> Dynamic Material Instance 사용!
- 이 연결은 단방향 : 블루프린트가 머터리얼을 읽고 쓸 수는 있으나 반대는 불가능
- 구상해보기 : Bool Logic을 써서 Star를 끄고 키면 되겠지? -> 그러나 기존의 Material 내에서 사용하던 Static Bool Param/Switch Bool Param은 Dynamic Material Instance 활용 불가 -> If 노드 사용해서 Scalar Parameter 생성!
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007213332.png">
- 블루프린트에 InitSkySphereMaterial 함수 생성 : DynamicMaterialInstance 생성 후 변수에 저장
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007214441.png">
- Construction Script를 통해 생성이 제대로 되었는지 점검
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007214516.png">
- HandleNightSetting에서 이 DMI를 통해 Set Scalar Parameter Value 노드 사용. 이를 통해 IsStarVisible 값 변경(낮, 밤 둘 다 설정)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007214613.png">

##### 23강 : 달
- Material Graph에서 Ctrl + Space 누르면 Content Browser 열기 가능
- M_DynamicSkySphere에 Moon 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007215821.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007215829.png">
- 새로 알게된 점
	- Texture Sample 우클릭 후 Texture Object로 변경 가능
	- SkyAtmosphereImage로 쉽게 달 이미지 추가 가능
	- SkyAtmosphereLightDirection으로 쉽게 빛의 방향 설정 가능
	- MakeFloat2 함수로 간단하게 float1->float2 치환 가능

##### 24강 : 섹션 챌린지 - 달 가시성
- 별과 같이 낮에는 달이 안보이도록 설정(Dynamic Material Instance 활용)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007220544.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241007220555.png">

#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 26강 : BP에서 더 많은 속성 조절하기
- Material Instance의 속성 변경을 BluePrint로 이동시키기(이를 통해 Detail에서 조정 가능)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241008131137.png">

- Yaw 회전도 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241008131213.png">

##### 30강 : 블루프린트 Enum
- 다양한 구름 모드를 조절하기 위해 Enum(열거형) 사용
- 생성 과정
	1. Contents Browser에서 우클릭 후 Blueprint->enum 클릭 생성
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241008131958.png">
	2. 생성한 Enum 클릭 후 Enumerator 추가
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241008132037.png">
	3. BP_DynamicSky에 변수 추가(Type은 생성한 Enum 이름)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241008132153.png">
	4. 생성한 변수를 통해서 Enum간 전환 구현
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241008132255.png">
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241008132312.png">
	
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 31강 : 2D 구름
- M_DynamicSky에 2DClouds 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241009132837.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241009132844.png">
- 하지만 아직 문제 발생
	- 지평선에 구름이 존재
	- 돔 모양 꼭대기에 이음새가 발생
	- 구름과 하늘간의 블랜드가 어색함(특히 밤에는 너무 밝음)

##### 32강 : 2D 구름 조정
- 지평선 구름 존재 -> 별에 사용했던 Sky Mask를 named reroute로 만든 후 공용 사용
- 이때, 공용으로 바꼈으므로 변수의 Category도 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241009133252.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241009133340.png">
- 돔 모양 꼭대기에 이음새가 발생 -> 꼭대기 부분의 구름을 지우자 -> 그러기 위해선 마스크가 필요해 -> 어떤 마스크? 상단이 0, 아래가 1 -> 아 UV의 V축을 쓰면 되겠구나
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241009134209.png">

##### 33강 : 하늘 분위기 틴트
- 구름과 하늘간의 블랜드가 어색함 -> 하늘 빛과 구름을 Lerp를 통해 Blend
- 변수간 거리가 너무 멀 때는 Named Reroute 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241009135058.png">
- 밤과 낮에 필요한 Alpha값이 다름 -> 블루프린트로 해결

##### 34강 : 블루프린트에서 2D 구름 조정
- 새로운 Macro와 Variable로 블루프린트에 2DClouds 관련 변수들 노출
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241009140958.png">
- 이는 2D Clouds일때만 노출되어야 함.
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241009141054.png">

##### 35강 : 평면 투영
- 기존(UV 투영)과 비교한 평면 투영의 장단점
	1. World Position을 기준으로 하기 때문에 Mesh를 이동, 회전, Scale을 적용해도 영향을 받지 않음
	2. 단, X-Y-Z 한 축으로만 투영이 가능
	
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 36강 : Volumetric 구름
- Volumetric 구름 설정을 위해 열거형 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010203928.png">
- Volumetric Cloud 디자인을 위한 Material 생성 -> 설정 변경(Material Domain, Blend Mode, Used with VolumetricCloud)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010204015.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010204036.png">
- Volumetric Metric의 구현 과정
	- 2D Texture Mask(오늘 Topic)
	- 3D Volume Texture
	- Volumectric Advanced Output
- Material 구현에서 제일 중요한 출력핀은 Extinction, 다음과 같이 구현(2D Texture로 구현하는 과정)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010205725.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010205744.png">

##### 37강 : 볼륨 질감
- 구름에 3DNoise를 통해 질감 추가하기
- 이때, Texture Sample을 바로 Parameter로 만드는 것이 아닌 / Texture Object로 만든 후 Parameter화 이후 연결(그래야 이후 Texture 변경 가능)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010212506.png">
- Add로 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010212556.png">

##### 38강 : Volumetric 고급 출력
- Volumetric Advanced Output으로 구름에 대한 추가적인 속성 제어 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010221749.png">
- PhaseG/PhaseG2 : 빛이 앞으로 또는 뒤로 얼마나 많이 산란되는지 제어[-1,1]
- PhaseBlend : 이 두 함수를 Blend(Lerp와 유사)[0,1]
- MultiScatteringContribution : 구름을 통과하는 빛의 양 조절[0,1]
- MultiScatteringOcclusion : 자체 그림자 강도[0,1]
- MultiScatteringEccentricity : 다중 산란양 미세 조절[0,1]
- 이때, VAO의 Detail에서 MultiScattering 부분 변경 필요
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010221815.png">

##### 39강 : 영향력 반경 리팩토링
- InfluecedRadiusDecreaseAmount 속성의 경우 직관적이지 못함. 변경 필요
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010222111.png">

##### 40강 : 레이어 내 표준 고도
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010225904.png">
- Cloud Sample Attributes 노드의 NormAltitudeInLayer 핀을 이용해서 구름의 하위 부분과 상위부분에 다른 변형 적용
- 따로 구현 후 Lerp를 통해 블랜드
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241010230014.png">
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 41강 :  구름용 매크로 변형
- 랜덤성을 늘리기 위해 Macro Variation 추가
	1. Starter Content를 불러와서 Metal 종류의 Material에서 MacroVariation 찾기
	2. 찾은 노드들 복사한 후 Material Function 생성
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011102316.png">
	3. M_VolumetricCloudsMaster에 해당 MF 추가(Switch 전환은 덤)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011102531.png">
- 최적화를 위해 ConservativeDensity 노드 사용 : 구름이 없는 위치는 리맵하지 않음
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011103253.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011103337.png">

##### 42강 : Volumetric 구름 패닝
- 움직이는 구름 구현을 위해 UV를 통한 Panning 구현
- 2D Noise, 3D Noise에 모두 적용시켜야 하므로 2D에만 사용 가능한 Panner는 사용하지 않음.
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011104416.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011104422.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011104429.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011104437.png">

##### 43강 : 블루프린트에서 Volumetric 구름 조정하기
- ToggleVolumetricCloud 매크로 구현해서 Enum에 따라 Cloud 변경 기능 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011111046.png">
- Set VolumetricCloudSettings로 Volumetric Cloud의 설정을 Detail 패널에서 바꿀 수 있게 설정(이때, 원래 있는 설정은 VolumeticCloud, 사용자 정의 설정은 Dyn_MI 사용)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011111148.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011111159.png">

##### 44강 : 다중 샘플러 유형 지원
- 3D Noise Texture의 Sampler Type은 Linear Color / Masks 2개로 나뉨
- 이때 현재 만든 Master Material에 Mask 3D Noise Texture로 교체하면 에러 발생
- 해결 법 : Mask용 Texture Object도 만든 후 Switch Parameter를 통해 교체 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241011112105.png">
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 41강 :  구름용 매크로 변형
- Booleand으로 live preview 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241012201524.png">

#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!
##### 51강 : 노이즈 스컬프팅
- 랜드스케이프 모드에서 Sculpt로 지형 생성 가능 이때, Texture를 Noise Texture로 바꿔서 더욱 다양한 지형 생성가능

##### 53강 : 텍스쳐 폭격 Voronoi
- Texture Bombing 진행과정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241013203300.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241013203305.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241013203312.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241013203317.png">

##### 54강 : 삼면 투영 기본값
- 삼면 투영(Triplanar)는 언리얼 내장 함수로도 가능 WorldAlignedTexture 노드
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241013203830.png">

##### 55강 : 삼면 투영 재구축
- 3면 투영 : X축 투영, Y축 투용, Z축 투영 3개 합치기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241013205937.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241013205943.png">
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 56강 : UV 삼면 투영
- 이전의 방법은 Texture Sample이 3개나 필요해 material이 무거워짐 -> Texture Sample을 혼합하는게 아닌 UV를 혼합하자!
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241014134416.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241014134424.png">
- 다만 UV 혼합 시 축끼리 만나는 지점에서 아티팩트 발생 -> CheapContrast를 이용해서 부드럽게 만들기(다만, 작은 Object에는 여전히 부적합하므로 Landscape같은 큰 곳에 이용)

##### 57강 : 삼면 폭격
- Texture Bombing과 Triplanar 합치기
- Triplanar의 최종 출력값을 Texture Bombing의 CachedProjectionUV로 교체하면 손쉽게 완료
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241014135032.png">

#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 61강 : MF_ConputeLandscapeUV
- 56강에서 만든 UV 삼면 투영 방법을 따로 MF으로 만듬
- MF_ComputeLandscapeUV 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241015232918.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241015232923.png">

##### 62강 : 랜드스케이프 레이어 조합
- 지금까지 제작한 MF를 통해 최종 랜드스케이프 레이어 조합한 MF 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241015233840.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241015233847.png">

##### 63강 : 그라운드 레이어 기본 색상
- MF_LandscapeLayerProcess에 색감 조정 및 Set Material instance 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241015234517.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241015234524.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241015234529.png">

##### 64강 : 기본 색상 매개변수
- MF_LandscapeLayerProcess에 남은 입력 핀들 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241015235323.png">

##### 65강 : 그라운드 레이어 노멀 및 ORD
- Normal 및 ORM 추가, Macro variation 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241016002226.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241016002230.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241016002234.png">
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 66강 : 경사 레이어
- Texture sampler의 sample source를 wrap으로 변경 -> 다른 레이어를 추가하기 위한 기본 설정
- 기존의 Ground Layer 부분 복사후 Slope Layer 추가 Blend 노드를 통해 둘이 합치기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241016102840.png">

##### 67강 : 경사 블렌드
- 경사 마스크 제작 후 적용하여 자동으로 경사 레이어에 다른 Material이 적용되도록 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241016104541.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241016104547.png">

##### 69강 : 야간 설정 조정
- 야간에는 구름의 Brightness가 낮아지게 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241016140102.png">
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 72강 : 눈 오는 날씨를 위한 조명
- 눈 오는 날씨를 위해 조명 조정
	- DirectionLight
		- Intensity : 8.f
		- LightColor 어둡게
		- SourceAngle : 0.f
		- Temperature : 8500
	- SkyLight
		- IntensityScale : 1.5f
	- SkyAtmosphere
		- MultiScattering : 0.8
		- RayleighScattering : Darker
		- MieScatteringScale : 1.5f
		- MieAbsorbtionScale : 0.6f
		- MieAnisotropy : 0.f
		- AerialPerspective : 1.f
	- HeightFor
		- Volumetric Fog 활성화
		- EmissiveColor : Darker
		- ExtinctionScale : 0.8f
##### 73강 : 데이터 애셋
- Data Asset : 변수 값을 애셋으로 저장
- 필요한 것 :
	- BP Parent Class : 변수 정의
	- Parent Class로부터 상속된 Data Asset : 변수에 값 정의
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018124829.png">
	
##### 74강 : 블루프린트 구조
- 현재 변경해야하는 변수가 너무 많음 : 블루프린트 구조체를 사용하여 쉽게 엑세스할 수 있도록 저장
- 구조체 생성 후 변수 추가 -> 기본값 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018131352.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018131401.png">
- Parent Class에 변수 추가(변수 타입은 만든 구조체로 생성)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018131550.png">
- Data Asset에서 추가된 모습 확인
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018131624.png">

##### 75강 : 날씨 전환
- 데이터 애셋의 또 다른 장점은 사용자 지정 썸네일 가능(우클릭->Asset Actions -> Capture Thumbnail)
- DA_Snowy 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018135536.png">
- BP_DynamicSky에 날씨 설정을 위한 함수 2개 추가
	- HandleWeatherSettings : Contstruction 함수 연결 함수
	- SetWeatherLightingProperties : DA를 통해 조명 변수 초기화
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018135635.png">
- Sunny/Snowy간 전환을 위해 CurrentWeatherPreset 변수 추가(Type명은 BP WeatherDataAssetBase - Object Reference)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018135830.png">
- Data Asset을 이용하여 SetWeatherLightingPropertie 함수 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018135938.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018135926.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018135950.png">
- 눈 오는 날씨일 때는 밤으로 변경되지 않으려 함(TimeOfDay 고정) : 이를 위해서는 Weather마다 다른 초기화가 필요하므로 Enum을 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018140057.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018140104.png">
- 이를 통해 HandleWeatherSettings 함수 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018140134.png">
- Contruction 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018140147.png">
- 다만 Snowy일때 시간은 조정이 안되긴하나, 변경 시 Snowy 상태가 풀리는 문제 -> 어디선가 조명값에 변화를 주고 있다. -> Handle Night Setting에서 발견
- 기존에 조명값을 변경하던 부분을 Handle Weather Settings로 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241018140253.png">

#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 76강 : 전체 새로고침
- DA_Snowy 상태가 될 시 구름이 더이상 필요없음. -> Snowy 상태일 시 구름을 끄도록 구현
- Snowy 상태일 때와 Sunny 상태일 때를 구분해서 구현하는 부분이 많으므로 Macro로 새로 구현(GetCurrentWeatherType)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021202256.png">
- 기존 Handle Weahter Setting 함수에서 Switch를 썼던 부분을 새로 만든 Macro로 대체
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021202355.png">
- Cloud 설정을 담당하는 Handle Cloud Settings에서 기존 동작은 Sunny일때, Snowy일때는 구름을 끄는 형식으로 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021202548.png">
---
- Data Asset에서 설정 변경 시 바로 적용되지 않음 -> Construction Script가 BP에 변화가 있을 시 실행되므로 어떠한 변화가 필요함
- 새로운 변수(FullRefresh)를 만들어서 클릭 시 변화가 적용되도록 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021202812.png">

##### 78강 : MF_SnowyWeatherBlend
- Snowy 날씨에 눈이 내림으로 인한 Landscape/물체 들과 같이 Object들에 눈이 쌓인 듯한 Blend를 주기 위해 새로운 Material Function 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021213858.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021213912.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021213926.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021213935.png">
- 이를 Landscape Material 최종값에 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021214001.png">

##### 79강 : Material Parameter Collection
- Material Parameter Collection : 
	- scalar/Vector 변수의 값들을 저장하는 Asset
	- Material과 Blueprint 사이 공유 가능
	- 기존의 Dynamic_Instance도 가능하나 이의 경우 블루프린트가 머터리얼의 래퍼런스를 얻어야 가능. 이번 지형 머터리얼의 경우 레퍼런스 얻을 방법이 없음.
- Material Parameter Collection 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021221836.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021221844.png">
- M_AutoLandscape에 해당 Snowing 변수를 사용하여 If문에 따라 비활성화시 Alpha값에 0을 넣어 눈이 없도록 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021221957.png">
- BP_DynamicSky에도 해당 변수의 값을 변경하는 Macro 생성(Toggle Snow)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021222334.png">
- 해당 Macro를 HandleWeatherSettings에서 날씨에 따라 변경하도록 배치
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021222425.png">

##### 80강 : 섹션 챌린지:눈 객체 블랜드
- 객체에 SnowBlend를 추가하고 싶으면 해당 Actor의 Material로 들어가서 출력 핀을 다음과 같이 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021224618.png">
- 이후 해당 Material로 Instance 생성 후 변수값 변경하며 세부 조정
- 단, 수풀같은 Opacity Mask를 사용하는 Material의 경우 반투명을 고려해야함. -> MF_SnowyWeatherBlend에서 해당 Opacity Mask값을 처리하는 과정 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021224727.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241021224740.png">

#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 82강 : Anim 알림
- Footprint 구현을 위해 필요한 3가지
	- Anim Notify(이번 강의에서 알아볼 것!)
	- Decal Material
	- Niagara System
- Anim Notify 
	- 애니메이션 알림으로 애니메이션 시퀀스 중 특정 지점에서 이벤트를 트리거
	- 이를 통해 Pawn 애니메이션중 발이 바닥에 닿을 때 외부 동작(발바닥 생성)을 수행하도록 구현
- Pawn 구현 기준은 아래와 같다
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023211826.png">
- 오류 발생! : 게임 플레이 누를 시 Snowy가 적용되지 않는 상황 -> 매개 변수 컬렉션을 Construction Script 내에서만 설정했기 때문 -> Event Graph의 Begin Play에 Handle Weather 함수 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023211934.png">
- AnimNotify 생성(Blueprint Class 생성 -> AnimNotify를 parent로 설정)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023212941.png">
- Recieived Notify Function 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023213031.png">
- 해당 애니메이션 이동 후 트랙에서 Notify 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023213111.png">
- 해당 트랙 우클릭 후 Add Notify로 생성한 AnimNotify 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023213139.png">
- 나중에 충돌 방지를 위해 AnimNotify Blueprint -> Class Default -> Show Fire in Editor 비활성화

##### 83강 : 블루프린트 매크로 라이브러리
- Footprint 구현에 필요한 3가지 구현
	- Spawn Limitation : Snowy에서만 나오게
	- Detect Surface : 표면 감지
	- Left/Right Foot : 어느 발인지
- 날씨 인식을 위해 AN_SpawnFootprint안에도 Macro를 만들고 싶으나 불가능 -> 그러나 For each, Branch와 같은 기존의 Macro는 사용가능
- 뭐가 다를까? -> 이 둘은 표준 블루프린트 매크로 라이브러리에 속함 -> 아 그럼 내가 블루프린트 매크로 라이브러리를 만들어서 거기에 사용하고자 하는 매크로를 넣자\
- NM_NotifyMacroLibrary 생성(Parent는 AnimNotify로 어디에 노출할지 설정)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023214836.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023214931.png">
- NM_NotifyMacroLibrary 안에 IsSunny 매크로 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023215046.png">
- AN_SpawnFootprint에 IsSunny 호출
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023220744.png">
- 왼발, 오른발 처리를 위한 Enum 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023220934.png">
- Enum과 Local Variable을 통해 오른발/왼발 변화 처리 진행
- 이때 Local Variable을 쓰는 이유는 해당 Recived_Notify Function이 const이기 때문에 Set을 쓸려면 Local 변수를 사용해야함
- Local 변수는 눈 모양을 눌러서 detail 패널에 보이게 한 뒤 사용할 애니메이션에서 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023221019.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023221057.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023221406.png">
- LineTrace for Object를 이용해서 바닥을 탐지(아래는 전체 함수)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023221128.png">
- 이때 Debug Type을 통해 작동 확인
- 마무리로 애니메이션에서 해당 Notify 채우기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023221226.png">

##### 84강 : 데칼 머터리얼
- decal : Mesh에 투영되는 Materials
- decal Material 생성 : Material 생성 후 Mode 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023222137.png">
- decal Material 늘어짐 현상 제거법 : 기존의 Triplanar 기법 사용
- 이때 World Spcae Normal 입력 핀에 기존의 VertexNormalWS가 아닌 SceneTexture:WorldNormal이 연결된 것에 주의
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023222357.png">

##### 85강 : 나이아가라 리프레셔
- Niagar의 중요 내용
	- Renderers
	- Module/Stages
	- VFX Material
	- Parameter Map
- Renderers
	- 이 강의에서는 2가지의 렌더러 사용
	- Sprite Renderer : 카메라를 향하는 2d 평면 렌더링, 아무리 회전해도 정면이 보임
	- Decal Renderer : Decal을 직접 렌더링
- Module/Stages
	- Module은 블루프린트 함수와 매우 유사 
	- Niagara 작업 시 Stage 아래에서 작업
	- Stage의 종류는 많지만, 모두 Spawn과 Update 유형으로 분류 가능
	- Spawn Stage에 배치된 모든 Niagara Module은 한 번 실행
	- Update Stage에 배치된 모든 Niagara Module은 매 프레임 실행
	- Blueprint의 BeginPlay와 Tick과 유사
- VFX Material
	- VFX Material을 만들 때 주로 두 가지 블렌드 모드를 사용
	- Additive(밝음)/Translucent(어두움)
	- 주로 사용하는 Node는 Particle Color로 이를 통해 Niagara에서 직접 색상과 불투명도를 가져올 수 있음
- Parameter Map
	- Niagara에 배치하는 모든 Module은 기본적으로 Niagara Parameter Map 내의 매개변수에 값을 씀
- 예시
	- VFX Material 생성 및 Mode 변경
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023223634.png">
	- VFX Material 노드 간단하게 구현 및 연결
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023223740.png">
	- Niagara 생성 후 VFX 연결
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241023224155.png">
	
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 86강 : 풋프린트 나이아가라 시스템
- 발자국에 사용할 Footprint Decal 생성. 이를 통해, MI_LeftFoot, MI_RightFoot을 생성
- 이때, Particle Color가 아닌 Decal Color를 사용함에 주의
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025191854.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025192131.png">
- 해당 Decal Material들을 사용하는 Niagara System 생성
- SimpleSpriteBurst 베이스 변경사항
	- Renderer를 Decal Renderer로 변경(Material 설정)
	- Initialize Particle에서 lifetime을 6, Color를 검정으로 설정
	- Scale Color에서 FadeOut 그래프의 시작을 0.5로 설정
	- Decal이 자연스럽게 캐릭터 회전에 맞춰 정렬되도록 Initial Decal Orientation 추가(방향 모드 POrient to Vector -> System)
	- Preview에 안보일 시 Preview Scene Setting에서 Environment->Show Floor 활성화(메뉴 탭 안보일 시 왼쪽 위 Window에서 추가)
	- 추가로, 크기 변경 필요 시 : 원래 Sprite Renderer의 경우엔 Initialize Partice의 Uniform Sprite Size에서 크기 변경 가능.
	- 하지만 Decal이므로 다른 방법 사용 : Decal Renderer 클릭 후 Decal Size Binding에 어떤 변수가 연결되어있는 지 확인, Particle Spawn에서 Set Parameter 추가(Set new or existing parameter directly라 보일 거임)  -> add 누르고 Decal Size 선택(Binding되어 있는 값), 값 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025222517.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025222532.png">
- 이제 AnimNotify인 AN_SpawnFootprints에서 해당 Niagara System 생성 구현
	- Spawn System at Location 으로 Niagara system 생성
	- 생성 시스템 왼/오 구분 위해 Select 사용, Boolean 연결에는 사용한 Bone이름을 가져온 후 String 변환, Contatin 함수를 통해 'l'이 포함되어 있는지 확인으로 구별
	- 생성 Location의 경우 Hit Result를 Local Variable로 바꾼 후 Break hit Result를 통해 필요한 변수(Location)만 가져와 연결
	- Roation의 경우 사용자의 방향과 일치시켜야 하므로 Get Mesh Comp -> Get Owner -> Get Actor Rotation으로 구현
	- 이때, Snowy의 경우에만 구현되어야 하므로 Macro Libarar에서 Get Current Weather Type을 추가로 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025223928.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025224303.png">

##### 88강 : 날씨 입자 준비
- Snow Particle 생성에 필요한 3가지
	- Snow Emitter
	- Smoke Emitter
	- Performance(중요!)
- 모든 Landscape에 Particle을 뿌릴 수 없으므로 생성 반경을 제어(해당 영상에서는 Spawn Shape을 원기둥으로 생성)
- Spawn Shape
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025225122.png">
- Spawn Shape 구현에 있어서 우리가 알아야 할 Camera Properties
	- Camera World Position
	- Camera Forward Vector
	- Camera Up Vector
	- Camera Moving Speed
- 이 모든 것을 계산하기 위해 사용자 정의 Niagara Module 생성 예정
##### 89강 : NMS_GetCameraProperties
- FollowCameraTemplate 이름의 Niagara System 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025231602.png">
- 내부에서 Local Module인 NMS_GetCameraProperties 생성 및 구현
	- Get Camera Properties를 이용해서 Camera 값들 가져와 Map Set으로 변수 저장
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025231711.png">
	- Dynamic Spawn Radius를 계산. 현재 Camera 위치에서 이전 Camera 위치를 뺀 값(이동거리) / DeltaTime을 통해 속도 계산, 속도가 낮을 경우 DefaultSpawnRadius 사용  
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025231747.png">
	- Spawn Origin을 Vector 연산을 통해 계산 
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025232028.png">
- 완성된 Module의 모습
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241025232120.png">
- 이제 생성한 FollowCameraTemplate를 Parent로 새로운 Niagara System 생성 가능

##### 90강 : 눈 입자
- FollowCameraTemplate를 parent로 NS_SnowStorm 생성
- Add Emitter를 통해 Blowing Particle 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026001454.png">
- 세부 속성 조정
	- Emitter Scale에서 Loop Behavior/Loop Duration 조정
	- Spawn Rate에서 SpawnRate 조정
	- Initialize Particle에서 LifeTime 속성/Color Mode(컬러, 투명도) 조정, 이때 New Dynamic Scratch Input으로 입력값에 대한 함수 생성 가능
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026001817.png">
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026001824.png">
	- Shape Location으로 생성 반경 조정 가능, 이때 NS_SnowMan에서 정의한 변수를 대입 가능
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026001919.png">
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026001930.png">
	- Gravity Force로 내려오는 속도 조정 가능
	- Wind Force에서 풍속 조정 가능
- 특정 각도를 볼 때만 눈 입자가 보이는 현상 '클리핑 현상' 발생 : Fixed Bound을 크게 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026002303.png">
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 91강 : 눈 연기 입자
- Snow Smoke를 위한 M_SnowSmokeMaster_Additive 머터리얼 생성
- 이때 Blend Mode : Additive/ Shading Model : Unlit으로 설정
- Depth Fade는 Particle과 바닥간의 경계가 생기는 현상을 없애기 위해 연결
- Dynamic Parameter는 Niagara System과 Material간의 변수 공유를 위해 생성
- SmokeEdgeSoftnessAmout가 1일 시 Particle Size의 10%를 Depth Fade의 Fade Distance로 설정 10일 시는 그대로 사용
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026143158.png">
 - NS_SnowStorm에 SnowSmoke Emitter 추가(parent는 simple burst sprite)
 - Sprite Renderer에서 base material 변경
 - Sprite Renderer에서 Sub Uv/Sub Image Size 8-8로 변경
 - Sub UVAnimation 추가, Sprite Renderer로 설정
 - Spawn Rate로 교환,  Random Range Float로 1-4로 설정
 - Initialize Particle로 Size 키우기(3000)
 - Dynamic Material Parameters 추가
 - SmokeEdgeSoftnessAmout는 Random Range Float로 4-6으로 설정
 - 그 외 다양성을 주기 위해 크기, 사이즈, WInd 등에 random range 적용
 - Scale Color에서 FadeCurve는 Snow_Base와 같게 설정
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026144519.png">
##### 92강 : 나이아가라 시스템 구성 요소 토글
- DA_Snowy일 때만 SnowStorm이 작동하도록 하고 싶음 -> BP_DynamicSky에서 설정
- 새로운 Component인 Niagara Particle System Component 추가 후 NS_SnowStorm 할당, Auto Active는 비활성화
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026150119.png">
- 새로운 Macro 'ToggleNiagaraSystemComponent'생성해서 해당 Component의 Auto Active 조작
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026150200.png">
- 해당 Macro를 사용해서 Snowy일때만 SnowStorm이 작동하도록 설정(Toggle Snow에서 설정)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026150237.png">

##### 93강 : 섹션 과제 - 사용자 매개변수
- Niagara System의 속성 값을 Blueprint에서 쓰기 위해 User Parameter 사용
- 원하는 속성 값에 'Read from new User parameter' 사용해서 User Parameter로 만들기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026192628.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026192656.png">
- Detail 창 커스터마이징 위해 User Parameter를 저장할 Struct 생성 : 안해도 됨. 드롭다운 형식으로 만들기 위한 선택사항
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026192752.png">
- BP_DynamicSky에서 해당 Struct를 변수형태로 갖는 변수 생성, 눈 모양 클릭
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026192828.png">
- 'Set Snow Particle Settings' 이름의 Macro 생성 후 Struct를 이용해서 Niagara System 내의 User Parameter 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026192925.png">
- Detail 창에서 동작 확인
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026192959.png">

##### 94강 : 눈 커버리지 애니메이션
- 눈이 점차 쌓이는 애니메이션 효과 넣어주기 : Lerp 노드 활용
- MF_SnowyWeatherBlend에서 Blend 부분 수정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026193954.png">
- Viewport에서 Actor 클릭 시 BP_DynamicSky만 선택 됨 
	- 이유 : Particle이 퍼져 있기 때문
	- 해결 : 반투명 선택 비활성화하기(키보드 T)
- 이제 BP_DynamicSky에서 시간에 따라 Is_Snowing 변하게 하기(Struct에 변수 2개 추가)
- 시작 시 Snowy 상태 확인 및 Snow Animation 활성화 확인(확인 후 Is_Snowing을 0으로 초기화)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026200733.png">
- 1.5초의 딜레이 후 Set Play Rate로 진행 시간 설정/ Timeline으로 Is_Snowing의 값을 0~1로 천천히 변경 후 적용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026200903.png">
- Timeline은 다음과 같이 설정(이때, F 클릭 시 확대, 1 클릭 시 스무스화)
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026200917.png">

##### 95강 : 기본값 동기화
- 언제나 Macro, Variable등 카테고리화 일상화
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026201538.png">
- 블루프린트를 ViewPort에 드롭다운한 후 다양한 값을 변경했다면 Blueprint와 다시 동기화 필요. 안그럴시 삭제 후 다시 드롭다운하면 블루프린트 기준 기본값으로 초기화됨.

##### 96강 : 눈 애니메이션 조정하기
- 눈 애니메이션에서 발생하는 추가 문제점 해결
1. Snowy Animation을 사용하지 않는 경우 Delay 시간 후 갑자기 눈이 생기는 문제
	- 원인 : Is_Snowing을 0~1로 바꾸는 과정이 애니메이션을 껐을 때도 적용되어  0에서 0.0001로 바뀔 때 If문에 의해 갑자기 눈이 생김
	- 해결 : 애니메이션 유무에 따라 사용하는 변수를 분리(SnowAmount 변수 생성 후 애니메이션의 Is_Snowing을 대체)
	- 과정 : 
		1. MPC_WeatherProperties에 새 변수인 SnowAmount 추가
		2. MF_SnowyWeatherBlend에 SnowAmount 대체
		 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026202531.png">
		 3. BP_DynamicSky에서 Toggle Snow와 Event Graph에서 SnowAmount 항목 추가 및 대체
		 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026202649.png">
		 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241026202741.png">
2. 눈이 내릴 시 바닥에 눈이 너무 골고루 쌓이는 문제
	- 원인 : 눈이 쌓이는 표면에 무작위성이 없어서 갑자기 여러 개의 눈 입자가 화면에 등장 
	- 해결 : 머터리얼 함수를 수정해서 무작위성 추가 그 과정에서 타일링 이슈도 해결
	- 과정 : 
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 100강 : 비오는 데이터 에셋
- 비오는 날씨 구현 절차
	- Lighting
	- Material
	- Interaction
	- Particles
- Rainy 구현 전 관련 Data들 추가
	- Enum 'EWeatherType'에 Rainy 추가
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027121419.png">
	- 'DA_Rainy' 생성
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027121442.png">
	- 'BP_DynamicSky'에서 'GetCurrentWeatherType' 변경
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027121517.png">
	- 'BP_DynamicSky'에서 'HandleWeatherSetting' 변경
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027121556.png">

##### 101강 : 비 오는 날을 위한 조명
*Lighting 구현*
- 비 오는 날씨에 맞춰 DA_Rainy 조명 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027140406.png">
- 비 오는 날씨에는 2D Cloud가 되도록 설정
- 비 오는 날씨 구름 설정을 위해 새로운 구조체 S_RainyWeatherSettings 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027140453.png">
- 해당 구조체를 통해 비오는 날 2D Clouds 날씨를 조정하는 Macro 'Set 2D Clouds Settings Rainy'생성(구조체를 Parent로 변수 'Rainy Weather Settings' 생성)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027140554.png">
- Handle Cloud Setting에서 위의 사항들 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027140634.png">

##### 102강 : 웅덩이의 속성
*Material 구현*
- 물 웅덩이(Puddle) 구현
	- Shape
	- Key Material Attributes(Base Color/Specula/Roughness/Normal)
	- Ripples(잔물결)
	- Waves(파도)
- 이번 강좌에서는 Shape과 Key Material Attributes 구현
- Puddle Example Material 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027142832.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027142847.png">
- Mask에서 필요한 Channel을 사용하고 싶을 때 사용하는 2가지 노드
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027143018.png">
- 이 두 노드의 동작은 거의 동일하나, Static의 경우 Runtime 도중에는 변경 불가능이라는 차이점 있음
- 결과
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027143103.png">

##### 103강 : 잔물결(Ripples)
- 이번 강좌에서는 Ripples 구현
- Flipbook Texture : 애니메이션도 처리해줌
- Ripple 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027144928.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027145014.png">
- 이때 Frac 사용이 중요 Frac은 정수부를 버리고 소수부만을 취함. 이를 통해 좌표를 각 쉘로 할당시켜줌(Flipbook 사용에 필수적)
- 구현한 CachedPuddleNormalOutput을 기존의 웅덩이의 Normal과 교환
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027145041.png">
---
- 잔물결이 가장자리를 넘어 생기는 문제 발생
	- 원인 : Mask의 값이 0~1 사이인 부분(0.01등)에도 잔물결이 생성되는 문제
	- 해결 : 잔물결이 사용하는 Mask에만 1 미만의 값들을 전부 제거
		1. 웅덩이 마스크를 재사용하기 위해 Cached 사용
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027145817.png">
		2. Lerp와 Step 노드를 사용해서 잔물결용 마스크 추가 적용
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027145850.png">

##### 104강 : 웅덩이 물결
- 웅덩이 애니메이션을 구현은 Normal에 Animation을 줘서 사용
- 내부 함수 'Motion4WayChoas_Normal'을 사용하여야 하나, 이는 라이브러리에 노출되어 있지 않으므로 우클릭 후 MotionFunctionCall(혹은 F누르고 왼쪽 클릭) 생성 후 해당 함수 할당
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027151721.png">
- 그러나 해당 함수 내부에는 문제가 있으므로 이를 복사하여 MF 생성 후 문제 해결하여 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027151804.png">
- 수정한 해당 함수를 사용하여 Wave 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027153917.png">
- 기존 잔물결 Normal과 결합해야함. Add를 쓸 수는 있으나 이는 Normal의 강도가 낮아지는 문제가 발생. BlendAngleCorrectedNormal 사용(Lerp 전에)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027154018.png">

##### 105강 : MF_GenerateRainyWeatherPuddles
- 이전에 만들었던 Puddle Example Material의 기능을 그대로 가져온 MF_GenerateRainyWeatherPuddles 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027162234.png">

##### 106강 : 스무스 스텝
- 경사면에도 물웅덩이가 있는 문제 : 경사쪽 Mask를 0으로 만들기
- 해결 법 : Smooth Step을 사용.
- Smooth Step : Min/Max/Value값을 입력으로 받아
	- Min > Value : 0
	- Max > Value > Min : 0~1
	- Value > Max : 1
	- 이를 사용하는 이유는 Max와 Min 사이일 시 Smooth하게 변환을 넣어 경계가 생기지 않도록 구현
- 적용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027173256.png">

##### 107강 : 비 토글
- DA_Rainy가 아닐 때는 웅덩이가 없도록 Toggle Rain 구현
- MPC_Weather에 Is_Rainning 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027180705.png">
- MF_GenerateRainyWeatherPuddle에 Is_Rainning이 1일 때만 웅덩이가 생기도록 노드 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027180755.png">
- BP_DynamicSky에서 Toggle Rain 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027180815.png">
- HandleWeatherSettings에서 Toggle Rain 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027180836.png">

##### 108강 : 리퀴드 마스터 머터리얼
- Rain Particles 생성 과정
	- Liquid Material
	- Surface Interaction
	- Performance
- Liquid Master Material 생성(Blend Mode : Additive/Shading Model : Unlit)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027200758.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027200813.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027200843.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027200902.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027200917.png">
- 전체 배치
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027200936.png">

##### 109강 : 메인 빗방울
- Particle의 두 종류
	- CPU Particle : 다량의 Paritcle 생성에 불리, 콜리전 등의 이벤트 처리 가능
	- GPU Particle : 다량의 Particle 생성에 유리, 콜리전 등의 이벤트 처리 불가
- 빗방울 아이디어 : 소량의 CPU Particle을 생성해서 Collision Event를 처리, 빈 곳을 채우기 위해 다량의 GPU Particle 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027201403.png">
- NS_Rain 생성(base는 follow camera)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027202122.png">
- Simple Sprite Burst Emitter 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027202143.png">
- 내부 설정값 변경
	- Sprite Renderer에서 Material 설정
	- Sprite Renderer에서 Alighnment : Velocity Aligned
	- Sprite Renderer에서 Sub UV : 3-2
	- Particle Update에 새로운 Module 추가 : Sub UVAnimation / Dynamic Material Paramters
	- Sub UVAnimation에서 sprite 설정 : Sprite Renderer
	- Dynamic Material Parmeter에서 Random Float로 값 설정
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027202343.png">
	- Emitter State에서 Life Cycle Mode System으로 변경/ NS_Rain의 System State에서 Lifetime을 1로 변경
	- Spawn Burst 삭제 후 Spawn Rate 추가 -> SpawnRate 2000으로 설정
	- Initiallize Particle 값 변경(Sprite Size 변경에 주목)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027203258.png">
	- Shape Location 모듈 추가
	- Scale Sprite Size 모듈 추가, 상승 곡선으로 변경
	- Gravity Force  모듈 추가
	- 진행 사항
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027203424.png">

##### 110강 : 거리별 밝기
- 위를 볼 때 비 Particle이 사라지는 문제 발생
	- 원인 : 생성 Cylinder Origin 계산이 카메라 전방 벡터 + 위 벡터라서 위를 볼시 대각선 위에 생기는 문제 발생
	- 해결법 ; 위 벡터 계산을 카메라 기준이 아닌 World 기분 절댓값(0,0,1)로 계산하게하여 언제나 우리 위에 있게 하기
	- 과정 :
		- NMS Get Camera Properties Origin 계산 부분 변경
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027204238.png">
---
- 빗방울이 카메라에 아주 가까이 다가오면 너무 밝음
	- 원인 : 그냥 비가 너무 밝음
	- 해결법 : 전체적으로 낮추기 보다는 카메라를 기준으로 밝기를 낮추기(가까우면 어둡게=투명하게)
	- 과정 :
		- Scale Color 에서 Scale RGB를 대상으로 Scratch Dynamic Input 생성
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027205818.png">
		- DI_BrightnessByDistToCamera 구현
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027205918.png">
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027205930.png">
	- 이때 CurrentCamearWorldPosition의 경우 기존 System의 Parameter. 가져오는 법
		- System overview로 가서 해당 변수 우클릭 Copy Reference
		- Scratch로 와서 해당 시스템 Base 변수 생성(여기선 Position) 이름에다가 붙여넣기
		- 앞에 System_ 삭제 후 Input->System으로 Namespace 변경
	- 구현한 Scratch의 각 값들을 Scale Color 모듈에서 변경(Random Range Float 사용해서 무작위성 추가)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241027210201.png">
	
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!

##### 111강 : 룩업 각도별 밝기
- 카메라 위를 볼 시 비의 밝기가 너무 밝은 문제
	- 해결 : 위를 볼 시 비의 밝기를 낮추기
	- 아이디어 : 전방 벡터와 위 벡터의 내적 후 Arccos 적용 시 각도가 나옴. 이 각도를 기준으로 일정 이하일 시 밝기 낮추기
	- 구현 : 기존의 밝기 제어 모듈인 'DI_BrightnessByDistToCamera' 사용
		- 변수 생성
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028143507.png">
		- 밝기 제어
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028143551.png">
##### 112강 : 충돌 이벤트
- 빗방울 튀는 것을 위한 Collision Event 설정
- 'MainRainDrops_CPU' 변경사항
	- Collision Module 추가
	- Kill Particles Module 추가 : 변수 값으로 HasCollided 설정
	- Generate Collision Event Module 추가
	- Properties에서 Requires Persistenet IDs 활성화
- 충돌 시 생성될 Particle인 'RainSplashes' 추가(Parent는 SimpleSpriteBurst)
	- Stage클릭 후 Event Handler 추가
	- Receive Collision Event Module 추가 값 입력
		- Source : MainRainDrop의 Collision Event
		- Execution Mode : Spawned Particles(이래야 안 깜빡임)
		- Max Events Per Frame : 프레임당 이벤트 발생 횟수(10)
		- Spawn Number : 스폰 갯수(10)
	- Emitter State에서 Life Cycle System으로 변경
	- Scale Burst Module 삭제
##### 113강 : 빗방울 튐
- 새로 만든 Emitter에 사용할 Material Instance 생성을 위해, 기존의 'M_LiquidMaster_Additive'를 사용하여 'MI_RainSplashes_Additive'생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028150052.png">
- 나이아가라 시스템의 'RainSplashes' Emitter에서 Sprite Renderer로 가서 해당 MI 적용 후 SUB UV값 4-4로 변경.
- 정확한 빗방울 생성 위치를 조정하기 위해 'MainRainDrops_CPU'의 Collision에서 Particle Radius Scale 낮추기(0.15)
- 'RainSplashes' 속성 조정
	- LifeTIme Random화(0.5-0.75)
	- Color에 NID_RandomOpacity(동적 스크래치 사용자 모듈) 적용(0.3-0.5)
	- Sprite Size 'Random Uniform'으로 변경 후 값 적용(25-50)
	- Dynamic Material Parameter Module 추가 및 값 조정
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028151053.png">
- Local Module(동적 스크래치) 다른 나이아가라 시스템에도 노출하는 법
	- 해당 모듈 우클릭 후 'create Asset' 저장
	- Asset 들어가서 Category 설정 후, Library Visibility를 Exposed로 변경
##### 114강 : GPU 비
- GPU Emitter인 'MainRainDrops_GPU' 생성
	- CPU Emitter 복사 붙여넣기
	- Properties에서 값 변경
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028152144.png">
	- Generate Event 모듈 삭제 및 Collision/Kill Particles 비활성화
	- Spawn Rate에서 Multiply Float로 바꾼 후 A에는 CPU와 같은 Rate값, B에는 배율을 설정(사진 속에서는 CPU보다 10배 많은 Particle을 생성한다는 뜻)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028152309.png">
---
- 비가 User Pawn에는 충돌이 안됐으면 좋겠음
	- 해결법 : Collision 모듈에서 Collsion Channel을 Visibility로 설정(어떤 채널을 쓸지 모르겠다면 ThirdPerson BP로 들어가서 Collision Capsule의 채널을 보고 결정)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028152603.png">
##### 115강 : 섹션 챌린지 : Rain FX 토글
- Rainy 일때만 비가 오도록 구현하기
	- ViewPort에서 NS_Rain 삭제
	- BP_DynamicSky에서 Niagara Component 추가 및 NS_Rain 할당/Auto Activate 비활성화
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028153454.png">
	- Toggle Rain 후반부에 노드 추가
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028153513.png">
##### 117강 : Rain FX 사용자 매개변수
- NS_Rain속 속성을 BP_DynamicSky의 Detail에서 조정할 수 있도록 설정
	- NS_Raint에서 User Parameter 생성
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028165414.png">
	- S_RainyWeatherSettings에 해당 User Parameter들 추가
	 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028165453.png">
	 - BP_DynamicSky에서 해당 속성을 Detail을 통해 제어할 수 있도록 Macro 'SetRainParticlesSettings' 추가 및 구현
	 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028165555.png">
##### 118강 : 피지컬 머터리얼
- Physical Material : Material을 통해 물리적으로 시뮬레이션된 Primitive가 적용된 Asset으로 물리적 객체가 세계와 동적으로 상호작용할 때의 반응을 정의하는데 도움을 줌.
- Puddle 물튀김을 생성하는 과정
	1. Project Settings : 프로젝트 설정에서 사용자 정의 물리 머터리얼 타입을 정의
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028170919.png">
	2. Physical Material Asset : 물리 머터리얼 에셋 생성 후 Puddle로 설정
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028172549.png">
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028172636.png">
	3. Phys 인식 logic 처리
		3-1.  AN_SpawnFootprints에서 Is_Sunny 매크로를 ShouldDoLineTrace로 이름 변경 후 내부 로직 변경
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028173045.png">
		3-2. GetCurrentWeather Type에서 Rainy 처리 부분 추가 구현
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028173304.png">
	4. Landscape Phys Material Output 처리 : 다음 장 설명
##### 119강 : 랜드스케이프 피지컬 머터리얼 출력
4. Landscape Physical Material Output 처리
	- Node 주의 사항 : 
		- 랜드스케이프와 랜드스케이프 머터리얼과 함께 사용
		- 입력 소켓은 단일 float값
		- Material Parameter Collection과 같이 작동하지 않음(기본값만 받고 머터리얼 노드 내 업데이트를 고려하지 않음)
	- 과정 :
		1. AutoLandscape Material에서 우클릭 후 노드 생성 및 입력값 추가 후 PM_Puddle 추가
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028174120.png">
		2. 해당 Input Socket에는 Puddle의 위치를 알려줄 단일 Float값이 필요한데 어떡하지? -> MF_GenerateRainyWeatherPuddles 안에서 Noise Texture를 통해 Mask를 생성했었지 -> 밖에서는 접근 불가능한데 어떻게 해야할까 -> 출력핀을 추가해서 해당 마스크를 연결하자!
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028174824.png">
		4. 0~1사이의 애매한 부분을 밟아도 웅덩이가 detect되기 때문에 Round를 통해 반올림하여 애매한 부분들 삭제
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028174949.png">
##### 120강 : 물웅덩이 물튀김
- PuddleSplash를 표현하기 위한 Material인 MI_PuddleSplashes_Additive 생성(Base는 M_LiquidMaster_Additive)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028180849.png">
- 해당 Material을 사용할 NS_PuddleSplash 생성(Simple Sprite Burst)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028183652.png">
- NS_PuddleSplash 내부 속성 변경
	- Sprite Renderer에서 Material변경
	- 각종 속성들 Random Float 설정
	- Dynamic Material Paramter 추가
	- Scale Sprite Size 모듈 추가 후 Ease-in 그래프 설정
	- Scale Sprite Size의 사이즈 증가의 시작점이 밑이였으면 좋겠으므로 Sprite Renderer에서 Default Pivot 위치 변경
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028183945.png">
	- Pivot 위치 변경으로 Particle의 위치가 위로 올라갔으므로 Initialize Particle에서 Position Offset을 통해 조정
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028184028.png">
- AnimNotify에서 Rainy일 때 해당 NS Spawn 하도록 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028184551.png">

##### 122강 : 번개 플래시
- 번개 표현을 위한 NS_Lightning 생성
- 번개 플래시의 특징
	- 매우 순간적 : LifeTime을 매우 짧게 설정
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028190416.png">
	- User 기준 엄청 위에 존재 : DynamicSpawnOrigin 기준 Z축을 많이 증가시킨 위치에 Position Offset 설정
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028190520.png"> 
	- NDI_ComputeLargeNumber는 큰 숫자를 쉽게 입력할 수 있는 사용자 정의 Scratch Dynamic Input
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028190628.png">
	- 아주 큼 : Sprite Size에 아주 큰 값 부여
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028190703.png">
	- 생성에 무작위성 필요 : Sprite Burst Instantaneous에 Random Float 추가, Loop Duration에 Random Float 추가
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028190745.png">
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028190808.png">

##### 123강 : 번개 볼트
- Lightning Bolt를 표현하기 위한 Material 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028200028.png">
- NS_Lightning에서 새로운 Emitter LightningBolt(Simple Sprite Burst) 생성 및 속성 변경
	- 크기 변경
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028200205.png">
	- Sub UV 설정 변경(4-1), Sub UV Animation 추가
- Bolt 카메라에서 밀어내고 Random 생성하기
	- Camera 기준 거리를 만들고 특정 범위 내에서 Random한 위치값을 반환하는 Scratch Input을 만든 후 Position에 할당
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028204221.png">
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028204230.png">
	- Initialize Particle 내부 구현
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028204651.png">
- Scale Sprite Size 모듈 추가 후 내부 수정<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241028204342.png">
- 위에서부터 변화가 시작되기를 원하니 Pivot 값 변경(0.5-0), 변경에 따라 Z축 이동이 생기기 때문에 보정해주기 위해 UpOffsetScale의 값 조정
- Spawn Burst Instantaneous 모듈 생성 후 랜덤 생성 구현(0.5-0.6)
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!
##### 126강 : 표면의 빗방울
- 표면의 빗방울 처리를 위한 Material 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241029104136.png">
	- 새로운 노드 설명
		- ConstantBiasScale : 입력으로 받은 값에 Bias만큼 더하고 Scale만큼 곱함. 해당 구현에서는 0~1로 되있는 채널을 -1~1로 재매핑하기 위해 Bias에 -0.5, Scale에 2를 넣음
		- DebugScalarValues : Material 구현 과정에서 값들을 화면으로 볼 수 있도록 Debug를 도와주는 노드
		- DeriveNormalZ : X와 Y값을 통해 Z값을 유추하는 노드. 유추 식은 sqrt(1-(x*x + y*y))
		- TImeWithSpeedVariable : 이 노드를 쓰면 다음과 같이 점점 올라가는 숫자를 얻을 수 있음. 여기서 Frac을 통해 소숫점만 가져오면 0~1 사이에서 증가하는 반복되는 값을 가져올 수 있음.
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241029105322.png">
- 표면 빗방울에 무작위성 주기 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241029104846.png"> 
##### 127강 : 포스트 프로세스 빗방울 FX
- 화면에 보이는 빗방울 효과를 위해 Post Process Material 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241029110954.png">
- 생성 후 설정 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241029111013.png">
- 이전에 만든 RainDrop을 들고 와서 DeriveNormalZ 부분 삭제 후 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241029114028.png">
- 해상도에 맞추기 위해 Texture Sample의 UV에 연산 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241029114055.png">
#### Unreal Engine 5 : 강의 하나로 DynamicSky 시스템 완벽 마스터하기!
##### 128강 : 시스템에 포스트 프로세스 FX 추가
- 시스템에 PostProcess FX 추가 및 토글을 통한 제어를 위한 과정
	1. MPC_WeatherProperties에 EnableRainDropsPostProcessFX 추가
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030124456.png">
	2. PPM_RainDropsOnLens에 Is_Raining&&EnableRainDropsPostProcessFX 일때만 작동하도록 노드 추가
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030124540.png">
	3. 토글을 위해 S_RainyWeatherSettings에 EnableRaindropsPostProcessFX 변수 추가(이전에 진행했던 번개도 Rainy Tap에 넣기 위해 ShouldEnableLightning도 추가)
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030124640.png">
	4. Toggle Rain에 번개, PostProcessFX 토글 추가
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030124715.png">
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030124731.png"><img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030124743.png">
##### 131강 : 물 웅덩이 솔루션
- 물 웅덩이 애니메이션 생성법
	- Material : SmoothStep에서 Min의 값을 1~0으로 바꾸면서 점차 Noise Texture가 퍼져나가게 하기
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030144543.png">
	- MPC_WeatherProperties
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030144953.png">
	- S_RainyWeatherSettings : ShouldAnimateRainCoverageInRuntime와 FullSnowCoverageTime를 추가
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030145055.png">
	- BP_DynamicSky : Toggle Rain
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030144834.png">
	- BP_DynamicSky : Event Graph
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241030145155.png">
