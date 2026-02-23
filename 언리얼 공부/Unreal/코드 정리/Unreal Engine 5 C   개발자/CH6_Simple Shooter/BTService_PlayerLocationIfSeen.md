### 기능
---
 Behaviour Tree에서의 Service 구현으로, 
 PlayerLocation을 추적하고 BlackBoard의 변수를 업데이트한다.

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "BehaviorTree/Services/BTService_BlackboardBase.h"
#include "BTService_PlayerLocationIfSeen.generated.h"

/**
 * 
 */
UCLASS()
class SIMPLESHOOTER_API UBTService_PlayerLocationIfSeen : public UBTService_BlackboardBase
{
	GENERATED_BODY()
public:
	UBTService_PlayerLocationIfSeen();

protected:
	//Tick마다 진행되는 함수
	virtual void TickNode(UBehaviorTreeComponent &OwnerComp, uint8 *NodeMemory, float DeltaSeconds) override;
};

```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.


#include "BTService_PlayerLocationIfSeen.h"
#include "BehaviorTree/BlackboardComponent.h"
#include "Kismet/GameplayStatics.h"
#include "GameFramework/Pawn.h"
#include "AIController.h"

UBTService_PlayerLocationIfSeen::UBTService_PlayerLocationIfSeen() 
{
	//BT에서 사용할 Service 이름 설정
    NodeName = "Update Player Location If Seen";
}

void UBTService_PlayerLocationIfSeen::TickNode(UBehaviorTreeComponent &OwnerComp, uint8 *NodeMemory, float DeltaSeconds) 
{
    Super::TickNode(OwnerComp, NodeMemory, DeltaSeconds);

	//User가 사용하는 Pawn 불러오기
    APawn *PlayerPawn = UGameplayStatics::GetPlayerPawn(GetWorld(), 0);
    if (PlayerPawn == nullptr)
    {
        return;
    }

    if (OwnerComp.GetAIOwner() == nullptr)
    {
        return;
    }

	//Ai의 시야에 PlayerPawn이 보인다면
    if (OwnerComp.GetAIOwner()->LineOfSightTo(PlayerPawn))
    {
	    //Bt의 Detail패널에서 선택한 변수에 Player를 저장
        OwnerComp.GetBlackboardComponent()->SetValueAsObject(GetSelectedBlackboardKey(), PlayerPawn);
    }
    else
    {
	    //보이지 않는다면 Player를 저장했던 변수를 초기화
        OwnerComp.GetBlackboardComponent()->ClearValue(GetSelectedBlackboardKey());
    }
}

```

