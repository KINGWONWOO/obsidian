### 기능
---
 AI의 Controller로 사망처리, BT 설정 구현

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "AIController.h"
#include "ShooterAIController.generated.h"

/**
 * 
 */
UCLASS()
class SIMPLESHOOTER_API AShooterAIController : public AAIController
{
	GENERATED_BODY()
public:
	virtual void Tick(float DeltaSeconds) override;
	//죽음 확인
	bool IsDead() const;

protected:
	virtual void BeginPlay() override;

private:
	//연결할 BT 설정정
	UPROPERTY(EditAnywhere)
	class UBehaviorTree* AIBehavior; 

};

```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.


#include "ShooterAIController.h"

#include "Kismet/GameplayStatics.h"
#include "BehaviorTree/BlackboardComponent.h"
#include "ShooterCharacter.h"


void AShooterAIController::BeginPlay() 
{
    Super::BeginPlay();

	//AIBehavior를 블루프린트에서 연결했다면
    if (AIBehavior != nullptr)
    {
	    //실행
        RunBehaviorTree(AIBehavior);

		//Pawn의 위치를 들고와 BT의 Startlocation 변수에 저장
        APawn *PlayerPawn = UGameplayStatics::GetPlayerPawn(GetWorld(), 0);

        GetBlackboardComponent()->SetValueAsVector(TEXT("StartLocation"), GetPawn()->GetActorLocation());
    }
}

void AShooterAIController::Tick(float DeltaSeconds) 
{
    Super::Tick(DeltaSeconds);
}

bool AShooterAIController::IsDead() const
{
	//ShooterCharacter 파일에 IsDead를 호출
    AShooterCharacter* ControlledCharacter = Cast<AShooterCharacter>(GetPawn());
    if (ControlledCharacter != nullptr)
    {
        return ControlledCharacter->IsDead();
    }

    return true;
}

```

