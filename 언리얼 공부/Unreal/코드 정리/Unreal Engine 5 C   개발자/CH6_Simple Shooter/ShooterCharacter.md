### 기능
---
AI와 User 모두에게 적용되는 Character cpp 기능 구현
키입력을 통한 제어, 데미지 처리, 사격, 사망, 체력, 총 연결 관련 처리 구현

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once
#include "CoreMinimal.h"
#include "GameFramework/Character.h"
#include "InputMappingContext.h"
#include "ShooterCharacter.generated.h"

class UInputMappingContext;
class UInputAction;
class AGun;

UCLASS()
class SIMPLESHOOTER_API AShooterCharacter : public ACharacter
{
    GENERATED_BODY()

public:
    // Sets default values for this character's properties
    AShooterCharacter();

	//데미지 받을 시 함수
    virtual float TakeDamage(float DamageAmount, struct FDamageEvent const &DamageEvent, class AController *EventInstigator, AActor *DamageCauser) override;

	//사격
    void Fire();

protected:
    // Called when the game starts or when spawned
    virtual void BeginPlay() override;

public:
	//죽었는가?
    UFUNCTION(BlueprintPure)
    bool IsDead() const;

	//남은 체력 퍼센트 반환 -> HUD의 Progress bar에 사용
    UFUNCTION(BlueprintPure)
    float GetHealthPercent() const;
    // Called every frame
    virtual void Tick(float DeltaTime) override;
    // Called to bind functionality to input
    virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;
    //EnhancedInput 연결
    UPROPERTY(EditAnywhere, Category = Input)
    UInputMappingContext* InputMappingContext;

    UPROPERTY(EditAnywhere, Category = Input)
    UInputAction* Jumping;

    UPROPERTY(EditAnywhere, Category = Input)
    UInputAction* Looking;

    UPROPERTY(EditAnywhere, Category = Input)
    UInputAction* Moving;

    UPROPERTY(EditAnywhere, Category = Input)
    UInputAction* FireAction;

	//사용할 총 연결
    UPROPERTY(EditDefaultsOnly)
    TSubclassOf<AGun> GunClass;

    UPROPERTY()
    AGun* Gun;
	   
	//최대체력 설정
    UPROPERTY(EditDefaultsOnly)
    float MaxHealth = 100;

	//현재체력 설정
    UPROPERTY(VisibleAnywhere)
    float Health;

private:
    class APlayerController* PlayerController;

	//키 입력에 따른 bind 함수
    void Move(const FInputActionValue& Value);
    void Look(const FInputActionValue& Value);
    // void LookUp(float AxisValue);
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
  
#include "ShooterCharacter.h"
#include "EnhancedInputComponent.h"
#include "InputMappingContext.h"
#include "EnhancedInputSubsystems.h"
#include "Gun.h"
#include "GameFramework/CharacterMovementComponent.h"
#include "Components/CapsuleComponent.h"
#include "SimpleShooterGameModeBase.h"

// Sets default values
AShooterCharacter::AShooterCharacter()
{
    // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
    PrimaryActorTick.bCanEverTick = true;

	//Enhanced Input 초기화 과정정
    static ConstructorHelpers::FObjectFinder<UInputMappingContext> InputMappingContextFinder(TEXT("/Game/Input/IMC_Character.IMC_Character"));
    if (InputMappingContextFinder.Succeeded())
    {
        InputMappingContext = InputMappingContextFinder.Object;
    }

    static ConstructorHelpers::FObjectFinder<UInputAction> InputActoinMoveFinder(TEXT("/Game/Input/IA_Moving.IA_Moving"));
    if (InputActoinMoveFinder.Succeeded())
    {
        Moving = InputActoinMoveFinder.Object;
    }

    static ConstructorHelpers::FObjectFinder<UInputAction> InputActoinLookFinder(TEXT("/Game/Input/IA_Looking.IA_Looking"));
    if (InputActoinLookFinder.Succeeded())
    {
        Looking = InputActoinLookFinder.Object;
    }

    static ConstructorHelpers::FObjectFinder<UInputAction> InputActionJumpFinder(TEXT("/Game/Input/IA_Jump.IA_Jump"));
    if (InputActionJumpFinder.Succeeded())
    {
        Jumping = InputActionJumpFinder.Object;
    }

    static ConstructorHelpers::FObjectFinder<UInputAction> InputActionFireFinder(TEXT("/Game/Input/IA_Fire.IA_Fire"));
    if (InputActionFireFinder.Succeeded())
    {
        FireAction = InputActionFireFinder.Object;
    }
}

// Called when the game starts or when spawned
void AShooterCharacter::BeginPlay()
{
    Super::BeginPlay();

	//시작시 현재 체력을 최대체력으로 초기화
    Health = MaxHealth;
	//Enhanced Input 초기화 과정정
    PlayerController = Cast<APlayerController>(GetController());
    if (PlayerController != nullptr)
    {
        UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PlayerController->GetLocalPlayer());
        if (Subsystem != nullptr) {
            Subsystem->AddMappingContext(InputMappingContext, 0);
        }
    }
    //Weapon_r 스켈레탈에 총 클래스 연결
    Gun = GetWorld()->SpawnActor<AGun>(GunClass);
    GetMesh()->HideBoneByName(TEXT("weapon_r"), EPhysBodyOp::PBO_None);
    Gun->AttachToComponent(GetMesh(), FAttachmentTransformRules::KeepRelativeTransform, TEXT("WeaponSocket"));
    Gun->SetOwner(this);
}

bool AShooterCharacter::IsDead() const
{
	//현재 체력 기준으로 죽었는가를 확인
    return Health <= 0;
}

float AShooterCharacter::GetHealthPercent() const
{
	//Progress bar 사용을 위한 체력 백분위 반환환
    return Health / MaxHealth;
}

// Called every frame
void AShooterCharacter::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
}

// Called to bind functionality to input
void AShooterCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

    UEnhancedInputComponent* Input = Cast<UEnhancedInputComponent>(PlayerInputComponent);
    if (Input != nullptr)
    {
	    //키입력과 함수 bind
        Input->BindAction(Moving, ETriggerEvent::Triggered, this, &AShooterCharacter::Move);
        Input->BindAction(Looking, ETriggerEvent::Triggered, this, &AShooterCharacter::Look);
        Input->BindAction(Jumping, ETriggerEvent::Triggered, this, &ACharacter::Jump);
        Input->BindAction(FireAction, ETriggerEvent::Triggered, this, &AShooterCharacter::Fire);
    }
}

float AShooterCharacter::TakeDamage(float DamageAmount, struct FDamageEvent const &DamageEvent, class AController *EventInstigator, AActor *DamageCauser)
{
	//받을 데미지 설정
    float DamageToApply = Super::TakeDamage(DamageAmount, DamageEvent, EventInstigator, DamageCauser);
	//체력이 0보다 밑으로 가지 않기 위해 남은 체력과, 받을 데미지 중 더 작은 걸로 설정
    DamageToApply = FMath::Min(Health, DamageToApply);
    //체력에서 데미지만큼 감소
    Health -= DamageToApply;
    UE_LOG(LogTemp, Warning, TEXT("Health left %f"), Health);

	//데미지를 받고 죽을 시
    if (IsDead())
    {
        ASimpleShooterGameModeBase *GameMode = GetWorld()->GetAuthGameMode<ASimpleShooterGameModeBase>();
        if (GameMode != nullptr)
        {
	        //Pawn은 죽었음을 알림림
            GameMode->PawnKilled(this);
        }

		//더이상 Control 사용 불가, Collision 삭제제
        DetachFromControllerPendingDestroy();
        GetCapsuleComponent()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
    }

    return DamageToApply;
}

void AShooterCharacter::Move(const FInputActionValue& Value)
{
    if (PlayerController)
    {
        // 크기
        float FowardValue = Value.Get<FVector2D>().Y;
        float SideValue = Value.Get<FVector2D>().X;
        // 방향
        const FRotator Rotation = PlayerController->GetControlRotation();
        const FRotator YawRotation(0, Rotation.Yaw, 0);

        FVector FowardDirection = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::X);
        FVector SideDirection = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::Y);
        
        AddMovementInput(FowardDirection, FowardValue);
        AddMovementInput(SideDirection, SideValue);
    }  
}

void AShooterCharacter::Look(const FInputActionValue& Value)
{
    if (PlayerController)
    {
        AddControllerYawInput(Value.Get<FVector2D>().X);
        AddControllerPitchInput(Value.Get<FVector2D>().Y);
    }
}

void AShooterCharacter::Fire()
{
	//사격시 총에 연결된 PullTrigger 함수 호출
    Gun->PullTrigger();
}
```

