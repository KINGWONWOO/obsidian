## 1일차
- 3가지의 멀티 모델 존재 : 턴제, 실시간 세션 기반, Persistent World(MMO)
- 언리얼은 실시간 세션 기반 게임 지원
- server-client 모델 지원 - 서버에서 계산된 상태만이 정확하다.
- HasAuthority()를 통해 server와 client 구별 가능
- 서버가 복제를 허용한 정보만 클라이언트가 업데이트 가능
``` C++
 if (HasAuthority()) {
	SetReplicates(true);
	SetReplicateMovement(true);
}
```
- 어떤 식으로 override 되지 않은 객체의 속성을 바꾸면 이는 server에서만 적용되는 점 주의
- NAT은 디폴트로 서버 호스팅하기가 불가능. 조인, 이메일/알림 수신은 가능
- 간단한 멀티 테스트를 위해서는 Hamachi를 이용
- A에서 B까지의 방향 벡터 == (B-A).GetSafeNormal()
- A에서 B까지의 거리 == (B-A).Size()
- 서버 host & join은 Game Instance로 진행. Game Instance는 모든 레벨에서 하나만 존재.
- 생성자는 에디터 & 플레이 시 실행. Init은 플레이 시만 실행.
- UFunction()에 Exec 매개변수를 넣음으로써 ~ 명령어와 상호작용 가능한 함수 생성 가능
- Exec 사용 가능 클래스 : PlayerControllers, Possessed Pawns, HUDs, Cheat Managers, Game Modes, Game Instances
- Exec이 사용된 함수에 매개변수를 추가하면 명령어 입력 시 전달 가능.
# 2일차
- C++ 에서 블루프린트 접속 시 다음 명령어를 사용
``` C++
	Constructorhelpers::FClassFinder<원하는 클래스> 이름(TEXT("블루프린트 위치"));
	if(!ensure(이름.Class != nullptr)) return;
```
- Widget Blueprint에 접속하기 위해서는 build.cs에서 의존성에 UMG 추가 필요. 이후, .uproject에 visual 파일 재생성 필요
- Widget을 화면에 추가하고, 마우스 입력이 가능하도록 하는 코드.(그냥 블루프린트 쓰자...)
``` C++
	UUserWidget* Menu = CreateWidget<UUserWidget>(this, MenuClass);
	if (!ensure(Menu != nullptr)) return;
	Menu->AddToViewport();

	APlayerController* PlayerController = GetFirstLocalPlayerController();
	if (!ensure(PlayerController != nullptr)) return;

	FInputModeUIOnly InputModeData;
	InputModeData.SetWidgetToFocus(Menu->TakeWidget());
	InputModeData.SetLockMouseToViewportBehavior(EMouseLockMode::DoNotLock);

	PlayerController->SetInputMode(InputModeData);

	PlayerController->bShowMouseCursor = true;
```
- MainMenu C++ 부모 파일 생성 후, 키 바인딩 시 다음과 같은 코드 사용. 이때, 변수명과 실제 버튼 이름이 같아야 자동으로 바인딩.
``` C++
//.h
protected:
	virtual bool Initialize();

private:
	UPROPERTY(meta = (BindWidget))
	class UButton* Host;

	UPROPERTY(meta = (BindWidget))
	class UButton* Join;

	UFUNCTION()
	void HostServer();
//.cpp in initialize
Host->OnClicked.AddDynamic(this, &UMainMenu::HostServer);

```
- 종속성은 compile 종속성(단방향), Runtime 종속성(양방향)이 존재. Menu를 플러그인 처럼 다양한 게임에 사용하기 위해선 MenuSystem -> GameInstance로 향하는 host/Join의 compile 종속성을 없앨 필요가 있음. 이를 위해 사용하는 것이 종속성 반전
- 종속성 반전은 Interface를 새로 생성하는 방법으로 해결. MenuSystem은 Interface에게 Compile 종속.
- Interface 생성 시 함수를 선언하되, 구현하지는 않음. 이를 위해서 pure virtual로 만들어야 함.
```C++
virtual void Host() = 0;
```
- Interface의 클래스를 2개로 나눈 이유는 다이아몬드 상속을 피하기 위해.
- Interface를 인스턴스화 할 수 없는 이유는 순수 가상 함수를 가지고 있어서

# 4일차
- 언리얼 C++ 메모리 관리는 스택과 힙을 사용
- 힙 사용 시 참조 카운팅 및 가비지 컬렉션 사용
- UObject의 경우 자동으로 가비지 컬렉션 사용 Mark and Sweep 방식 : 루트에서 도달 가능한 객체들을 Mark하고 도달 불가능하면 Sweep 진행
- Non-UObject의 경우 참조 카운팅으로 관리. (TSharedPrt'<'T'>', TSharedRef'<'T'>'와 같은 스마트 포인터 사용) 참조 카운팅이 0이 되면 자동으로 delete 호출

# 5일차
- Client와 Server간 동기화 과정에서 RPC 통신을 사용.
```C++
//.h
UFUNCTION(Server, Reliable, WithValidation)
void Server_MoveForward(float Value);
//.cpp
PlayerInputComponent->BindAxis("MoveForward", this,&AGoKart::Server_MoveForward);

void AGoKart::Server_MoveForward_Implementation(float Value)
{
	Throttle = Value;
}

bool AGoKart::Server_MoveForward_Validate(float Value)
{
	return FMath::Abs(Value) <= 1;
}
```
- Server는 모든 객체에 Authority를 보유하여 업데이트가 실시간 적용
- Client는 본인의 Controller 객체를 AutonomousProxy, 그 외를 SimulatedProxy로 구분. SimulatedProxy는 업데이트가 적용되지 않아 이를 코드로 구현 필요.
- 또한, Server_MoveForward와 같이 서버 통신만 적용 시, Server의 화면에서는 Client의 Pawn이 움직이나 Client의 화면에서는 움직이지 않는 현상이 발생하므로 기존의 Move 함수도 구현한 뒤 안에서 RPC 통신 호출.
```C++
//.cpp
--PlayerInputComponent->BindAxis("MoveRight", this, &AGoKart::Server_MoveForward);
++PlayerInputComponent->BindAxis("MoveForward", this, &AGoKart::MoveForward);

void AGoKart::MoveForward(float Value)
{
	Throttle = Value;
	Server_MoveForward(Value);
}

```
- 그러나 해당 구현 시, 다른 타임 스텝으로 인한 수치 적분의 부정확성으로 Pawn의 위치가 User마다 달라지는 시뮬레이션 오류 발생.  이를 해결하기 위해 우선 서버에서 변수를 복제하는 방법 사용.
```C++
//.h
UPROPERTY(Replicated)
FVector ReplicatedLocation;

UPROPERTY(Replicated)
FRotator ReplicatedRotation;

//.cpp

AGoKart::AGoKart()
{
 	// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;
	bReplicates = true;

}

void AGoKart::GetLifetimeReplicatedProps(TArray< FLifetimeProperty > & OutLifetimeProps) const
{
	Super::GetLifetimeReplicatedProps(OutLifetimeProps);
	DOREPLIFETIME(AGoKart, ReplicatedLocation); 
	DOREPLIFETIME(AGoKart, ReplicatedRotation);
}

if (HasAuthority()) 
	{
		ReplicatedLocation = GetActorLocation();
		ReplicatedRotation = GetActorRotation();
	}
	else 
	{
		SetActorLocation(ReplicatedLocation);
		SetActorRotation(ReplicatedRotation);
	}

```
- 매번 업데이트 하기 보다는 복제 시 코드가 트리거 되도록 하고 그때 업데이트 진행. 그 사이는 시뮬레이션 진행.
```C++
//.h
//ratation이랑 location을 합쳐서 리팩토링
UPROPERTY(ReplicatedUsing=OnRep_ReplicatedTranform)
FTransform ReplicatedTranform;

UFUNCTION()
void OnRep_ReplicatedTranform();

//.cpp
void AGoKart::BeginPlay()
{
	Super::BeginPlay();
	
	if (HasAuthority())
	{
		NetUpdateFrequency = 1;
	}
}

if (HasAuthority()) 
{
	ReplicatedTranform = GetActorTransform();
}

void AGoKart::OnRep_ReplicatedTranform()
{
	SetActorTransform(ReplicatedTranform);
}

```
- 동기화는 완료했으나 부드럽지 못하고 끊기는 글리칭 현상 발생. 이를 해결하기 위해 다른 변수 값도 복제하여 전달.
```C++
//.h
UPROPERTY(Replicated)
FVector Velocity;

UPROPERTY(Replicated)
float Throttle;

UPROPERTY(Replicated)
float SteeringThrow;

//.cpp
void AGoKart::GetLifetimeReplicatedProps(TArray< FLifetimeProperty > & OutLifetimeProps) const
{
	Super::GetLifetimeReplicatedProps(OutLifetimeProps);
	DOREPLIFETIME(AGoKart, ReplicatedTranform);
	DOREPLIFETIME(AGoKart, Velocity);
	DOREPLIFETIME(AGoKart, Throttle);
	DOREPLIFETIME(AGoKart, SteeringThrow);
}

```
- 마지막으로 랙 발생. 랙은 패킷 전달 과정에서 발생하는 왕복 시간에 의해 발생. 클라이언트 뒤에 있는 서버 위치로 재설정 되기에 발생. 이에 왕복 시간도 계산하여 client가 업데이트를 전달 받을 시, 위치가 계산된 이후로 우리의 움직임을 리플레이.
- 이를 구현하기 위한 3단계 의사 코드.(+는 아직 구현하지 않은 것)
	+ OnTick - Client
		1. 새로운 Move 구조체 생성
		2. Unacknowledged move의 리스트 저장 +
		3. server에게 move를 전송
		4. 이후 로컬 환경에서 move를 시뮬레이션
	- OnReceiveMove - Server
		1. Move가 Valid한 지 검사(No Cheating!)
		2. move를 시뮬레이트
		3. 하나로 정해진 State를 Clinet한테 전송
	- OnReceiveServerState - Client
		1. State에 들어있는 모든 Move를 삭제 +
		2. Server State로 Reset
		3. 시뮬레이션된 Unacknowledged move를 Replay +
- 먼저 새로운 Move 및 State 구조체 생성. 이를 통해 기존의 복제되는 변수 리팩토링. 단, Move 경우 LocalControl때만 생성 되도록 구현.
```C++
//.h
USTRUCT()
struct FGoKartMove
{
	GENERATED_USTRUCT_BODY()

	UPROPERTY()
	float Throttle;
	UPROPERTY()
	float SteeringThrow;

	UPROPERTY()
	float DeltaTime;
	UPROPERTY()
	float Time;
};


USTRUCT()
struct FGoKartState
{
	GENERATED_USTRUCT_BODY()

	UPROPERTY()
	FTransform Tranform;

	UPROPERTY()
	FVector Velocity;

	UPROPERTY()
	FGoKartMove LastMove;
};

//기존의 함수를 대체
UFUNCTION(Server, Reliable, WithValidation)
void Server_SendMove(FGoKartMove Move);

UPROPERTY(ReplicatedUsing = OnRep_ServerState)
FGoKartState ServerState;

UFUNCTION()
void OnRep_ServerState();


//.cpp
if (IsLocallyControlled())
	{
		FGoKartMove Move;
		Move.DeltaTime = DeltaTime;
		Move.SteeringThrow = SteeringThrow;
		Move.Throttle = Throttle;
		//TODO: Set time

		Server_SendMove(Move);
	}
	
void AGoKart::OnRep_ServerState()
{
	SetActorTransform(ServerState.Tranform);
	Velocity = ServerState.Velocity;
}
```
- OnRecieveMove의 Move Simulate 구현
```C++

//기존 Tick에서 하던 동작을 SimulateMove로 이동. 이에 Tick에서 SimulateMove(Move) 호출 필요.
void AGoKart::SimulateMove(const FGoKartMove& Move)
{
	FVector Force = GetActorForwardVector() * MaxDrivingForce * Move.Throttle;

	Force += GetAirResistance();
	Force += GetRollingResistance();

	FVector Acceleration = Force / Mass;

	Velocity = Velocity + Acceleration * Move.DeltaTime;

	ApplyRotation(Move.DeltaTime, Move.SteeringThrow);

	UpdateLocationFromVelocity(Move.DeltaTime);
}

void AGoKart::Server_SendMove_Implementation(FGoKartMove Move)
{
//이제 Throttle, SteeringThrow는 복제할 필요 없으므로 관련 코드 삭제.
	SimulateMove(Move);
	ServerState.LastMove = Move;
	ServerState.Tranform = GetActorTransform();
	ServerState.Velocity = Velocity;
}
```
- UnacknowledgeMove list 생성.
```C++
//.h
//Queue가 쌓일 시 LastTime 이전 Queue(직전 State와 현재 State 사이 외 Queue)는 제거.
FGoKartMove CreateMove(float DeltaTime);
void ClearAcknowledgeMoves(FGoKartMove LastMove);

//TArray 사용(TQueue를 사용할 수 있으나 해당 변수명이 더 용이.)
TArray<FGoKartMove> UnacknowledgedMoves;

//.cpp

//기존 Tick에서 진행하던 Create Move를 리팩토링
FGoKartMove AGoKart::CreateMove(float DeltaTime)
{
	FGoKartMove Move;
	Move.DeltaTime = DeltaTime;
	Move.SteeringThrow = SteeringThrow;
	Move.Throttle = Throttle;
	Move.Time = GetWorld()->TimeSeconds;
	
	return Move;
}

void AGoKart::ClearAcknowledgeMoves(FGoKartMove LastMove)
{
	TArray<FGoKartMove> NewMoves;

	for (const FGoKartMove& Move : UnacknowledgedMoves)
	{
		if (Move.Time > LastMove.Time)
		{
			NewMoves.Add(Move);
		}
	}

	UnacknowledgedMoves = NewMoves;
}
```
- GetWorld()->GetTimeSeconds()로 Move의 Time 변수를 설정하여 움직임 비교도 가능하지만, AGameStateBase::GetServerWorldTimeSeconds()로 더 강력하게 가능.
- OnRep_ServerState()에 전달받은 Move로 업데이트 -> SimulateMove함수 사용
```C++
for (const FGoKartMove& Move : UnacknowledgedMoves)
{
	SimulateMove(Move);
}
```
- SimulatedProxy가 예측하는 과정에서 생기는 문제 해결. 너무 빠르게 움직인다거나... -> SimulateMove가 너무 자주 호출되는 것. -> Tick에서 진행되는 코드를 역할별로 확실히 나누자.
```C++
void AGoKart::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

	if (Role == ROLE_AutonomousProxy)
	{
		FGoKartMove Move = CreateMove(DeltaTime);
		SimulateMove(Move);

		UnacknowledgedMoves.Add(Move);
		Server_SendMove(Move);
	}

	// We are the server and in control of the pawn.
	if (Role == ROLE_Authority && IsLocallyControlled())
	{
		FGoKartMove Move = CreateMove(DeltaTime);
		Server_SendMove(Move);
	}

	if (Role == ROLE_SimulatedProxy)
	{
		SimulateMove(ServerState.LastMove);
	}

	DrawDebugString(GetWorld(), FVector(0, 0, 100), GetEnumText(Role), this, FColor::White, DeltaTime);
}
```
