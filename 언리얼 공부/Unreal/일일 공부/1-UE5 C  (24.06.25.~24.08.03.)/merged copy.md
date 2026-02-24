
#### Unreal Engine 5 C++ 개발자  
##### 13강
- 피직스 
- simulate Physics : 물리 켜기
- Mass(kg) : 무게 설정
- Enable gravity : 중력 켜

##### 14강
- Object : data와 operation의 집합, 무언가를 대표하는 것
- Actor : Object
- Component : Actor를 구성하는 Object
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240625203721.png">
- 블루프린트에서 StaticMeshComponent 불러오기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240625203802.png">
- 뷰 포트에서 큐브 선택 후 블루프린트 우클릭
- Reference : 주소 참조하기

##### 15강
- Pulse : 시간에 따라 가해지는 힘
- Impulse : 즉각적인
- 힘이 가해지는 벡터 값은 '힘 = 질량 * 가속도', 'Impulse = 질량 * 속도 변화량' 참고하여 계산
- 입력 칸 안에서 사칙연산 가능
-  Vel Change 체크 시 질량 무시 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240625204958.png">

##### 16강
- Class : Object를 만드는 템플릿
- Instance : Class로 만든 Object
- Unreal에서의 Class -> 블루프린트
- 다음과 버튼으로도 생성 가능(외는 직접 생성)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240625210100.png">

##### 17강
- Spawning : 플레이 도중 Object를 생성
- Transform : Location + Rotation + Scale
#### Unreal Engine 5 C++ 개발자  
##### 18강
- Data Type : data의 모양
- Object : data와 Functionality의 집합
- Struct : 작은 Object

##### 19강
- Get Player Pawn : Pawn의 reference 가져오기
- Get Actor Location : Actor의 위치 vector

##### 20강
- Pawn과 카메라 회전은 동기화 되있지 않다. -> 카메라를 회전해도 Pawn의 Roation은 바뀌지 않음
- 이를 동기화하기 위해서는 Get Actor Rotation이 아닌, Get Control Roation 노드를 사용

##### 22강
- Get Forward Vector : 전방 벡터를 가져옴 이때 크기는 1
- Multiply와 같은 사칙 연산 노드는 핀 우클릭으로 핀 데이터 타입 변경 가능
#### Unreal Engine 5 C++ 개발자  
##### 24강
- Geometry Brush에서는 Scale로 크기 조절 X -> Brush Setting에서 크기조정
- 복사 이동할 땐 Alt + 드래그, Shift로 다중 선택가능

##### 25강
- 프로젝트에서 검색 시 Filter 활용 가능

##### 26강
- Mesh 2개를 합치고 싶을 때는 Detail 창에 드래그해서 자식 컴퍼넌트로 만들
##### 27강
- 뷰포트의 Lit을 클릭해서 뷰 모드 변경 가능
- WireFrame : 컴퓨터가 보는 세상
- Player Collision : Collision으로 보기
- Mesh 들어가서 Collision 수정 가능

##### 30강
- 블루프린트에서 여러 노드를 선택 후 우클릭 -> Collapse to function으로 함수화 가능

##### 32강
- Pure Function : Side Effect가 없는 함수(단순 값 계산)
- Side Effect : 무언가의 영향 변화를 줌
- Pure Function은 실행 핀 연결을 안하는 것이 보통

##### 33강
- 객체 지향 프로그래밍 : Function은 그것이 다루는 Data와 같은 위치에 정의되는 것이 좋음
- Member Function : Class의 함수

##### 34강
- 5초 지연 후 레벨을 다시 시작
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240627152322.png">

#### 장애물 공격 게임 제작 시작(36강 ~ 68강)
##### 38강
- 3인칭 Blueprint에서 캐릭터를 하나 생성할 때마다 Create Child로 생성하는 버릇 들이기
- <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240627161455.png">
- Parent Third Person Blueprint에서 Turn에 오류 발생 시 Turn Right로 대체

##### 43강
- 설치 순서
- Visul studio community 2022 설치(호환 확인) -> 게임 개발을 위한 C++ 체크 -> Unreal 관련 사항 체크 후 다운
- .Net 6.0(호환 확인) 설치
- Vs Code 설치(추가사항 2개 체크) -> Extension C++, Unreal Snippets 설치
- [Vs 호환 확인](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/DevelopmentSetup/VisualStudioSetup/)
- [VS 설치](https://visualstudio.microsoft.com/downloads/)
- [.NET 설치](https://dotnet.microsoft.com/ko-kr/download/dotnet?cid=getdotnetcore)
- [Vs code 설치](https://code.visualstudio.com/)
##### 44강
- Code 작성 프로그램 바꾸기 (좌측 상단 Edit -> Editor Preference -> Apperance -> Source Code)
- C++ Class를 생성했으나 보이지 않을 시 (좌측 상단 Tools -> Refresh -> Open)
- 그래도 workspace로 들어갈 수 없을 경우 저장 디렉토리의 .code-workspace를 열기
- VS code에서 컴파일 하는 법 : ctrl + shift + B 후 'win64 development build' 선택
- 에디터에서 라이브코딩 하는 법 : 다음 버튼을 클릭<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240627185326.png">

##### 46강
- 라이브 코딩으로 인한 변경 값 손실 방지 : 에디터를 닫으면 무조건 Vs code에서 재컴파일

##### 48강
- Struct나 Class는 초기값 설정 시 Constructor(생성자)를 통해 초기화
- Vector의 Type명은 FVector로 이는 구조체
- 선언 -> FVector MyVector = FVector(1, 2, 3);
- 호출 -> FVector.X, FVector.Y, FVector.Z

##### 49강
- Detail 패널의 값 우클릭으로 간편하게 복사 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240627192553.png">

##### 52강
- Pseudo code(의사 코드) : Comment등으로 작성되는 코드에 대한 설명

#### Unreal Engine 5 C++ 개발자  
##### 53강
- GetActorLocation()으로 현재 위치 가져오기 가능(반환값은 FVector)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628124138.png">

##### 54강
- Vector값에 변화를 줘 Actor를 이동시킬 경우 직접적인 값 연산보다 FVector 타입의 Velocity를 따로 선언하여 연산에 사용하는 것이 안전
- 이때 프레임률을 위해 DeltaTime을 곱해주어야함
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628124312.png">
- UPROPERTY(Category = " ")를 통해 Detail창에서의 카테고리 구분 가능

##### 55강
- 코드 작성시 Actor가 범용으로 사용될 수 있게 작성할 것(시작 위치 초기화 X)
- 코드 내부에서만 사용할 변수라면 UPROPERTY 안붙혀도 됨
- 이동한 거리 계산 법 : 현재 위치 - 시작 위치
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628125339.png">
- 편집할 필요는 없으면 UPROPERTY(VisibleAnywhere) 처리

##### 57강
 - 다음과 같이 코드 작성 시 속도가 너무 빠를 경우 원하는 StartLocation을 넘어버릴 수 있음
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628131508.png">
 - 다음과 같이 Normal Vector를 통해 정확한 도착 위치를 설정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628131808.png">

##### 58강
- 생성한 C++ Class 기반의 블루프린트 생성 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628133059.png">

##### 59강
- Actor간 충돌간에 글리치 현상 발생 시(멈춰있을 때) 가만히 있는 경우에도 Sweep(충돌 감지)를 하게 해줘서 해결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628141503.png">
##### 60강
- 원하는 장소에서 플레이 디버깅을 하고싶을 경우 뷰 포트 우클릭 후 Play Form Here로 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628142131.png">
- 이를 위해서는 Gamemode를 통해 사용할 Pawn이 설정 + Player Start 배치가 되있어야함.

##### 61강
- Log를 통한 디버깅 가능(snipchat extention 깔려 있을 시 ulog만 입력해도 가능)
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628145241.png">
 - 첫 번째 인수 : 보통 LogTemp 사용
 - 두 번째 인수 : Display, Warning, Error 3개 사용
 - 세 번째 인수 : 출력할 텍스트값 사용 변수 값 출력시 % 포맷 사용
 - 그 외 인수 : 포맷에 넘겨줄 변수들 선언 (FString 일시  *  붙여야함)
##### 62강
- GetName()으로 Actor의 이름 가져오기 가능
##### 65강
- const 함수 : 어떠한 변수의 변경도 발생하지 않는 함수 ( = 블루프린트의 pure function)
- 당연히 const 함수 내 const가 아닌 함수 호출 불가능
##### 66강
- Rotation을 Update하는 부분에서 다음과 같이 Moving을 구현한 것과 똑같이 적용하면 오류가 발생 : -90도에서 +90도로 바뀌는 현상
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628154146.png">
-  이를 위해 다음과 같은 함수를 사용
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628154216.png">

#### Crpyt Raider 게임 제작 시작(69강 ~ 111강)
##### 71강
- View Mode를 Lit -> ULit으로 바꾸면 Lighting에 의한 효과를 제거해서 볼 수 있음.
- 오른쪽 위 4분할 화면 클릭 시 다양한 측면의 화면을 볼 수 있음.
- Wireframe은 길이 재단에 용이. 좌측 상단 Perspective를 Back-Right-Top으로 바꾼 후 휠 클릭으로 길이 측정 가능.

##### 72강
- 4분할 Wireframe을 통해 다음과 같은 모듈화 배치를 정확하게 가능 (이때, 오른쪽 위 격자 이동 범위를 조정하면 더 쉬움)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628173739.png">

##### 73강
- scale 조작을 통해 좌우/상하 반전 편집 가능
- 뷰포트에서 드래그 사용 : Ctrl + Shift + 드래그
- 폴더화 간단히 하는 법 : Wireframe 창에서 드래그 후 Shift + 클릭으로 추가/ Ctrl + 클릭으로 제거 -> Outliner에서 우클릭 후 Move to로 폴더화
- 폴더화가 제대로 됐는지 확인하기 위해서 폴더 옆 눈 버튼을 클릭해서 놓친 것이 없나 확인

##### 75강
- Lighting 종류
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628190445.png">
- Directional Light : 태양광 구현
- Point Light : 퍼져나가는 광원
- Spot Light : 스포트라이트 효과-방향성이 있는 광원
- Rect Light : 방향성을 가지나 한 면에 비추는 광원
- Sky Light : 하늘 구현
- 스카이 오브젝트는 레벨을 감싸는 아주 큰 구형태이다. 이러한 먼 거리의 오브젝트의 빛을 캡쳐하기 위해서는 Sky Light가 필요. (이후 Recapture, Directional light와의 연결)

##### 76강
- 루멘 : 5에 새로 도입된 빛 처리 알고리즘
- 구식에서 만들어진 Material의 경우 루멘을 고려하지 않아 빛 처리가 의도치 않게 진행되는 경우 발생
- 특히, Inst의 경우 임시 Material 느낌(랜더링 처리가 빠져있음)
- Material에 빛의 반사가 이상(일거나)할 경우 사용하는 머터리얼(혹은 Parent)로 가서 Pixel Depth Offset 연결 해제
- Mobility 3가지
	- Static : 어떤 식으로든 움직이거나 변할 수 없음
	- Stationary : 움직일 순 없으나 변할 순 있음
	- Movable : 모두 가능
- 빛이 새는 것을 막는 작업 시 모든 조명을 Movable로 바꾸고 작업하길 추천
- 이후 추가 Object를 통해 빛 차단하기

##### 77강
- 그림자 생성을 위해선 Light에 cast shadow 설정
- 일부 객체에서 shadow 없애고 싶을 시, 설정에서 Static shadow, Dynamic shadow 해제
- Attenuation Radius로 범위 조절 가능(작게 하면 그림자 연산 줄어들어서 성능 증가)
- Intencity로 세기 조절 가능
- 해당 Instance의 변경을 Blueprint에 적용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240628203006.png">
#### Unreal Engine 5 C++ 개발자  
##### 78강
- Inheritance : 상위 클래스에 중복 로직을 구현해두고 이를 물려받아 코드를 재사용하는 방법(Is-a)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630143937.png">
- Composition : 다른객체의 인스턴스를 자신의 인스턴스 변수로 포함해서 메서드를 호출(has-a)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630144433.png"> 

##### 79강
- Component 생성법
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630145237.png">
##### 81강
- 다음과 같이 Owner의 함수 호출 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630151037.png">

##### 82강
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630151525.png">

##### 83강
- Bool에 따라 벽을 움직이는 코드 구현(VInterpConstantTo 사용이 핵심)
- Actor가 움직이지 않을 시 Mobility가 Static이 아닌가 확인
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630153909.png">

##### 84강
- 씬 컴포넌트 : 다른 Scene에 Attatch할 수 있어서 Transform값을 동기화할 수 있음.
- 카메라를 따라가기 위해서는 Character의 카메라에 Attatch

##### 85강
- 물체 인식(트레이스) 대표적인 방식 2가지
- Line Trace
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630155653.png">
- Shape Trace
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630155706.png">
- Trace Channel : 특정 물체만 잡고 싶거나 복잡한 Trace 로직 구현시
- Block, Ingnore은 해당 트레이스에서 막을거냐(인식), 무시할꺼냐(통과)를 물음
- 생성한 Channel이 안나올시 프로젝트 재시작

##### 86강
- UWorld : 최상위 Object 이를 통해 Trace함수 호출 가
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630160816.png">
```C++ 
//다음과 같은 방식으로 UWorld 사용 가능
#include "Engine/World.h"
UWorld* World = GetWorld();
UWorld-> ...
```

##### 87강
- Trace가 올바로 작동하는지 확인하기 위한 DrawDebugLine 사용
```C++ 
#include "DrawDebugHelpers.h"
FVector Start = GetComponentLocation();
FVector End = Start + GetForwardVector() * MaxGrabDistance;
DrawDebugLine(GetWorld(), Start, End, FColor::Red);
```

##### 88강
- Pointer와 Reference

|        |        포인터        |        참조        |
| :----: | :---------------: | :--------------: |
|   저장   |        주소         |        주소        |
| 주소 재할당 |        가능         |       불가능        |
|  Null  |       저장 가능       |      저장 불가능      |
|  값 접근  |     *ActorPtr     |     ActorRef     |
| 주소 접근  |     ActorPtr      |    &ActorRef     |
|  값 변경  | *ActorPtr = Actor | ActorRef = Actor |

##### 89강
- Reference의 가장 큰 사용점은 함수에서의 매개변수
- Reference 사용시 매개변수의 복사본을 만들지 않음.
- 하지만 원본 Update의 위험성이 있기 때문에 const로 제한
```C++ 
void PrintDamage(const float& Damage);
```
- Out Parameter : 의도적으로 함수 안에서 변수 값을 Update
- Out Parameter라는 증거
	- 초기화되지 않은 변수가 다음 줄에 바로 함수로 넘겨짐
	- 함수명이 'Out-'으로 시작
	- 함수의 Parameter가 const가 없는 Reference만 사용(아래 예시)
```C++ 
bool HasDamage(float& OutDamage)
{
	OutDamage = 5;
	return true;
}
```

##### 90강
- Sweep 사용
```C++ 
FCollisionShape Sphere = FCollisionShape::MakeSphere(GrabRadius);
FHitResult HitResult;

bool HasHit = GetWorld()->SweepSingleByChannel(
	HitResult, //Hit 결과
	Start, //시작
	End, //끝
	FQuat::Identity, //회전량(여기서는 0으로 설정)
	ECC_GameTraceChannel2, // Trace채널(config\DefaultEngine들어가서 Crtl + F찾기)
	Sphere // 모양
	);
	
if(HasHit){
	AActor* HitActor = HitResult.GetActor();
	UE_LOG(LogTemp, Display, TEXT("Hit : %s"), *HitActor->GetActorNameOrLabel());
	}
else{
	UE_LOG(LogTemp, Display, TEXT("Hit : no actor hit"));
}
```

##### 91강
- Enhanced Input 사용
- Input Action와 Input Mapping Context 생성
- Player Blueprint에 다음과 같은 노드 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630184213.png">

##### 93강
- Trace Preset 수정 : Collision Preset 검색 후 Custom으로 바꾸고 확장
- C++ 함수 블루프린트로 불러오기
```C++
//.h구현
UFUNCTION(BlueprintCallable)
void Grab();

UFUNCTION(BlueprintCallable)
void Release();
```
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240630190624.png">

##### 94강
- 상위 Actor에서 다른 Component 가져오는법(FindComponentByClass<>사용)
```C++
찾고자하는타입* FindComponent = GetOwner()->FindComponentByClass<찾고자하는타입>();
//포인트에 null값 저장 시 오류발생 예외처리 필수
if(FindComponent == nullptr){
    return
}
```

##### 95강
- 게임에서 물체를 잡을 경우 잡는 위치도 중요
- 이때 HitResult에서 Impact Point를 쓸 건지 Location을 쓸 건지 구분해야함.(보통 ImpactPoint가 맞음)
- 이를 위해 Debug Sphere를 그려서 판단
```C++
DrawDebugSphere(
	GetWorld(),   //UWorld Object 
	Location,     //구가 그려질 위치
	10,           //반지름
	10,           //구체에 들어갈 조각 개수
	FColor::Blue, //색깔
	false,        //지속(true시 안사라짐)
	5             //지속 시간
)
```

##### 96강
- 물건 잡기(PhysicsHandle의 GrabComponentAtLocationWithRotation)
```C++
//Grab함수 속 HasHIt인 경우
PhysicsHandle->GrabComponentAtLocationWithRotation(
	HitResult.GetComponent(),   //잡은 물체(UPrimitiveComponent)
	NAME_None,                  //Bone의 이름(특정한 Bone으로 잡을 시)
	HitResult.ImpactPoint,      //잡은 위치
	HitResult.GetComponent()->GetComponentRotation()  //잡은 물체의 Rotation 값
);
```



#### Unreal Engine 5 C++ 개발자  
##### 97강
- Physics는 일정 이상 쓰지 않으면 sleep 상태로 빠짐. 이로인해 물건 잡기가 안되는 경우가 발생.
- Primitive Component는 Scene Component로 물리 시뮬레이션을 수행
- 다음과 같은 코드로 Trace에 인식된 액터의 Physics 활성화 가능
```c++
UPrimitiveComponent* HitComponent = HitResult.GetComponent();
HitComponent->WakeAllRigidBodies();
```
- Release 함수
```c++
if (PhysicsHandle->GetGrabbedComponent() != nullptr)
{
    PhysicsHandle->ReleaseComponent();
}
```
#### Unreal Engine 5 C++ 개발자  
##### 99강
- Overlap 이벤트 설정 시 아래와 같이 Generate Overlap Event 활설화 후 Preset 설정
- 이때 Generate Overlap Event는 사물 2개 모두 켜져있어야 사물 간 이벤트 발생

<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240713171714.png">
- 블루프린트를 통해 Trigger(자체 C++ 코드), Collision 생성 후 범위 지정
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240713171859.png">
- 해당 트리거를 통해 이벤트 노드에  On Component Begin Overlap 생성(찾아도 안나올시 좌측 탭에서 해당 트리거 클릭 후 우클릭 해보자.)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240713172009.png">

##### 100강
- Component 생성 시 Tick이 활성화 되있지 않을 수 있음(최적화 때문)\
- 이에 생성자 함수를 추가해 다음 코드를 넣어 활성화
```C++
PrimaryComponentTick.bCanEverTick = true;
```
- + Actor의 경우에는 Tick이 디폴트로 활성화되있음.
##### 101강
- Overlap되는 물체들 인식같이 변수의 갯수가 가변적일때는 TArray 사용. 아래는 TArray를 사용한 Overlap함수 인식 예제
- GetOverlappingActors함수는 반환값이 없고, 인수로 전달한 TArray를 레퍼런스로 가져가 함수 내 변경으로 구현.
```C++
TArray<AActor*> Actors;
GetOverlappingActors(Actors);
```

#### Unreal Engine 5 C++ 개발자  
##### 103강
- for each 가능
```c++
for (AActor* Actor : Actors)
    {
        FString ActorName = Actor->GetActorNameOrLabel();
        UE_LOG(LogTemp, Display, TEXT("%s"), *ActorName);
    }
```

##### 104강
- 특정 Actor에만 반응하도록 하기 위해 Tag 사용 가능
- Actor의 Tag는 에디터 디테일 패널에서 추가가능
- 사용은 아래와 같은 코드들로 사용
```c++
//.h
private :
	UPROPERTY(EditAnywhere)
	FName TagName;
//.cpp
Actor->ActorHasTag(TagName);
```

##### 105강
- Trigger를 통한 Mover 작동 시 다음과 같은 코딩이 편함
```C++
void UTriggerComponent::SetMover(UMover* NewMover)
{
    Mover = NewMover;
}
```

#### Unreal Engine 5 C++ 개발자  
##### 107강
- Actor를 다른 Actor에 붙이기 위해서는 SetSimulatePhysics 함수를 통해 물리적인 효과를 비활성화 후 AttachToComponent를 사용
```c++
if(Actor != nullptr)
{
	UPrimitiveComponent* Component 
	= Cast<UPrimitiveComponent>(Actor->GetRootComponent());
    if(Component != nullptr)
    {
        Component->SetSimulatePhysics(false);
    }
    Actor->AttachToComponent(this, FAttachmentTransformRules::KeepWorldTransform);
    Mover->SetShouldMove(true);
    }
```

##### 108강
- 물체를 잡고 있는 동안 다른 효과 방지하기 -> 잡고 있을 때만 추가되는 Tag를 활용
- 다음은 Tag의 추가와 삭제 예시 코드
```C++
//추가
HitResult.GetActor()->Tags.Add("Grabbed");
//제거
AActor* GrabbedActor = PhysicsHandle->GetGrabbedComponent()->GetOwner();
GrabbedActor->Tags.Remove("Grabbed");
```


##### 110강
- 뒤돌 때마다 어두워지는 문제는 포스트 프로세스 문제
- 해결 법 : postprocessVolume을 생성 후 Global 폴더로 이동
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240718160932.png">
- 이동 후 맵 전체에 적용될 수 있도록 범위를 늘린 후 detail 패널에서 Metering Mode 활성화후 Auto Exposure Histogram -> Auto Exposure Basic으로 변경
- Trigger와 Mover가 각기 다른 Actor의 Component일 시 Level 블루프린터에서 연결 가능
- 다음은 Grab한 Actor를 다시 활성화하는 코드
```C++
HitComponent->SetSimulatePhysics(true);
HitComponent->WakeAllRigidBodies();
AActor* HitActor = HitResult.GetActor();
HitActor->Tags.Add("Grabbed");
HitActor->DetachFromActor(FDetachmentTransformRules::KeepWorldTransform);
```
#### Unreal Engine 5 C++ 개발자  
##### 114강
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240721145600.png">

##### 115강
- 전방 선언 : .h에서 다른 include를 불러오는 것은 상속 과정에서 코드가 쓸데 없이 증가하는 문제가 발생한다. 이에 .h에는 전방 선언을 사용 후 실제로 세부 구현이 이뤄지는 .cpp에서 include를 진행
```C++
private :
    UPROPERTY()
    class UCapsuleComponent* CapsuleComp; //전방선언
```
- UStaticMeshComponent* 의 경우 기본으로 정의되어있기 때문에 전방 선언을 할 필요 없다. 오류를 잘 읽어서 판단하자.

##### 116강
- CreateDefaultSubobject<>() 함수
- <> 안에는 생성하고자하는 Type
- () 안에는 생성하고자하는 이름
- 반환값은 생성된 Object의 pointer 값
```C++
CapsuleComp = CreateDefaultSubobject<UCapsuleComponent>(TEXT("Capsule Collider"));
RootComponent = CapsuleComp; //Root Component 설정
```

##### 117강
- Attatch로 Component 붙이기
```C++
TurretMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Turret Mesh"));
TurretMesh->SetupAttachment(BaseMesh);
```

##### 120강
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240721165243.png">
##### 121강
- Component는 VisibleAnywhere 사용 추천
##### 122강
- blueprint의 부모 class 바꾸기 : class setting 클릭 후 detail 패널에서 변경
- Camera와 SpringArm은 한쌍 시야를 변경하고 싶으면 SpringArm 트랜스폼 값 변경(카메라는 조작 금지)
##### 123강
- 폰에 빙의하기 : 원하는 Instance의 Detail에서 Auto Possess Player의 설정 값을 Player 0으로 설정
##### 124강
- 만들어둔 Input C++ 내 함수에 매핑하기
```C++
void ATank::SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

    PlayerInputComponent->BindAxis(TEXT("MoveForward"), this, &ATank::Move);
}
```
#### Unreal Engine 5 C++ 개발자  
##### 125강
- 물체 이동 시 Local Offset과 World Offset 구분
- Local Offset 이동 코드
```C++
void ATank::Move(float Value)
{
    FVector DeltaLocation(0.f);
    DeltaLocation.X = Value;
    AddActorLocalOffset(DeltaLocation);
    //AddActorLocalOffset의 입력값은 4개 그러나 3개가 기본값 존재
}
```

#### Unreal Engine 5 C++ 개발자  
##### 126강
- 물체 이동 시 프레임 보정 필요 -> Deltatime 활용
- Tick 외 함수에서 Deltatime 호출 필요 시 다음과 같은 함수 사용
```C++
#include "Kismet/GameplayStatics.h"
UGameplayStatics::GetWorldDeltaSeconds(this);
```

##### 127강
- AddActorLocalOffset(DeltaLocation) 의 두 번째 입력값은 bool값인 Sweep
- Sweep은 다른 물체와의 겹침을 인지하여 두
- 물체가 중첩되지 않도록 조정
- Actor의 collision이 설정되어 있어야 작동
```C++
AddActorLocalOffset(DeltaLocation, true);
```
- Local Rotate를 줄려면 AddLocalRotation을 사용
- FRotator는 Pitch, Yaw, Roll의 3가지 요소로 구성. 각각 Y, Z, X축을 기준으로 회전
```C++
void ATank::Turn(float Value)
{
    FRotator DeltaRotation = FRotator::ZeroRotator;
    DeltaRotation.Yaw = Value * TurnRate * UGameplayStatics::GetWorldDeltaSeconds(this);
    AddActorLocalRotation(DeltaRotation, true);
}
```

##### 128강
- AplayerController는 Pawn에 할당되는 Controller
- 코드에서는 APawn::GetController로 불러오며 이를 변수에 할당하여야 사용가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240724152227.png">
- 다만 GetController()로 반환되는 값은 AController이다.
- 하위 항목인 APlyaerController에 상위 항목인 AController를 저장할 순 없음 -> Cast 사용
```C++
PlayerControllerRef = Cast<APlayerController>(GetController());
```

##### 129강
- GetHitResultUnderCursor(TraceChannel, bTraceComplex, HitResult)
- 항상 포인터를 사용 전에는 포인터가 null인지 확인 필요
```C++
    if(PlayerControllerRef)
    {
        FHitResult HitResult;
        PlayerControllerRef->GetHitResultUnderCursor(
            ECollisionChannel::ECC_Visibility,
            false,
            HitResult
            );
        DrawDebugSphere(
            GetWorld(),
            HitResult.ImpactPoint,
            25.,
            12,
            FColor::Red,
            false,
            -1.f
        );
    }
```
#### Unreal Engine 5 C++ 개발자  
##### 130강
- 원하는 방향을 입력값으로 받아 회전시키는 함수
- 라인 트레이스를 블록할 보이지 않는 물체 필요시 Block Volume 생성 후 Collision에서 Visibility를 Block으로 설
```C++
void ABasePawn::RotateTurret(FVector LookAtTarget)
{
    FVector ToTarget = LookAtTarget - TurretMesh->GetComponentLocation();
    FRotator LookAtRotation = FRotator(0.f, ToTarget.Rotation().Yaw, 0.f);
    TurretMesh->SetWorldRotation(
        FMath::RInterpTo(
            TurretMesh->GetComponentRotation(),
            LookAtRotation,
            UGameplayStatics::GetWorldDeltaSeconds(this),
            25.f
        )
    );
}
```


##### 131강
- 두 물체간 거리를 구할 때는 간편하게 Dist함수 사용
```C++
float Distance = FVector::Dist(GetActorLocation(), Tank->GetActorLocation());
```
- C++ 변수를 에디터에선 변경하고 싶으나 모든 액터가 같아야할 때는 EditAnywhere보다는 EditDefaultsOnly 설정

##### 132강
- 동작 매핑은 BindAction 사용
- BindAxis에 비해 Enum 열거형 인자 하나 추가됨(IE_Pressed, IE_Released)
```C++
PlayerInputComponent->BindAction(TEXT("Fire"), IE_Pressed, this, &ATank::Fire);
```

##### 133강
- 타이머 사용하기
```C++
// .h
FTimerHandle FireRateTimerHandle;
float FireRate = 2.f;
void CheckFireCondition();

// .cpp | BeginPlay()
	#include "TimerManager.h"

   GetWorldTimerManager().SetTimer(
	FireRateTimerHandle, //TimerHandle, 따로 초기화 할 필요는 없음.
	this, //콜백 함수가 위치한 클래스
	&ATower::CheckFireCondition, //콜백 함수
    FireRate, //타이머 시간
    true); //반복여
```
#### Unreal Engine 5 C++ 개발자  
##### 135강
- TSubclassOf<>는 <>안의 타입을 UClass 형태로 저장하게 도와줌.
- UClass는 블루프린트와 C++ 사이 연동인 리플렉션 시스템 활용에 사용
```C++
    UPROPERTY(EditDefaultsOnly, Category = "Combat")
    class UStaticMeshComponent* ProjectileMesh;
```

- 그럼 TSubclassOf는 왜 필요한가? : SpawnActor의 첫 번째 전달값이 UClass, C++로는 전달하기 어려운 정보들(Static Mesh 설정)을 블루프린트로 전달
- SpawnActor<>(UClass, 위치, 회전)는 UWorld의 함수
```C++
GetWorld()->SpawnActor<AProjectile>(
        ProjectileClass,
        ProjectileSpawnPoint->GetComponentLocation(),
        ProjectileSpawnPoint->GetComponentRotation()
    );
```

##### 137강
- UPrimitiveComponent에는 충돌 관련 함수들이 정의되어 있음(아래 상속된 타입들도 동일)
- Hit Event는 Multicast Delegate로 한 번 발생하면 여러 함수에 전달
- 이때 전달 받는 함수들의 집합을 Invocation list라하고 전달하는 과정을 Broadcast라 함
- Invocation list에 사용자 정의 함수를 추가하는 법
```C++
//.h
UFUNCTION() //UFUNCTION 필수
void OnHit(UPrimitiveComponent* HitComp, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit);
//.cpp | BeginPlay()
ProjectileMesh->OnComponentHit.AddDynamic(this, &AProjectile::OnHit);
```
- 이때 함수 입력값은 최대한 자세하기 설정

##### 138강
- UActorComponent : No Transform, No attachment
- USceneComponent : Has Transform, Has Attachment
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240726164557.png">
```C++
//Create a callback
// .h | private:
UFUNCTION()
void DamageTaken(AActor* DamagedActor, float Damage, const UDamageType* DamageType, class AController* Instigator, AAcotr* DamageCauser);
//Bind it to the delegate
// .cpp | BeginPlay()
GetOwner()->OnTakeAnyDamage.AddDynamic(this, &UHealthComponent::DamageTaken);
```

##### 140강
- AGameModeBase : 게임 규칙, 종료 조건(승리, 패배)
- AGameMode : 멀티 플레

##### 141강
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240726201817.png">
- HandleDestruction 구현
```C++
// in Tower
void ATower::HandleDestruction()
{
    Super::HandleDestruction();
    Destroy();
}
//in Tank
//Tank는 User가 사용하는 pawn이므로 Destroy()가 아닌 조작 불가로 만듦
//조작 불가 -> 숨기기/Tick 비활성화/Controller 비활성화
void ATank::HandleDestruction()
{
    Super::HandleDestruction();
    SetActorHiddenInGame(true);
    SetActorTickEnabled(false);
}
```
- ActorDied 구현
```c++
void AToonTanksGameMode::ActorDied(AActor *DeadActor)
{
    if (DeadActor == Tank)
    {
        Tank->HandleDestruction();
        if (Tank->GetTankPlayerController())
        {
            Tank->DisableInput(Tank->GetTankPlayerController());
            Tank->GetTankPlayerController()->bShowMouseCursor = false;
        }
    }
    else if (ATower* DestroyedTower = Cast<ATower>(DeadActor))
    {
        DestroyedTower->HandleDestruction();
    }
}
void AToonTanksGameMode::BeginPlay()
{
    Super::BeginPlay();
    Tank = Cast<ATank>(UGameplayStatics::GetPlayerPawn(this, 0));
}
```
- DamageTaken에서 Actor Died 호출하기
```c++
// GameMode 불러오기
ToonTanksGameMode = Cast<AToonTanksGameMode>(UGameplayStatics::GetGameMode(this));
// 함수 호출
if (Health <= 0.f && ToonTanksGameMode)
	{
		ToonTanksGameMode->ActorDied(DamagedActor);
	}
```
- 변수 이름 변경 시 ***F2*** 사용하면 사용된 모든 코드 위치에서 변경 적용

##### 142강
- 사용자 지정 플레이어 컨트롤러 생성
```C++
void AToonTanksPlayerController::SetPlayerEnabledState(bool bPlayerEnabled)
{
    if (bPlayerEnabled)
	{
	//GetPawn이 안될 시 #include "GameFramework/Pawn.h"
       GetPawn()->EnableInput(this);
    }
    else
    {
        GetPawn()->DisableInput(this);
    }
    bShowMouseCursor = bPlayerEnabled;
}
```

##### 143강
- SetTimer에서 Callback 함수에 입력값이 필요할 시 Delegate를 사용
```C++
if(ToonTanksPlayerController)
    {
        ToonTanksPlayerController->SetPlayerEnabledState(false);
        
        FTimerHandle PlayerEnableTimerHandle;
        FTimerDelegate PlayerEnableTimerDelegate = FTimerDelegate::CreateUObject(
            ToonTanksPlayerController, //부를 함수가 있는 위치
            &AToonTanksPlayerController::SetPlayerEnabledState, //부를 함수
            true // 전달 값
        );
        GetWorldTimerManager().SetTimer(
            PlayerEnableTimerHandle, //타이머 핸들
            PlayerEnableTimerDelegate, //타이머 delegate
            StartDelay, //딜레이 시간
            false // 반복
        );
    }
```
#### Unreal Engine 5 C++ 개발자  
##### 144강
- UFUNCTION(BlueprintImplementableEvent) 시 C++에서 정의할 필요 없이 블루프린트에서 구현 가능
- Widget BluePrint에서 Text나 Button같은 요소를 두기 위해서는 먼저 Canvas Pannel을 사용
- Widget을 화면상에 보이기 위해서는 블루프린트 노드 Create Widget -> Add Viewport 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240727140833.png">

##### 145강
- 카운트다운 처리 시 간단하게 Switch 사용 가능


##### 146강
- Widget 요소에서 Is Variable 활성화 시 Graph에서 변수로 사용 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240727142509.png">
- 변수로 만들 시 다음과 같이 Text 내용 변경 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240727142616.png">
- 더이상 위젯이 필요 없는 경우 다음 노드로 삭제 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240727142644.png">

##### 147강
- 필드 내 특정 Actor의 갯수가 알고 싶을 시 :  UGameplayStatics::GetAllActorsOfClass를 사용하여 특정 Actor들의 포인터 배열을 생성 후 .NUM()을 사용하여 배열의 크기로 알아내기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240727143850.png">
```C++
int32 AToonTanksGameMode::GetTargetTowerCount()
{
    TArray<AActor*> Towers;
    UGameplayStatics::GetAllActorsOfClass(this, ATower::StaticClass(), Towers);
    return Towers.Num();
}
```

##### 148강
- True/False에 따라 다른 값이 필요할 시 Branch 노드도 유용하지만, Select도 편리
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240727144347.png">

##### 149강
-  파티클 다루기
```C++
//.h | private | 파티클 정의
UPROPERTY(EditAnywhere, Category = "Combat")
class UParticleSystem* HitParticles;

//.cpp | 파티클 생성
UGameplayStatics::SpawnEmitterAtLocation(
	this, 
	HitParticles, 
	GetActorLocation(), 
	GetActorRotation()
);
```

##### 150강
- 파티클을 컴포넌트로 만들어서 사용 가능( 물체를 따라다니거나, 지속적으로 작용하는 파티클의 경우 )
```C++
//.h | private | 파티클 컴퍼넌트 정의
UPROPERTY(VisibleAnywhere, Category = "Combat")
class UParticleSystemComponent* TrailParticles;

//.cpp | 파티클 컴퍼넌트 생성 및 부착
TrailParticles = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("Smoke Trail"));
TrailParticles->SetupAttachment(RootComponent);
```

##### 152강
- 사운드의 경우 파티클과 매우 유사
```C++
//.h | private | 사운드 생성
UPROPERTY(EditAnywhere, Category = "Combat")
class USoundBase *LaunchSound;

//.cpp | 사운드 재생
UGameplayStatics::PlaySoundAtLocation(this, HitSound, GetActorLocation());
  ```

##### 153강
- CameraShake 추가
- 1. CameraShake 블루 프린트 생성
- 2. 코드 추가
```C++
//.h | private | 쉐이크 생성
UPROPERTY(EditAnywhere, Category = "Combat")
TSubclassOf<class UCameraShake> HitCameraShakeClass;

//.cpp | 쉐이 재생
GetWorld()->GetFirstPlayerController()->ClientPlayCameraShake(HitCameraShakeClass);
  ```
##### 154강
- SprintArm의 Camera Lag 설정을 변경하여 카메라 무빙을 좀 더 부드롭게 변경 가능(선택 사항)
#### Unreal Engine 5 C++ 개발자  
##### 159강
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728141630.png">
- Controller를 통한 조작 시 DeltaTime을 통한 계산 필수

##### 160강
- 카메라 세부적인 위치 조정은 스프링암의 Offset 조절
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728143007.png">
- 카메라가 회전을 따라오지 않는다면 detail 체크
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728145806.png">

##### 162강
- 콜리전 오류 발생 시 에디터의 View 모드를 바꿔서 확인 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728150224.png">
- 이후 해당 Actor 클릭 후 Mesh로 이동해서 Collision 편리

##### 163강
- 애니메이션 블루프린터에서는 Blend 함수를 통해 두 애니메이션간 혼합 가능
- 하지만 이는 이동 애니메이션과는 적합하지 않음
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728160649.png">


##### 164강
- 애니메이션간 적절한 혼합-변환을 위해서는 Blend Space 기능 활용
- 다음과 같이 설정 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728160623.png">
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728160635.png">
##### 165강
- 만들어진 Blend Space는 다음과 같이 Animation Blueprint에서 사용 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728161348.png">
- 이때 Angle과 Speed와 같이 애니메이션을 결정 짓는 입력값들은 Animation Blueprint Event Graph에서 설정 가능. 다음은 Speed를 설정한 모습
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728161513.png">

##### 166강
- 각도 계산은 로컬 트랜스폼에서 진행되어야함. 이를 포함한 계산 식
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728164146.png">

##### 167강
- 발미끄러짐 현상을 최소화하기 위해서는 애니메이션 속도 계산 필요
- 애니메이션을 재생 후 다음 공식 적용
- 속도 = (발 떨어지는 y값 - 발 붙은 y값)/(발 떨어지는 시간 - 발 붙은 시간)으로 계산
- 이후 이 값을 BlendSpace에 적용

##### 169강
- 한 C++ 클래스에서 다른 클래스 Actor Spawn하기
```C++
//.h | public
UPROPERTY(EditDefaultsOnly)
TSubclassOf<AGun> GunClass;

UPROPERTY()
AGun* Gun;
//.cpp | BeginPlay()
Gun = GetWorld()->SpawnActor<AGun>(GunClass);
```

##### 170강
- Socket을 통한 Mesh 부착하기
- 1. Socket 만들기 : Skeletal 설정에 가서 Add Socket 사용용
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240728190050.png">
- 2. 코드를 통해 캐릭터에 해당 Mesh 부착
```C++
//기존에 있던 총 숨기기
GetMesh()->HideBoneByName(TEXT("weapon_r"), EPhysBodyOp::PBO_None);
//Mesh 부착
Gun->AttachToComponent(GetMesh(), FAttachmentTransformRules::KeepRelativeTransform, TEXT("WeaponSocket"));
//이후 처리를 위해 Owner로 설
Gun->SetOwner(this);
```

##### 174강
- LineByTrace를 위해서는 Collision 세팅에서 Trace Channel을 추가 -> 이때 Preset에서 필요한 수정 필요(OverlapAll, BlockAll, IgnoreAll, Invisible---)
- 추가 코드
```C++
FVector End = Location + Rotation.Vector() * MaxRange;
FHitResult Hit;
bool bSuccess = GetWorld()->LineTraceSingleByChannel(Hit, Location, End, ECollisionChannel::ECC_GameTraceChannel1);
if (bSuccess)
{
    DrawDebugPoint(GetWorld(), Hit.Location, 20, FColor::Red, true);
}
```

##### 175강
- 파티클이 반대로 튀는 경우(총을 쏘고 맞추는 위치에서 발생 시) 다음과 같은 코드 활용 가능
```C++
FVector ShotDirection = -Rotation.Vector();
UGameplayStatics::SpawnEmitterAtLocation(GetWorld(), ImpactEffect, Hit.Location, ShotDirection.Rotation());
```

##### 176강
- float TakeDamage 함수
```C++
float TakeDamage (
float Damage , //데미지량
struct FRadialDamageEvent const& RadialDamageEvent, //데미지의 타입, 설명
class AController* EventInstigator, //데미지 발생시킨 주체
AActor* DamageCauser //데미지 원인(총, 수류탄)
)
```
-  FRadialDamageEvent : 수류탄 같은 데미지
-  FPointDamageEvent : 총 같은 데미지
```C++
FPointDamageEvent(
float InDamage //데미지량
struct FHitResult const& InHitInfo //타격위치 정
FVector const& InShortDirection //사격 방향
TSubclassOf<class UDamageType> InDamageTypeClass
)
```
- 실제 예시 코드
```C++
#include "Engine/DamageEvents.h"

AActor* HitActor = Hit.GetActor();
if (HitActor != nullptr)
{
	FPointDamageEvent DamageEvent(Damage, Hit, ShotDirection, nullptr);
	HitActor->TakeDamage(Damage, DamageEvent, OwnerController, this);
}
```

##### 177강
- 다이나믹 디스패치 : 효율성을 중시하는 C++에 의도적인 비효울성을 강제하는 것
- Virtual 접두사 : C++의 경우 오버라이드가 진행된 클래스 사이에서도 포인터를 통한 함수 호출 시 부모 함수를 부르는 상황 발생. 이를 방지하기 위해 Virtual을 사용 -> 오버라이드 된 함수가 있는가 검사
- Override 접미사 : 일종의 안전장치, 이 함수가 이름이 틀리진 않았는가, Virtual로 선언된 함수를 오버라이드 하고 있는가등을 검사.

##### 178강
- 데미지 받는 것을 처리하기 위해 상위 클래스의 TakeDamage 함수를 Override
```C++
float AShooterCharacter::TakeDamage(float DamageAmount, struct FDamageEvent const &DamageEvent, class AController *EventInstigator, AActor *DamageCauser) 
{
	float DamageToApply = Super::TakeDamage(DamageAmount, DamageEvent, EventInstigator, DamageCauser);
	DamageToApply = FMath::Min(Health, DamageToApply);
	Health -= DamageToApply;
	UE_LOG(LogTemp, Warning, TEXT("Health left %f"), Health);
	return DamageToApply;
}
```

##### 179강
- 애니메이션 블루프린트에서 Blend Poses by Bool을 통해 상황에 맞춘 애니메이션 선택 가능
#### Unreal Engine 5 C++ 개발자  
##### 180강
- C++ 함수를 블루프린트에서 사용하기 위해서는 BlueprintCallable사용, 순수 노드로 사용하기 위해서는 BlueprintPure 사용
- 순수함수 : 실행핀이 없으며 어떠한 변화도 일으키지 않는 함수 -> const 사용
```C++
UFUNCTION(BlueprintPure)
bool IsDead() const;
```

##### 181강
- 사용자 Custom AI Controller 적용법
- AIController 기반 C++ class 생성
- 해당 클래스 기반 블루프린트 생성
- 이후 Character BP의 Detail에서 Pawn\AI Controller Class 설정 변경
- <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802142026.png">

##### 182강
- AIController 내장 함수에는 Focus를 설정하는 함수가 3개 존재
	- SetFocalPoint(FVector, 우선순위) : 고정된 한 지점을 응시
	- SetFocus(AActor*, 우선순위) : 움직이는 물체를 지속해서 추척 응시
	- ClearFocus(우선순위) : 응시를 해제
- Foucs 인자로는 우선순위를 전달 미리 정의된 우선순위는 다음과 같음.
	- Default = 0
	- Move = 1
	- Gameplay = 2
- Pawn을 가져온 후 SetFocus를 사용하는 코드 예시
```C++
#include "Kismet/GameplayStatics.h"

void AShooterAIController::BeginPlay()
{
    Super::BeginPlay();
    APawn* PlayerPawn = UGameplayStatics::GetPlayerPawn(GetWorld(), 0);

    SetFocus(PlayerPawn);
}
```

##### 183강
- AI가 User를 쫓아오게 하기
	1. Nav Mesh를 통해 이동 가능한 구역 설정
	<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802144747.png">
	2. AIController에서 코드 작성
	```C++
	APawn *PlayerPawn = UGameplayStatics::GetPlayerPawn(GetWorld(), 0);
    MoveToActor(PlayerPawn, 200); //200은 2m 여유를 두고 접근
    //MoveToLocation도 존재
	```

##### 184강
- AI의 시야에 User(혹은 특정 사물)이 있을 경우에만 동작하게 하고 싶을 시 LightOfSightTo 함수 사용
```C++
 if (LineOfSightTo(PlayerPawn))
    {
        SetFocus(PlayerPawn);
        MoveToActor(PlayerPawn, AcceptanceRadius);
    }
 else
    {
        ClearFocus(EAIFocusPriority::Gameplay);
        StopMovement();
    }
```

##### 185강
- 위와 같이 AI의 행동 절차를 코드로 구현해도 되지만, Behavior Tree, BlackBoard를 통해 더욱 쉽게 구현 가능
	- Behavior Tree는 AI의 행동 절차를 구현
	- BlackBorad는 AI의 행동 절차에 필요한 변수를 저장하는 메모리 역할
- 코드를 통한 Behavior Tree 활성화
```C++
//.h
private:
        UPROPERTY(EditAnywhere)
        class UBehaviorTree* AIBehavior;
//.cpp | beginplay()
if (AIBehavior != nullptr)
    {
        RunBehaviorTree(AIBehavior);
    }
```

##### 186강
- C++로 블랙보드 키 설정하기(변수 추가하기)
	1. C++ 코드에 블랙보드 변수 추가
	```C++
	#include "BehaviorTree/BlackboardComponent.h`
		
	APawn *PlayerPawn = UGameplayStatics::GetPlayerPawn(GetWorld(), 0);
	
	//1번째 인자 : 저장하는 변수명
	//2번째 인자 : 저장값
	GetBlackboardComponent()->SetValueAsVector(TEXT("PlayerLocation"), PlayerPawn->GetActorLocation());
	```
	2. 블랙보드에 해당 변수명과 같은 변수 추가

##### 187강
- BlackBoard에서 설정한 값들을 이용하여 Behavior Tree 구성 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802154941.png">

##### 188강
- Behavior Tree Selector 노드 : Left to Right로 실행 단, 자식 노드중 하나라도 실행이 완료되면 종료
- Decorator : Sequence노드에 Decorator를 추가해서 Loop나, 참-거짓 등 다양한 효과 추가 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802160118.png">
- Blackboard Decorator는 특정 변수가 갱신될 때 참을 반환
- 다음은 Tree 예시 구현 : PlayerLocation이 Set-갱신되는 경우(AI가 Player를 발견) Player를 쫓음 그 외에는 Player가 마지막으로 발견된 장소에서 대
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802160334.png">
- Blackboard Deco의 경우 Observer aborts 설정 가능
	- None : 아무 효과 없음
	- Self : Chase 실행 중 조건이 거짓이 되면 하던 작업을 멈추고 Selector를 재평
	- Lower Priority : Investigate 실행 중 조건이 참이 되면 바로 Chase 실행
	- Both : 참이 되면 Chase, 거짓이 되면 Investigate를 하던 작업을 중지하고 바로 실행
- Player가 시야에 보일 시 BlackBoard 변수들을 초기화하는 코드
```C++
if (LineOfSightTo(PlayerPawn))
    {
        GetBlackboardComponent()->SetValueAsVector(TEXT("PlayerLocation"), PlayerPawn->GetActorLocation());
        GetBlackboardComponent()->SetValueAsVector(TEXT("LastKnownPlayerLocation"), PlayerPawn->GetActorLocation());
    }
    else
    {
        GetBlackboardComponent()->ClearValue(TEXT("PlayerLocation"));
    }
```

##### 189강
- 사용자 Custom Task 만들기
	1. BTTask C++ 클래스 생성
	2. 해당 클래스에서 생성자를 통해 노드 이름 설정
	```C++
	UBTTask_ClearBlackboardValue::UBTTask_ClearBlackboardValue()
	{
	    NodeName = TEXT("Clear Blackboard Value");
	}
	```
	3. BT에서 해당 Task 호출 및 사용

##### 190강
- BTTask Node에 있어서 구현 중요성이 높은 함수들(Parent 코드의 Override들)
	1. ExecuteTask : Node 실행 시 첫 Tick에 실행되는 동작
	2. AbortTask : Node 종료 시 실행되는 동작
	3. TickTask : 첫 Tick 다음 Tick부터 지속적으로 실행되는 동작
	4. OnMessage : Node 종료 시 전달되느 메세지
- ExecuteTask를 통해 Key 삭제를 구현한 코드
```C++
`#include "BehaviorTree/BlackboardComponent.h"`

EBTNodeResult::Type UBTTask_ClearBlackboardValue::ExecuteTask(UBehaviorTreeComponent &OwnerComp, uint8 *NodeMemory)
{
    Super::ExecuteTask(OwnerComp, NodeMemory);

    OwnerComp.GetBlackboardComponent()->ClearValue(GetSelectedBlackboardKey());

    return EBTNodeResult::Succeeded;
}
```
- EBTNodeResult::Type 값으로는 4가지가 존재
	- Succeeded : 성공 처리, 진행
	- Failed : 실패 처리, 진행
	- Aborted : 실패 처리, 진행 불가
	- InProgress : 아직 안끝남


##### 191강
- Task 노드에서 Observe Blackboard Value 활성화 시 Value 값을 지속적으로 업데이
 <img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802163641.png">
 - Pawn의 함수를 사용하는 Task 생성 예시, 이때 호출하는 함수는 Public 이여야함.
```C++
#include "AIController.h"
#include "ShooterCharacter.h"
EBTNodeResult::Type UBTTask_Shoot::ExecuteTask(UBehaviorTreeComponent &OwnerComp, uint8 *NodeMemory)
{
    Super::ExecuteTask(OwnerComp, NodeMemory);

    if (OwnerComp.GetAIOwner() == nullptr)
    {
        return EBTNodeResult::Failed;
    }

    AShooterCharacter* Character = Cast<AShooterCharacter>(OwnerComp.GetAIOwner()->GetPawn());

    if (Character == nullptr)
    {
        return EBTNodeResult::Failed;
    }

    Character->Shoot();

    return EBTNodeResult::Succeeded;
}
```

##### 192강
- BT의 Service를 사용하면 AI Controller에서 하던 Value 업데이트를 따로 + 원하는 Tick 주기를 사용해서 구현 가능
- C++ BTService 종류의 Base 선택
- 아래 코드는 TickMode를 사용하여 Service 구현
```C++
void UBTService_PlayerLocationIfSeen::TickNode(UBehaviorTreeComponent &OwnerComp, uint8 *NodeMemory, float DeltaSeconds)
{
    Super::TickNode(OwnerComp, NodeMemory, DeltaSeconds);

    APawn *PlayerPawn = UGameplayStatics::GetPlayerPawn(GetWorld(), 0);

    if (PlayerPawn == nullptr) return;
    if (OwnerComp.GetAIOwner() == nullptr) return;
    
    if (OwnerComp.GetAIOwner()->LineOfSightTo(PlayerPawn))
    {
        OwnerComp.GetBlackboardComponent()->SetValueAsVector(GetSelectedBlackboardKey(), PlayerPawn->GetActorLocation());
    }
    else
    {
        OwnerComp.GetBlackboardComponent()->ClearValue(GetSelectedBlackboardKey());
    }
}
```
- Service를 추가한 모습(초록색)
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802172633.png">

##### 193강
- 총이 자기 자신을 맞추는 문제 해결
```C++
//Gun.cpp | PullTrigger()
//구조체 생성
FCollisionQueryParams Params; 
//총 자기 자신과, 총을 들고있는 ACtor를 구조체에 추가
Params.AddIgnoredActor(this);
Params.AddIgnoredActor(GetOwner());
//LineTraceSingleByChannel의 마지막에 구조체를 추가해서 무시할 목록을 전달
bool bSuccess = GetWorld()->LineTraceSingleByChannel(Hit, Location, End, ECollisionChannel::ECC_GameTraceChannel1, Params);
```
- 사망 후 계속해서 사격 + Collision이 남아있는 문제 해결
```C++
//ShooterCharacter.cpp | TakeDamage()
if (IsDead())
{
	//더이상 컨트롤 불가
	DetachFromControllerPendingDestroy();
	//Collision 비활성화
	GetCapsuleComponent()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
}
```

##### 194강
- 자체 GameMode 만든 후 다른 코드에서 해당 GameMode의 함수 호출하기
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802174009.png">
```C++
//ShooterCharacter.cpp | TakenDamage()
`#include "SimpleShooterGameModeBase.h"`
ASimpleShooterGameModeBase* GameMode = GetWorld()->GetAuthGameMode<ASimpleShooterGameModeBase>();
if (GameMode != nullptr)
{
    GameMode->PawnKilled(this);
}
```
#### Unreal Engine 5 C++ 개발자  
##### 195강
- 게임 종료 및 재시작등은 PlayerController에서 정의 이후 이를 Gamemode에 연결하여 실행 
- GameHasEnded() : PlayerController.h에 정의된 게임 종료를 알리기 위한 함수
- 입력
	- class AActor * EndGameFocus : 종료 후 뷰타겟(기본값 : nullptr)
	- bool bIsWinner : 성공이냐 실패냐 결과(기본값 : false)
```C++
APlayerController* PlayerController = Cast<APlayerController>(PawnKilled->GetController());
if (PlayerController != nullptr)
{
    PlayerController->GameHasEnded(nullptr, false);
}
```
- 게임 재시작도 내장된 함수를 통해 진행
```C++
GetWorldTimerManager().SetTimer(
	RestartTimer, 
	this, 
	&APlayerController::RestartLevel, 
	RestartDelay
);
```

##### 196강
- Widget_Blueprint에서 요소들 이동 시 Shift누르면 축에 고정된채로 이
- Widget 생성 후 추가하는 코드
```C++
//ShooterPlayerContorller.h | private
UPROPERTY(EditAnywhere)
TSubclassOf<class UUserWidget> LoseScreenClass;
//ShooterPlayerContorller.cpp | GameHasEnded()
UUserWidget* LoseScreen = CreateWidget(this, LoseScreenClass);
if (LoseScreen != nullptr)
{
    LoseScreen->AddToViewport();
}
```

##### 197강
- TActorRange<>()를 통해 월드 내 특정 클래스의 액터들을 모두 불러올 수 있음.
- 사용 예시
```C++
for (AController* Controller : TActorRange<AController>(GetWorld()))
{
    bool bIsWinner = Controller->IsPlayerController() == bIsPlayerWinner;
    Controller->GameHasEnded(Controller->GetPawn(), bIsWinner);
}
```

##### 199강
- Refactoring 예시
- 원본
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802211648.png">
- 수정
```C++
void AGun::PullTrigger()
{
    UGameplayStatics::SpawnEmitterAttached(MuzzleFlash, Mesh,TEXT("MuzzleFlashSocket"));
    FHitResult Hit;
    FVector ShotDirection;
    bool bSuccess = GunTrace(Hit, ShotDirection);
    if (bSuccess)
    {
        UGameplayStatics::SpawnEmitterAtLocation(GetWorld(), ImpactEffect, Hit.Location, ShotDirection.Rotation());
        AActor* HitActor = Hit.GetActor();
        if (HitActor != nullptr)
        {
            FPointDamageEvent DamageEvent(Damage, Hit, ShotDirection, nullptr);
            AController *OwnerController = GetOwnerController();
            HitActor->TakeDamage(Damage, DamageEvent, OwnerController, this);
        }
    }
}
```

```C++
bool AGun::GunTrace(FHitResult &Hit, FVector& ShotDirection)
{
    AController *OwnerController = GetOwnerController();
    if (OwnerController == nullptr)
        return false;
    FVector Location;
    FRotator Rotation;
    OwnerController->GetPlayerViewPoint(Location, Rotation);
    //타입명을 입력하면 지역변수가 되므로 제
    ShotDirection = -Rotation.Vector();

    FVector End = Location + Rotation.Vector() * MaxRange;
    FCollisionQueryParams Params;
    Params.AddIgnoredActor(this);
    Params.AddIgnoredActor(GetOwner());
    return GetWorld()->LineTraceSingleByChannel(Hit, Location, End, ECollisionChannel::ECC_GameTraceChannel1, Params);
}
```

```C++
AController* AGun::GetOwnerController() const
{
    APawn *OwnerPawn = Cast<APawn>(GetOwner());
    if (OwnerPawn == nullptr)
        return nullptr;
    return OwnerPawn->GetController();
}
```

##### 201강
- 사운드를 더 풍부하게 하기 위해 Sound_Cue 사용 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802213336.png">
- Random : 입력 핀의 사운드를 랜덤하게 하나 골라 재생(Detail에서 비복원/복원 설정 가능)
- Modulator : Pitch와 Volume을 랜덤하게 설정해 재생
- 여러 오디오를 한 번에 불러올 때는 Editor의 Content browser에서 다중 선택 후 Cue에서 우클릭 시 간단하게 불러오기 가능

##### 202강
- 사운드를 공간화(거리에 따른 감쇠, 좌우 스테레오 음향)을 위해서는 어테뉴에이션 설정
- Cue의 Detail 패널에서 설정 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240802220547.png">
#### Unreal Engine 5 C++ 개발자  
##### 204강
- 체력바와 같은 HUD 구현을 위해서는 progress bar를 사용
- progress bar의 percent를 bind를 통해 상태 변화 함수와 연결
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240803200700.png">
##### 205강
- 에임 오프셋 : Additive Animation으로 다른 애니메이션 위에 얹은 변형된 애니메이션이다. 이에 다른 애니메이션을 실행하면서 동시에 실행이 가능하다. 
- 해당 강의에서는 위-아래 에임 이동을 Pawn이 따라가도록 하기 위해 사용하였다.
- 아래는 유저의 회전을 계산해 Animation의 변수인 Anim_Pitch를 Set하는 예시이다.
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240803202732.png">

##### 206강
- State Machine : 여러 애니메이션간 전환을 간편하게 하기 위한 시스템.
- 아래와 같이 필요한 애니메이션들을 State로 만든뒤 연결하는 핀에서 전환 조건 검사
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240803205028.png">

##### 207강
- 다음 블루프린트 Node 'Is Falling'를 통해 현재 캐릭터가 점프중인지를 검사
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240803205548.png">
- State간 연결된 핀에서 이전 동작이 끝난 직후 바로 다음 애니메이션 재생을 원한다면(특정한 조건이 없다면) Detail 창에서 다음 설정 True
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240803205944.png">
- Blend 옵션을 통해 애니메이션간 전환을 더 부드럽게 조정 가능
<img src="https://raw.githubusercontent.com/KINGWONWOO/obsidian/main/Image/Pasted image 20240803211322.png">
- State간 중첩 가능

##### 208강
- Ambient Sound(전역 사운드)로 배경 음악 설정 가능
