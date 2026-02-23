### 기능
---
 Pawn들의 체력 관련 변수 및 함수 처리

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "Components/ActorComponent.h"
#include "HealthComponent.generated.h"

UCLASS(ClassGroup = (Custom), meta = (BlueprintSpawnableComponent))
class TOONTANKS_API UHealthComponent : public UActorComponent
{
    GENERATED_BODY()

public:
    // Sets default values for this component's properties
    UHealthComponent();

protected:
    // Called when the game start
    virtual void BeginPlay() override;

private:
	//최대 체력
    UPROPERTY(EditAnywhere)
    float MaxHealth = 100.f;

	//현재 체력, 일단 0으로 초기화 후 Begin Play에서 Max로 초기화
    float Health = 0.f;

	//데미지를 받으면
    UFUNCTION()
    void DamageTaken(AActor *DamagedActor, float Damage, const UDamageType *DamageType, class AController *Instigator, AActor *DamageCauser);

	//게임모드
    class AToonTanksGameMode* ToonTanksGameMode;

public:
    // Called every frame
    virtual void TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction) override;
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "HealthComponent.h"
#include "GameFramework/Actor.h"
#include "Kismet/GameplayStatics.h"
#include "ToonTanksGameMode.h"

// Sets default values for this component's properties
UHealthComponent::UHealthComponent()
{
    // Set this component to be initialized when the game starts, and to be ticked every frame.  You can turn these features
    // off to improve performance if you don't need them.
    PrimaryComponentTick.bCanEverTick = true;
    // ...
}

// Called when the game starts
void UHealthComponent::BeginPlay()
{
    Super::BeginPlay();

	//체력 초기화
    Health = MaxHealth;

	//Damage 발생 시 Broadcast되는 Invocation 함수 리스트에 사용자 정의 DamageTaken 함수를       추가
    GetOwner()->OnTakeAnyDamage.AddDynamic(this, &UHealthComponent::DamageTaken);
    ToonTanksGameMode = Cast<AToonTanksGameMode>(UGameplayStatics::GetGameMode(this));
}

// Called every frame
void UHealthComponent::TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction)
{
    Super::TickComponent(DeltaTime, TickType, ThisTickFunction);
    // ...
}

void UHealthComponent::DamageTaken(AActor *DamagedActor, float Damage, const UDamageType *DamageType, class AController *Instigator, AActor *DamageCauser)
{
	// 데미지 받을 시 체력에서 이를 감소
    if (Damage <= 0.f) return;
    Health -= Damage;
    // 0보다 작아졌다? 게임모드의 ActorDied 호출
    if (Health <= 0.f && ToonTanksGameMode)
    {
        ToonTanksGameMode->ActorDied(DamagedActor);
    }
}
```

