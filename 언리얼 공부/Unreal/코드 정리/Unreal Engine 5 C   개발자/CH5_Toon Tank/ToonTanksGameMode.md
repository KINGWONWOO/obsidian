### 기능
---
 게임 Rule을 설정하는 GameMode 구현

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "GameFramework/GameModeBase.h"
#include "ToonTanksGameMode.generated.h"
/**
 *
 */
UCLASS()
class TOONTANKS_API AToonTanksGameMode : public AGameModeBase
{
    GENERATED_BODY()

public:
	//엑터 삭제 발생 시, 이를 통해 각 Pawn에 Destruction 발생 시킴
    void ActorDied(AActor* DeadActor);

protected:
    virtual void BeginPlay() override;

	//게임 시작-종료, UFUNCTION 속성을 통해 블루프린트에서 구현
    UFUNCTION(BlueprintImplementableEvent)
    void StartGame();

    UFUNCTION(BlueprintImplementableEvent)
    void GameOver(bool bWonGame);

private:
	//Tank와 Controller 가져오기
    class ATank* Tank;
    class AToonTanksPlayerController* ToonTanksPlayerController;

	//시작 시간
    float StartDelay = 3.f;

	//게임 시작 처리
    void HandleGameStart();

	//남은 Tower 수
    int32 TargetTowers = 0;

	//남은 Tower 수 세기기
    int32 GetTargetTowerCount();
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "ToonTanksGameMode.h"
#include "Kismet/GameplayStatics.h"
#include "Tank.h"
#include "Tower.h"
#include "ToonTanksPlayerController.h"
#include "TimerManager.h"

void AToonTanksGameMode::ActorDied(AActor *DeadActor)
{
	//죽은게 Tank라면?
    if (DeadActor == Tank)
    {
	    //Tank의 Destruction 호출
        Tank->HandleDestruction();
        if (ToonTanksPlayerController)
        {
	        //Controller 비활성화
            ToonTanksPlayerController->SetPlayerEnabledState(false);
        }
        //게임 오버 - 실패
        GameOver(false);
    }
    //Turret이라면?
    else if (ATower* DestroyedTower = Cast<ATower>(DeadActor))
    {
	    //Turret의 Destruction 호출
        DestroyedTower->HandleDestruction();
        //Turret 수 감소
        --TargetTowers;
        //모든 Turret이 없어졌다면?
        if (TargetTowers == 0)
        {
	        //게임 오버 - 성공
            GameOver(true);
        }
    }
    //입력값이 필요한 콜백함수 사용시 Delegate 사용
    FTimerDelegate TimerDel = FTimerDelegate::CreateUObject(this, &AToonTanksGameMode::BeginPlay);
}

void AToonTanksGameMode::BeginPlay()
{
    Super::BeginPlay();

    HandleGameStart();
}

void AToonTanksGameMode::HandleGameStart()
{
	//타워 갯수 세기
    TargetTowers = GetTargetTowerCount();
    //탱크 가져오기
    Tank = Cast<ATank>(UGameplayStatics::GetPlayerPawn(this, 0));

	//컨트롤러 가져오기
    ToonTanksPlayerController = Cast<AToonTanksPlayerController>(UGameplayStatics::GetPlayerController(this, 0));

	//게임 시작
    StartGame();

    if (ToonTanksPlayerController)
    {
	    //시작시 컨트롤 불가
        ToonTanksPlayerController->SetPlayerEnabledState(false);

		//시작 타이머가 지나면 다시 컨트롤 활성화
        FTimerHandle PlayerEnableTimerHandle;
        FTimerDelegate PlayerEnableTimerDelegate = FTimerDelegate::CreateUObject(
            ToonTanksPlayerController,
            &AToonTanksPlayerController::SetPlayerEnabledState,
            true
        );
        GetWorldTimerManager().SetTimer(PlayerEnableTimerHandle,
            PlayerEnableTimerDelegate,
            StartDelay,
            false
        );
    }
}

int32 AToonTanksGameMode::GetTargetTowerCount()
{
	//타워 갯수 세기
    TArray<AActor*> Towers;
    UGameplayStatics::GetAllActorsOfClass(this, ATower::StaticClass(), Towers);
    return Towers.Num();
}
```

