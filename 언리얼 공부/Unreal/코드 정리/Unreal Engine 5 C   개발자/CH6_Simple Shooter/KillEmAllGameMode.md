### 기능
---
 모든 적을 죽여야 게임이 끝나는 게임모드 정의

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "SimpleShooterGameModeBase.h"
#include "KillEmAllGameMode.generated.h"

/**
 * 
 */
UCLASS()
class SIMPLESHOOTER_API AKillEmAllGameMode : public ASimpleShooterGameModeBase
{
	GENERATED_BODY()
	
public:
	//필드 내 Pawn이 죽을 시 실행되는 함수수
	virtual void PawnKilled(APawn* PawnKilled) override;

private:
	//게임이 끝난 경우 실행되는 함수
	void EndGame(bool bIsPlayerWinner);

};

```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.


#include "KillEmAllGameMode.h"
#include "EngineUtils.h"
#include "GameFramework/Controller.h"
#include "ShooterAIController.h"


void AKillEmAllGameMode::PawnKilled(APawn* PawnKilled) 
{
    Super::PawnKilled(PawnKilled);

	//Player의 Controller인가 확인을 위해 불러와보기
    APlayerController* PlayerController = Cast<APlayerController>(PawnKilled->GetController());
    //nullptr이 아니라면 죽은 Pawn의 Player
    if (PlayerController != nullptr)
    {
	    //패배로 Endgame 함수 실행
        EndGame(false);
    }

	// for each / TActorRange를 통해 필드 위 모든 AIController를 불러옴
    for (AShooterAIController* Controller : TActorRange<AShooterAIController>(GetWorld()))
    {
	    //하나라도 안죽었나>?
        if (!Controller->IsDead())
        {
	        //아직 게임이 안끝남
            return;
        }
    }
    
    //모두 죽었다면 for문 탈출
    //이에 플레이어의 승리로 게임 종료
    EndGame(true);
}

void AKillEmAllGameMode::EndGame(bool bIsPlayerWinner) 
{
    for (AController* Controller : TActorRange<AController>(GetWorld()))
    {
	    //모든 Controller에 게임이 끝났음을 알림.
	    //bIsWinner를 통해
	    //true가 온 경우(플레이어가 이긴 경우) 플레이어에게만 true, AI들에게는 False 전달
	    //false가 온 경우(AI가 이긴 경우) 플레이어에게만 false, AI들에게는 true 전달
        bool bIsWinner = Controller->IsPlayerController() == bIsPlayerWinner;
        Controller->GameHasEnded(Controller->GetPawn(), bIsWinner);
    }
}

```

