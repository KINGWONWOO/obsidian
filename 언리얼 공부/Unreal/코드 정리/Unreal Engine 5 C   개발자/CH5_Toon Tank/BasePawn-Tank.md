### 기능
---
 User가 조종하는 Tank 기능 구현현

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "BasePawn.h"
#include "Tank.generated.h"
/**
 *
 */
UCLASS()
class TOONTANKS_API ATank : public ABasePawn
{
    GENERATED_BODY()

public:

    ATank();
    // Called to bind functionality to input
    virtual void SetupPlayerInputComponent(class UInputComponent *PlayerInputComponent) override;
	// Called every frame
    virtual void Tick(float DeltaTime) override;

	//Tank 삭제 시 호출
    void HandleDestruction();

	//private 변수를 가져오는 경우가 필요할 시 아래와 같이 Get 함수 정의 가능
    APlayerController* GetTankPlayerController() const { return TankPlayerController; }

	//Tank는 살아있는가?
    bool bAlive = true;

protected:
    // Called when the game starts or when spawned
    virtual void BeginPlay() override;

private:

	//Tank 스프링암
    UPROPERTY(VisibleAnywhere, Category = "Components")
    class USpringArmComponent* SpringArm;

	//Tank 카메라 - 유저가 보는 시야 결정
    UPROPERTY(VisibleAnywhere, Category = "Components")
    class UCameraComponent* Camera;

	//Tank 이동 속도
    UPROPERTY(EditAnywhere, Category = "Movement")
    float Speed = 200.f;

	//Tank 회전 속도
    UPROPERTY(EditAnywhere, Category = "Movement")
    float TurnRate = 45.f;

	//Tank 이동, 회전 구현
    void Move(float Value);
    void Turn(float Value);

	//사용자 컨트롤러
    APlayerController* TankPlayerController;
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings. 
#include "Tank.h"
#include "GameFramework/SpringArmComponent.h"
#include "Camera/CameraComponent.h"
#include "Components/InputComponent.h"
#include "Kismet/GameplayStatics.h"

ATank::ATank()
{
	//스프링암, 카메라 생성 후 Attach
    SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("Spring Arm"));
    SpringArm->SetupAttachment(RootComponent);

    Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("Camera"));
    Camera->SetupAttachment(SpringArm);
}

void ATank::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

	//입력 키와 콜백 함수 바인딩
    PlayerInputComponent->BindAxis(TEXT("MoveForward"), this, &ATank::Move);
    PlayerInputComponent->BindAxis(TEXT("Turn"), this, &ATank::Turn);
    PlayerInputComponent->BindAction(TEXT("Fire"), IE_Pressed, this, &ATank::Fire);
}

void ATank::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);

    if (TankPlayerController)
    {
	    //커서 Hit 추적
        FHitResult HitResult;
        TankPlayerController->GetHitResultUnderCursor(
            ECollisionChannel::ECC_Visibility,
            false,
            HitResult);
		//커서를 보는 방향으로 터렛 회전
        RotateTurret(HitResult.ImpactPoint);
    }
}

void ATank::HandleDestruction()
{
    Super::HandleDestruction();

	//Tank 삭제 -> 게임 종료 -> 숨기기/Tick 비활성화/움직임 비활성화(다른 함수에서 구현)
    SetActorHiddenInGame(true);
    SetActorTickEnabled(false);
    //죽음 이후 Turret이 총알을 계속 쏘지 못하게 bAlive false로 변경
    bAlive = false;
}

void ATank::BeginPlay()
{
    Super::BeginPlay();
	//user controller 설정
    TankPlayerController = Cast<APlayerController>(GetController());
}

void ATank::Move(float Value)
{
	//(0,0,0) 벡터 생성
    FVector DeltaLocation = FVector::ZeroVector;
    // X = Value * DeltaTime * Speed
    // 앞, 뒤 이동만 구현
    DeltaLocation.X = Value * Speed * UGameplayStatics::GetWorldDeltaSeconds(this);
    //Local임에 주의
    AddActorLocalOffset(DeltaLocation, true);
}

void ATank::Turn(float Value)
{
	//(0,0,0) 벡터 생성
    FRotator DeltaRotation = FRotator::ZeroRotator;
    // Yaw = Value * DeltaTime * TurnRate
    DeltaRotation.Yaw = Value * TurnRate * UGameplayStatics::GetWorldDeltaSeconds(this);
    AddActorLocalRotation(DeltaRotation, true);

    GetController();
}
```

