### 기능
---
 User를 공격하는 Tower의 기능을 구현

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "BasePawn.h"
#include "Tower.generated.h"

/**
 *
 */
UCLASS()
class TOONTANKS_API ATower : public ABasePawn
{
    GENERATED_BODY()

public:
    // Called every frame
    virtual void Tick(float DeltaTime) override;
	// Turret 삭제 함수
    void HandleDestruction();

protected:

    virtual void BeginPlay() override;

private:
	// Tank 관련 처리를 위해 Tank 불러오기
    class ATank* Tank;
	// 유저 인식 거리
    UPROPERTY(EditDefaultsOnly, Category = "Combat")
    float FireRange = 300.f;   
	// 타이머 설정
    FTimerHandle FireRateTimerHandle;
	// 타이머 반복 시간
    float FireRate = 2.f;
	// Fire 가능한가?
    void CheckFireCondition();
	// Fire 거리안에 들어왔는가?
    bool InFireRange();
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "Tower.h"
#include "Tank.h"
#include "Kismet/GameplayStatics.h"
#include "TimerManager.h"

void ATower::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
	//사격 사정거리안에 들어왔을 시
    if (InFireRange())
    {
	    //Turret을 user Tank 방향으로 회전
        RotateTurret(Tank->GetActorLocation());
    }
}

void ATower::HandleDestruction()
{
    Super::HandleDestruction();
	//삭제
    Destroy();
}

void ATower::BeginPlay()
{
    Super::BeginPlay();

	//GetPlayerPawn으로 User의 Tank 불러와서 저장
    Tank = Cast<ATank>(UGameplayStatics::GetPlayerPawn(this, 0));

	//타이머 설정, 2초마다 반복으로, Callback 함수는 CheckFireCondition
    GetWorldTimerManager().SetTimer(FireRateTimerHandle, this, &ATower::CheckFireCondition, FireRate, true);
}

void ATower::CheckFireCondition()
{
    if (Tank == nullptr)
    {
        return;
    }
    //사정거리 안이며 Tank가 살아있으면 사격격
    if (InFireRange() && Tank->bAlive)
    {
        Fire();
    }
}

bool ATower::InFireRange()
{
	//사정거리 안에 들어왔는가를 Dist함수와 if 비교문을 통해 검사
    if (Tank)
    {
        float Distance = FVector::Dist(GetActorLocation(), Tank->GetActorLocation());
        if (Distance <= FireRange)
        {
            return true;
        }
    }

    return false;
}
```

