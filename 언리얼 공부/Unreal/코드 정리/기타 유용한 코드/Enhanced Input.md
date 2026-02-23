## 사전설정
---
[참고링크](https://reitbe.github.io/portfolio-explosion/2024/04/15/unrealengine5-character-movement-with-enhancedinput.html)
![[Pasted image 20240727231105.png]]
![[Pasted image 20240727231113.png]]
![[Pasted image 20240727231120.png]]
![[Pasted image 20240727231129.png]]

## .h
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

UCLASS()
class SIMPLESHOOTER_API AShooterCharacter : public ACharacter
{
    GENERATED_BODY()

public:
    // Sets default values for this character's properties
    AShooterCharacter();

protected:
    // Called when the game starts or when spawned
    virtual void BeginPlay() override;

public:
    // Called every frame
    virtual void Tick(float DeltaTime) override;
    // Called to bind functionality to input
    virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;

    UPROPERTY(EditAnywhere, Category = Input)
    UInputMappingContext* InputMappingContext;

    UPROPERTY(EditAnywhere, Category = Input)
    UInputAction* Jumping;

    UPROPERTY(EditAnywhere, Category = Input)
    UInputAction* Looking;

    UPROPERTY(EditAnywhere, Category = Input)
    UInputAction* Moving;

private:
    class APlayerController* PlayerController;

    void Move(const FInputActionValue& Value);
    void Look(const FInputActionValue& Value);
    // void LookUp(float AxisValue);
};
```

## .cpp
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "ShooterCharacter.h"
#include "Components/CapsuleComponent.h"
#include "GameFramework/SpringArmComponent.h"
#include "EnhancedInputComponent.h"
#include "InputMappingContext.h"
#include "EnhancedInputSubsystems.h"
#include "Camera/CameraComponent.h"
#include "GameFramework/CharacterMovementComponent.h"

// Sets default values
AShooterCharacter::AShooterCharacter()
{
    // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
    PrimaryActorTick.bCanEverTick = true;

    static ConstructorHelpers::FObjectFinder<UInputMappingContext> InputMappingContextFinder
    (TEXT("/Game/Input/IMC_Character.IMC_Character"));
    if (InputMappingContextFinder.Succeeded())
    {
        InputMappingContext = InputMappingContextFinder.Object;
    }

    static ConstructorHelpers::FObjectFinder<UInputAction> InputActoinMoveFinder
    (TEXT("/Game/Input/IA_Moving.IA_Moving"));
    if (InputActoinMoveFinder.Succeeded())
    {
        Moving = InputActoinMoveFinder.Object;
    }

    static ConstructorHelpers::FObjectFinder<UInputAction> InputActoinLookFinder
    (TEXT("/Game/Input/IA_Looking.IA_Looking"));
    if (InputActoinLookFinder.Succeeded())
    {
        Looking = InputActoinLookFinder.Object;
    }

    static ConstructorHelpers::FObjectFinder<UInputAction> InputActionJumpFinder
    (TEXT("/Game/Input/IA_Jump.IA_Jump"));
    if (InputActionJumpFinder.Succeeded())
    {
        Jumping = InputActionJumpFinder.Object;
    }
}

// Called when the game starts or when spawned
void AShooterCharacter::BeginPlay()
{
    Super::BeginPlay();

    PlayerController = Cast<APlayerController>(GetController());
    if (PlayerController != nullptr)
    {
        UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PlayerController->GetLocalPlayer());
        if (Subsystem != nullptr) {
            Subsystem->AddMappingContext(InputMappingContext, 0);
        }
    }
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
        Input->BindAction(Moving, ETriggerEvent::Triggered, this, &AShooterCharacter::Move);
        Input->BindAction(Looking, ETriggerEvent::Triggered, this, &AShooterCharacter::Look);
        Input->BindAction(Jumping, ETriggerEvent::Triggered, this, &ACharacter::Jump);
    }
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
```