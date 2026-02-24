#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 6강 : 기본 데이터 유형
- Material의 대표적인 Data Type 3가지 : Constant 1/2/3 Vector
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240804144639.png">
- BaseColor는 Constant 3 Vector를 사용.
- 숫자 1/2/3을 누른 채로 좌클릭 시 빠르게 Vector 생성 가능(단축키)

##### 7강 : 러프니스
- Roughness(1float) : 표면 반사정도를 설정. 0에 가까울수록 매끄럽게 되어 반사정도 증가

##### 8강 : Lerp 사용법
- Lerp(Linear Interpolation) : 선형 보간
- A와 B의 값을 Alpha 값을 통해 선형 보간 : Alpha가 0에 가까울수록 A, 1에 가까울 수록 B의 값을 반환
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240804150532.png">
- 이러한 Alpha의 특성을 통해 Noise Texture의 활용 가능
- Noise Texture에서 검정 부분이 1, 하얀 부분이 0, 회색 부분은 중간값
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240804150656.png">
- 이러한 Noise Texture의 색상 정보를 가져오기 위해 Texture Sample 노드 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240804150744.png">

##### 9강 : UV
- Noise를 통한 패턴 표현에서 한 가지 Noise로  Object마다 다른 패턴을 줄려면 어떻게 해야할까? -> UV 
- UV Mapping : 2D image를 3D 모델 표면에 투영하는 것
- U는 수평 축 / V는 수직 축을 의미함
- Node를 통한 조정에서는 Texture Coordinate(텍스쳐 좌표)를 통해 값 조절
- 이때 U와 V의 값이 커질 수록 투영되는 Texture의 크기가 작아져 패턴이 더 밀집되고, 값이 작아질 수록 크기가 커져 패턴이 더 확산됨
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240804154046.png">

#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)

##### 10강 : 컴포넌트 마스크
- 컴포넌트 마스크 : 여러 축으로 이루어진 값을 각각의 축으로 분리하여 사용하고 싶을 때 사용하는 노드
- Append : 분리된 값들을 다시 하나로 합치는 노드
- 사용 예시 : 
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810151129.png">

##### 12강 : 움직이는 텍스처 구현하기
- 특정 Texture의 투명도를 제어하기 위해서는 Detail 패널의 Blend Mode를 Translucent로 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810153645.png">
- 이때 Texture Sample의 R,G,B를 연결해보며 원하는 결과값 찾기(단, 찾기 어려울 시 직접 Texture에 들어가 R,G,B 껐다 켜보기)
- UV의 값 변경으로 움직이는 Texture 구현 가능
- 이동 거리 = 시간 * 속도 공식을 사용하며, 이때 시간은 Time 노드, 속도는 Constant1Vector 노드 사용
- Multiply, Substract, Add, Append 등의 계산 노드를 이용하여 원하는 Texture 이동 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810154802.png">

##### 13강 : 패너
- Panner : 위의 과정을 압축한 노드
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810155438.png">

##### 14강 : 머터리얼 인스턴스
- 원하는 설정 값들을(Constant1Vector 등) Parameter로 바꾼 후 해당 Material을 통해 Material Instance를 만들면 창 하나에 Parameter들을 모아 관리가능
- S 누르고 좌클릭 시 바로 Parameter 생성 가능

##### 16강 : 불 머터리얼 생성하기
- 가로/세로와 같이 2가지 움직임을 동시에 구현하고 싶을 시(대각선X) 2개의 Panner-Texture Coordinate를 생성 후 Multiply로 합쳐주기
- 밝기를 올릴려면 Base Color와 Emissive Color로 들어가는 값에 Multiply 곱해주기

##### 18강 : 사인 표현식
- Sine : 시간에 따라 값이 주기적으로 바뀌는 제어를 위한 Sin 함수를 표현해주는 노드. 
- Sin은 -1 ~ 1 사이 값을 반환하는데 머터리얼은 음수 값을 사용하지 않음
- 이에, Saturate 노드를 이용하여 0과1사이 값으로 변환
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810173344.png">

##### 19강 : 사인 표현식 다루는 방법
- 위의 사인 표현식을 특정한 값 범위로 보간하고 싶다면 Lerp 활용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810174126.png">
- Sine_Remapped : 위의 과정을 언리얼 내부적으로 구현한 노드 
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810174530.png">

##### 20강 : 떠다니는 바위
- 다양한 움직임 표현을 위해서는 World Position Offset 이용
- 이때도 Sin의 사용이 가능한데. 좀 더 Random한 움직임을 주고 싶을 시 함수간 Add 사용.
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810230444.png">
- 사용 예시
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810230459.png">

##### 21강 : 디졸브 머터리얼 생성하기
- 디졸브 : 사라졌다가 나타났다가 하는 행위
- 투명도를 제어하기 위해 Detail 패널의 Blend Mode를 Translucent로 변경
- Opacity에 noise texture와 Sin을 통한 값 변화를 적용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810231834.png">

##### 22강 : 가장자리에 빛나는 효과 추가하기
- Named Reroute를 통해서 노드의 집합을 함수처럼 사용 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810234835.png">
- Noise(LowRes)의 UV에 Noise 연결 시 가장자리들에 대한 정보를 얻을 수 있음.
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240810235521.png">
- 이렇게 구한 가장자리 값을 Emissive Color에 곱해서 가장자리에 맞춰서 빛이 나도록 설정

#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 24강 : 디졸브 머터리얼과 상호작용하기
- 플레이 도중 Material의 Parameter를 변경하여야 할 경우 Dynamic으로 변환이 필요함.
- 이는 블루프린트에서 진행되며 다음과 같음
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811160913.png">
- Set Material을 통해 블루프린트의 Component에 Material 설정
- Set Scalar Parameter Value를 통해 Material 속 Parameter 설정
- TimeLine 설정을 통해 원하는 값이 변화를 시간에 맞춰 구현
- End Overlap의 경우 TimeLine의 Reverse에 연결하여 역동작 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811161258.png">

##### 28강 : 마스터 머터리얼 소개
- Master Material : 수 많은 Object에 적용되는 Intance의 주체로, Material의 설정 값에 대한 모든 변화 권환이 있음.

##### 29강 : 완전한 UV 제어
- Advance UV Control : 기존에 하던 'UV값 설정을 통한 패턴 변화', 'UV Offset 값 변화를 통한 패턴 이동'을 Constant4Vector를 통해 더 수월하게 구현 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811163215.png">
##### 30강 : 정적 스위치 파라미터
- Static Switch Parameter : True/False에 따라 값을 선택적으로 받아옴.
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811163919.png">
- 본 강좌 사용 예시 : UV를 따로 설정하고 싶을 때 True, 같이 설정하고 싶을 때 False

##### 31강 : 완전한 Color 제어
- 다양한 색 제어 구현
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811165810.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811165822.png">

##### 32강 : 변수 정리
- Parameter의 Detail 설정을 바꿔 그룹화해 Master Material에서의 가시성을 높일 수 있음.
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811192732.png">
- Group을 통해 Parameter의 그룹을 설정. 이때, 그룹의 정렬을 위해 이름 앞에 숫자를 붙이기.
- Sort Priority를 통해 그룹 내 순서를 결정

##### 33강 : Metalic 제어
- 메탈릭 : Material의 금속 정도(매끈매끈함)를 결정 1에 가까울수록 금속, 0에 가까울수록 비금속
- 관련 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811194159.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811194352.png">

##### 34강 : Specular 제어
- Specular : 비금속성 표면의 반사정도를 설정 
- 관련 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811195322.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811194338.png">

##### 35강 : Roughness 제어
- Roughness : 표면의 매끄러운 정도를 제어
- 관련 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811195932.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811195940.png">

##### 36강 : 텍스쳐 압축 설정
- 원본 Texture Image에서 다음과 같은 설정들 변경
	1. Compress Without Alpha : Alpha 채널을 사용하는가 확인. 안할 시 비활성화
	2. Compression Settings : BaseColor에 사용 시 Default, Roughness와 같은 용도로 사용 시 Masks
	3. sRGB : BaseColor 시 활성화, 그 외 비활성화

<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811200604.png">

- Material에서 Texture Parameter들의 Detail에서 다음과 같은 설정들 변경
- Sampler Type : sRGB 활성화 시 Color, 그 외(Mask 등) 시 Linear Color
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240811200620.png">
#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 37강 : 노멀(Normal)
- Master Material에서 Normal 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915160534.png">
- 언리얼에서 Normal Texture는 DirectX, OpenGL이 존재
- 보통 DirectX를 사용, OpenGL은 다른 에디터 전용
- OpenGL밖에 없을 시 Detail에서 Flip Green Channel 시 DirectX와 동일하게 사용 가능

##### 38강 : 앰비언트 어클루전 (Ambient Occlusion)
- AO : 가려짐으로 인한 빛의 감쇠를 근사화하는 효과(가려짐으로 인한 그림자)
- Master Material에서 AO 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915163450.png">

##### 40강 : 채널 패킹
- AO, Roughness, Metalic의 경우 단일 float값을 사용 => R,G,B 채널의 값이 같음
- 이러한 낭비를 줄이기 위해 하나의 Texture에 3가지 요소를 매핑
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915164210.png">

##### 43강 : 섹션 과제2 : 마스터 머터리얼 내 채널 패킹된 텍스쳐
- Master Material에서 패킹된 텍스쳐 언패킹 하기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915165625.png">
- 패킹된 텍스쳐 사용 여부 결정 기능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915165636.png">

##### 44강 : 디스플레이스먼트(Displacement)
- Displacement : Mesh 표면의 높이차를 만들어주는 Texture
- 단, 언리얼 자체로는 적용 불가능해 외부 디자인툴(Blender), 언리얼 디자인 툴을 사용해야 함.

##### 45강 : 프로젝트 템플릿 생성하기
- 원하는 초기 환경으로 구성된 사용자 정의 템플릿 생성가능
- 프로젝트 생성 -> Migrate를 통해 해당 프로젝트의 환경 구성
- C:\Program Files\Epic Games\UE_5.4\Templates 로 이동해서 파일 생성
- C:\Users\qudtn\UnrealEngine 로 이동 후 해당 프로젝트에서 템플릿 폴더로 Config, .uproject, Content 복사
- 해당 프로젝트의 Template으로 쓰인 템플릿 폴더로 이동 후 Config -> TemplateDefs.ini 가져오기
- TemplateDefs 메모장 편집으로 제목, 설명 변경

#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 49강 : 씬 계획하기
- Scene을 계획하는 순서(상황에 따라 다름!)
	1. 참조 이미지 찾기 : 현실 세계, 이미지, 영상 등 다양한 수단을 통해 씬에 대한 아이디어 탐색
	2. Block Out : 기본적인 Geometry를 통해 Scene의 간단한 모형 생성
	3. Layering : Block Out을 통해 생성한 모형에 에셋을 이용하여 쌓아가는 절차

##### 50강 : 씬 조명 작업
- Add Quixel Content를 통해 멋진 Asset들을 불러오기 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915210339.png">

- 자동 노출 조정을 지우기 위해서는 Post Process Volume 배치 후 -> Metering Mode를 Manual로 변경 후
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915210515.png">
- Infinite Extent로 맵 전체 적용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915210553.png">
- 이후 Exposuer Compensation 설정으로 원하는 만큼의 빛 노출 설정

##### 52강 : 머터리얼 블렌드
- 머터리얼 블렌드 : 머터리얼 여러 개를 적절히 섞는 작업. 
- Quixel Bridge에서 Surface 선택 후 우측 밑 버튼으로 Blend Material 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915223107.png">
- 이후 Blend Material(Master Intance) 실행 후 Middle,Top Layer 설정

##### 53강 버텍스 페인팅
- 블렌딩한 머터리얼에서 Middle,Top Layer를 적용하려면 Vertex Painting을 이용 이를 위해서 모드를 Mesh Paint로 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915230050.png">
- Channel에서 Red = Middle Layer, Green = Top Layer
- 이때, Paint Color를 검정색으로 해야 칠해짐, 흰색은 지우개
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915230118.png">
- Material Instance에서 Albedo를 통해 색상 조정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915230232.png">

##### 56강 : 페인트 퍼들
- Blend Material에서 Puddle Layer를 체크함으로써 물웅덩이 생성 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240915234138.png">
- Paint의 Blue 채널 사용

##### 58강 : 데칼(Decal)
- Material 앞에 붙이는 스티커
- Quixel Bridge에서 다운로드

##### 59강 : 정적메쉬 채우기
- Quixel Bridge에서 정적메쉬들로 맵 꾸미기 가능
- 이때, Mesh 배치가 Decal에게 방해받을 시 Detail 설정으로 영향 안받게 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916003648.png">

##### 60강 : 폴리지 모드
- 에셋을 손쉽게 뿌릴 때 사용하는 모드
- 모드 변경 후
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916004130.png">
- 원하는 에셋을 드래그한 후 클릭, 크기 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916004456.png">
- Paint로 드래그로 설치

##### 61강 : 레벨 연출 설정
1. Level Sequence 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916010551.png">
2. 카메라 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916010617.png">
3. 시퀀스에 카메라 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916010652.png">
4. ViewPort 레이아웃 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916010714.png">
5. 왼쪽 Layout은 Perspective, Allow Cinematic Control 해제
6. 오른쪽은 Cinematic ViewPort, 오른쪽 위 그리드 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916010750.png">
7. 오른쪽 ViewPort에 카메라 고정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916010823.png">

##### 62강 : 카메라 움직임
- 카메라 3설정
	- Aperture(조리개) : 높을수록 빛을 덜 받아들임->어두워짐
	- Focal Length(초점 길이) : 줄일수록 축소
	- Focus Distance(초점 거리) : 초점을 잡는 거리
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916010942.png">
- 편집 칸을 이용해서 다양한 편집 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916014304.png">

##### 63강 : 씬 렌더링하기
- Master Sequence : 여러 Level Sequence를 모아놓은 상자 같은 존재(Level Sequence 생성 -> Add에서 Shot Track 추가 -> 기존에 제작한 Sequence 넣기)
- 렌더링 위해 **Movie Render Queue** 플러그인 추가
- 퀄리티 높일려면 png로 렌더링 + Anit-Aliasing 설정 추가
#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 67강 : 랜드스케이프 프로젝트 구축하기
- 초기 설정 
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916140802.png">

##### 68강 : 기본 조명 설정
- Scene에 Lighting 설정
- Main Light Source : Directional Light(Sun/Moon)
- We need a sky : Sky Atmosphere + Volumetric Cloud + Sky Light
- Get rid of the black void : Height Fog
- PostProcessVolume 설정 : Infinte + auto 설정
- 이 모든 과정을 Light Mixer로 쉽게 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916190055.png">

##### 69강 : 간단한 조각하기(Sculpting)
- Landscape 모드를 통해 원하는 모양의 지형 생성 가능
- 사용법 참고 : https://www.youtube.com/watch?v=gwLotMY_Fe8
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916201545.png">

##### 70강 : 머터리얼 함수
- Material Function을 통해 반복되는 Material Node 작업의 재사용성 및 모듈성 증가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916204332.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916204339.png">

##### 71강 : 머터리얼 함수로 베이스 컬러 제어
- 이를 통해 Material 함수 제어 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240916204415.png">
#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 72강 : 카메라 Depth Fade 표현식
- Mask : 머터리얼 내 여러가지 표면 유형을 정의할 때 사용(필터), 0-1사이 값을 가짐
-  Tiling 문제 : 큰 Mesh에 Texture를 깔게 되면 의도치 않은 반복적인 패턴이 나타날 수 있다.
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917162419.png">
- 첫 번째 해결법 : Camera Depth Fade로 Object가 카메라로부터 떨어진 정도에 따라 변화를 줌. 카메라 주변 검정(0) -> 멀어질수록(1)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917162600.png">
- FadeFallOff : 완전 하얗게 되는 거리(1)
- FadeStartDistance : Fade가 시작되는 거리
- 활용 : Lerp를 이용하여 거리에 따라 Texture의 크기를 다르게 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917162716.png">

##### 73강 : 텍스쳐 바밍(Bombing)
- Tiling을 깨는 2번째 수단 : Texture Bombing
- 이때, UVs가 Texture Coordinate가 아닌 Landscape Coords임에 주의
- 이를 통해, Material Function 수정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917172530.png">
- 수정한 Material Function 적용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917172603.png">

##### 74강 : 번형 매크로
- Macro Variation : 기존의 Tiling에 더욱 변형을 추가해주는 기법
- Starter Content의 Metal Material에서 쉽게 찾을 수 있음. -> 이를 통해 MF 생성
- 노드
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917174956.png">
- 기존의 MF에 추가(Static Switch 사용 주목)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917175030.png">

##### 75강 : 랜드스케이프 내 Specular
- Landscape Material의 퀄리티를 높이기 위해 Specular 설정을 추가(플라스틱 같은 느낌을 제거)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917193419.png">

##### 76강 : 랜드스케이프 내 Normal
- Landscape Material의 퀄리티를 높이기 위해 Normal 설정을 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917200432.png">
- 공통된 입력값이 여러 곳에서 쓰일 시 Named Reroute를 통해 관리

##### 77강 : 랜드스케이프 내 ORD
- Landscape Material의 퀄리티를 높이기 위해 ORD 설정을 추가<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917203253.png">
- 예상한대로 Constant4Vector로 4개의 변수 동시 설정 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917203339.png">

##### 79강 : Specular 및 변형 매크로 제어
- Specular 강도 제어 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917221638.png">
- Macro Variation 강도 추가
- MF에서 꺼낸 후 Material에 직접 추가/이를 위해 GetMaterial Attribute 활용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917221708.png">
##### 80강 : 랜드스케이프 레이어 블렌드
- 랜드스케이프는 보통 여러 가지의 레이어(머터리얼)로 구성
- 레이어를 여러 개 만드는 법은 단순한 복사
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917223849.png">
- 이를 연결하기 위해서는 Landscape Blend 노드 필요
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917223906.png">
- 연결 후 Landscape Mode의 Paint로 가서 Layer 확인
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240917223931.png">
- 이때, Layer가 뜨지 않을 경우 MI로 들어가서 Texture 초기화후 재할당
#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 81강 : 가이아로 랜드스케이프 만들기
- Landscape Blend 과정에서 경계선이 너무 잘 보인다면 Macro Variation의 Texture Sample의 Mip Bias 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922165846.png">
- Gaea 프로그램을 통해 간단하게 랜드스케이프 모형 생성 가능
- 다음과 같이 노드를 통해 맵 생성 후 편집 노드로 상세 조절, Combine 노드로 지형 혼합
- 노드 선택 시 미리보기 가능, 이때 노드 하나에 미리보기 고정시키고 싶으면 F키로 Pin 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922165515.png">

##### 82강 : 가이아에서 랜드스케이프 출력하기
- 다음과 같이 Mark For Export 후 Build 실행
- 첫 번째는 Height, Flow맵, 두 번째는 Slop맵이 될 것
- 이때 Build 형식은 PNG64, 해상도 크기는 1024 이하가 되도록 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922172835.png">

##### 83강 : 가이아에서 랜드스케이프 불러오기
- Height Map의 경우 Landscape Mode의 Mange->New->Import From File을 통해 불러오기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922173323.png">
- Landscape Mode->Manage->Import->Layer에서 특정 Map에 특정 Material 할당 가능(사진은 Flow Map에 Soil Material을 할당한 모습)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922175319.png">

##### 86강 : 경사 마스크 생성하기
- 경사마스크 생성하기
- Dot을 이용해서 VertexNormal이 Z축 방향에서 틀어진 정도를 계산
- Power를 통해 강도, CheapContrast를 통해 경계선을 조정
- Saturate로 1~-1 범위를 1~0으로 바꾼 후 1-x를 통해 반전
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922210206.png">

##### 87강 : 랜드스케이프 머터리얼에서 경사 마스크 사용하기
- Material Function 제작 : 2개의 머터리얼 블렌드를 위해 BlendMaterialAttributes 노드 사용
- 이때, Alpha값은 위에 제작한 Mask 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922212235.png">
- AutoLandscape Material 적용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922212340.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922212346.png">

##### 89강 : Triplanar 프로젝션 (세 개의 다른 이미지를 투사)
- 기존의 늘어남 문제를 해결하기 위해 UV Tile 사용(한 방향 투사) -> 평평하지 않은 곳에서 늘어남 발생
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922215406.png">
- 이를 해겨하기 위한 3방향 투사 기법 Triplanar 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922215448.png">
- 강의에서 제공된 Triplanar Material Function 사용(원래는 WorldAlignedTexture)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922215550.png">

##### 90강 : 경사 레이어를 위해 Triplanar 프로젝션 사용하기
- 기존의 Landscape Material Function에서 TextureBombing 함수를 Triplanar로 대체
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240922222208.png">
#### Unreal Engine 5: 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 92강 : 높이 마스크 생성하기
- 높이에 따른 변화를 주기 위한 Height Mask 생성(ex. 산 정상 눈 머터리얼)
- Absolute World Position 노드를 사용하여 높이 정보 불러오기
- Subtract를 통해 높이 조절
- Divide를 통해 FallOff 조절
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240923145755.png">
- 결과 예시
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240923145922.png">
##### 93강 : 랜드스케이프 머터리얼에서 높이 마스크 사용하기
- 앞서 만든 Height Mask를 통해 material function 생성 및 사용
- 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001172250.png">
- 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001172216.png">

##### 94강 : 높이 마스크 추가 조정
- 높이 마스크에서 경계 부분에 무작위성을 추가하기 위해 Slope Mask 활용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001172812.png">
- Before
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001172900.png">
- After
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001173211.png">
- 이를 실제 적용(Material Function 수정)
- 출력 값을 Mask->Material로 변경(이때, Mask는 Saturate가 필수 0-1값)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001175413.png">
- Landscape Material 수정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001175534.png">

##### 95강 : 높이 마스크와 경사 레이어 병행
- Scale Issue : 높이에 따라 Texture Scale 문제 발생(낮은 곳을 맞췄더니 높은 곳에서 Tiling 발생 등)
- 해결법 : 높은 곳에는 Triplanar, 낮은 곳에는 Texture Bombing 적용 -> 이를 위해 Height Blend-Blend Material Attribute 사용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001214451.png">
#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 97강 : 실시간 가상 텍스처(RVT)
- RVT : Landscape 머터리얼의 전체 머터리얼 결과를 Cache 하는 것
- RVT 장점 :
	1. Shader Complexity를 줄여 성능을 향상
	2. Non-Landscape Actor와 Blend 가능
- RVT 단점 : 
	1. dynamic한 것과 작동 불가
	2. ex) CameraDepthFade, Time, World Position Offset(떠있는돌 등)

##### 98강 : 실시간 가상 텍스처 구축하기
- RVT 설정
	1. Project Setting에서 RVT Support 허용
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001220028.png">
	2. Material Data의 Output을 RVT로 전달(RVT Node 사용)
		- 최종 결과 Name Reroute 이용해서 빼내기
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001220245.png">
		- 이를 통해 RVT Output 연결
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001220549.png">
	3. RVT Asset을 Landscape에 할당
		- RVT 생성
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001220923.png">
		- Landscape detail -> Virtual 검색 -> Draw In VT 를 통해 RVT 할당
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001220952.png">
	4. RVT Volume 버튼을 눌러 Volume 측정
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001221238.png">
		- Outliner를 통해 생성 확인
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001221300.png">
	5. 저장된 Data를 Landscaep에 다시 사용(Runtime Virtual Texture Sample 노드 사용)
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001221837.png">
		<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001222339.png">
- 전체 사용에 있어 Normal의 WorldSpcae - TangentSpace간 전환 주의
##### 99강 : 실시간 가상 텍스처 블랜드 생성하기
- 블랜드 필요 -> 마스크 필요
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001230923.png">
- A에는 원본 머터리얼, B에는 랜드스케이프 머터리얼 적용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001231418.png">
- 어떤 마스크가 필요할까?? -> 위에는 Black 아래는 White + Fall Out
- Alpha를 위해 Landscape의 Height 정보가 저장된 RVT가 새로 필요 -> RVT_Height 생성
- RVT_Height 생성 후 클릭해서 Vitual Texture content 변경
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001231100.png">
- RVT_Height를 Landscape에 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001231223.png">
- 이때 Volume 정보는 동일한 것을 사용하므로 기존의 것 복사후 이름 변경->할당 변경
- 만들어진 RVT_Height 사용해서 Mask 생성(Height Mask와 비슷함)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001232251.png">
##### 100강 : 머터리얼 내 실시간 가상 텍스처 사용하기
- Static Mesh에 적용하기 위해 Material Function 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241001233659.png">
- 적용하기 위해 해당 Static Mesh의 Material Instance -> Master Material 찾은 후 열기 이후 최종 출력에 해당 Function 넣으면 끝
#### Unreal Engine 5 : 강의 하나로 머터리얼 완벽 마스터하기  (Material 편)
##### 101강 : 자동 폴리지
- Auto Foliage가 가능한 2가지 방법과 장단점(영상에서는 첫번 째 방법 사용)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002143710.png">

##### 102강 : 랜드스케이프 그래스 타입
- LGT 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002144903.png">
- LGT 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002144923.png">
	+ Grass Mesh에서 원하는 Static Mesh 설정
	+ Grass Density로 밀도 설정
	+ Start/End Cull Distance 이용해서 Mesh가 거리에 따라 사라지게 해서 성능 향상
	+ Min LOD로 최소 LOD 설정(LOD : Level Of Detail로 거리에 따라 사용하는 triangle의 수가 달라지게 하여 성능 향상)
	+ Scale 설정을 바꿔 크기의 무작위성 추가
- LGT 사용을 위해 Node 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002145906.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002145921.png">

##### 103강 : 폴리지 마스크 생성하기
- 높이 마스크를 반전하여 낮은 곳에만 풀이 생기도록 설정
- 경사에는 풀이 자라면 안되므로 Height Mask에서 Slope Mask를 Subtract
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002155628.png">
- Material Function에서 Function Output 노드를 통해 Output 핀 추가 가능
##### 104강 : 폴리지 성능 최적화
- 성능 최적화 방법
	1. Console Command(~ 두 번 클릭 시 콘솔 창)
		r.Shadow.Virtual.NonNanite.IncludeInCoarsePages 0
		r.Shadow.Virtual.UseFarShadowCulling 0
	2. Foliage 설정 변경
		- Dynamic Shadow 끄기
		- LOD 설정 변경
		- Cull Distance 변경
		- Disable Wind 및 Move 제거(Master Material의 Time Node 연결 제거)
	3. Project Setting에서 virtual shadow map 설정 변경
	
##### 105강 : 그래스 페이드 인
- Foliage Fade Material Function 생성
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002162409.png">
	+ PerInstanceFadeAmount : Cull Distance 정보를 불러와 Mask 생성
	+ DitherTemporalAA : Mesh에 구멍을 뚫어줌
- 생성한 Function을 Master Material의 Opacity Mask 핀 연결 사이 추가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002162519.png">
- LGT에 Attribute(index)를 추가해서 다양한 요소들을 한 번에 추가 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002163733.png">
##### 106강 : 섹션 과제4 : 자동 나무
- 동일한 작업 진행
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002172056.png">
##### 107강 : 주변 환경 차단하기
- 무료 Asset인 Landscape Backgrounds 활용
- 큰 카메라 이동거리가 필요할 시 북마크 활용
	+ 북마크 설정 : Ctrl + 0~9
	+ 북마크 이동 : 0~9
##### 108강 : 후처리 작업
- 흙레이어 페인트시 그 위의 Grass, Tree도 지워지게 하기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002172909.png">
- PostProcess Volume 설정을 조정해서 다양한 분위기 연출 가능
	1. exposure : 노출
	2. ctrl+L로 라이트 각도 설정
	3. Temperature으로 색온도 조절 가능
	4. Lens Flare로 화면에 렌즈 플레어(햇빛 효과) 생성 가능
- Directional Light의 Light Shafts->Light Shafts Bloom으로 햇빛 연출 가능
##### 110강 : 섹션 마무리
- 나무 등의 LGT가 경사에서 기울어져서 올라오는 현상을 없애려면 LGT 파일 이동 후 Align to Surface 항목 비활성화
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002205930.png">
- 여러 Foliage Instance의 Detail을 수정해야할 경우 GlobalFoliageActor가 있는지 검색. 이를 통해 색상, 계절, 바람 등의 다양한 변경사항을 전체 Foliage에 동시 적용 가능
- Foliage만 따로 Paint 하고 싶을 시 Foliage Mode활용(Select에서 선택 후 Paint를 통해 그리기)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20241002210151.png">
