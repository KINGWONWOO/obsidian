### 기능
---
 사용자의 Controller 관련 변수 및 함수 처리

### .h 파일
---
```C++
#pragma once
#include "CoreMinimal.h"
#include "GameFramework/PlayerController.h"
#include "ToonTanksPlayerController.generated.h"
/**
 *
 */
UCLASS()
class TOONTANKS_API AToonTanksPlayerController : public APlayerController
{
    GENERATED_BODY()

public:
	//컨트롤 가능 여부
    void SetPlayerEnabledState(bool bPlayerEnabled);
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "ToonTanksPlayerController.h"
#include "GameFramework/Pawn.h"

void AToonTanksPlayerController::SetPlayerEnabledState(bool bPlayerEnabled)
{
	//입력값에 따라 사용자의 컨트롤 가능 여부 설정
    if (bPlayerEnabled)
    {
        GetPawn()->EnableInput(this);
    }
    else
    {
        GetPawn()->DisableInput(this);
    }
    bShowMouseCursor = bPlayerEnabled;
}
```

