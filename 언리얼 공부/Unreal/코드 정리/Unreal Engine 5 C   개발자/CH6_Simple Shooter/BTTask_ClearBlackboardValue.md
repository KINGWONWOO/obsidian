### 기능
---
 BT의 Task로, Blackboard의 Value를 초기화하는데 사용

### .h 파일
---
```C++
#pragma once
#include "CoreMinimal.h"
#include "BehaviorTree/Tasks/BTTask_BlackboardBase.h"
#include "BTTask_ClearBlackboardValue.generated.h"
/**
 * 
 */
UCLASS()
class SIMPLESHOOTER_API UBTTask_ClearBlackboardValue : public UBTTask_BlackboardBase
{
	GENERATED_BODY()
public:
	UBTTask_ClearBlackboardValue();
protected:
	virtual EBTNodeResult::Type ExecuteTask(UBehaviorTreeComponent &OwnerComp, uint8 *NodeMemory) override;
};
```

### .cpp 파일
---
```C++
#include "BTTask_ClearBlackboardValue.h"
#include "BehaviorTree/BlackboardComponent.h"
UBTTask_ClearBlackboardValue::UBTTask_ClearBlackboardValue() 
{
	//BT에서 사용할 Task 이름 설정
    NodeName = "Clear Blackboard Value";
}

EBTNodeResult::Type UBTTask_ClearBlackboardValue::ExecuteTask(UBehaviorTreeComponent &OwnerComp, uint8 *NodeMemory) 
{
    Super::ExecuteTask(OwnerComp, NodeMemory);
	//Bt에서 설정한 변수를 초기화한 후 성공 처리를 반환
    OwnerComp.GetBlackboardComponent()->ClearValue(GetSelectedBlackboardKey());
    return EBTNodeResult::Succeeded;
}
```

