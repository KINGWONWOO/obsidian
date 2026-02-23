### 기능
---
 물체에 이동 명령을 내림

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "Components/ActorComponent.h"
#include "Mover.generated.h"
  
UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent) )

class CRYPTRAIDER_API UMover : public UActorComponent
{
    GENERATED_BODY()
    
public:
    // Sets default values for this component's properties
    UMover();
  
protected:
    // Called when the game starts
    virtual void BeginPlay() override;
  
public:
    // Called every frame
	virtual void TickComponent(
	float DeltaTime, 
	ELevelTick TickType,
	FActorComponentTickFunction* ThisTickFunction
	) override;

	//움직임 여부를 변경하는 함수
    UFUNCTION(BlueprintCallable)
    void SetShouldMove(bool ShouldMove);

private:

	//움직이는 방향
    UPROPERTY(EditAnywhere)
    FVector MoveOffset;

	//움직임까지 걸리는 시간
    UPROPERTY(EditAnywhere)
    float MoveTime = 4;

	//움직임 여부
    bool ShouldMove = false;

	//시작 위치(움직임 연산에 필요)
    FVector OriginalLocation;
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "Mover.h"
#include "Math/UnrealMathUtility.h"
// Sets default values for this component's properties

UMover::UMover()
{
    // Set this component to be initialized when the game starts, and to be ticked every frame.  You can turn these features
    // off to improve performance if you don't need them.
    // Tick 활성화
    PrimaryComponentTick.bCanEverTick = true;
    // ...
}

// Called when the game starts
void UMover::BeginPlay()
{
    Super::BeginPlay();
    //해당 Mover라는 Component를 가지고 있는 Actor의 위치 값을 초기값으로 저장.
    OriginalLocation = GetOwner()->GetActorLocation();
}

// Called every frame
void UMover::TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction)
{
    Super::TickComponent(DeltaTime, TickType, ThisTickFunction);

    FVector TargetLocation = OriginalLocation;

    if (ShouldMove)
    {
	    //시작 위치에 MoveOffset을 변경하여 이동 위치를 계산
        TargetLocation = OriginalLocation + MoveOffset;
    }

	//Tick에 맞춰서 이동하는 도중의 위치값을 계속 받아옴
    FVector CurrentLocation = GetOwner()->GetActorLocation();
    //(거리 = 속력 * 시간)을 이용해서 이동 속도 계산 
    float Speed = MoveOffset.Length() / MoveTime;

	//VInterpConstantTo 함수를 이용하여 목표 위치까지 보간하여 천천히 이동
    FVector NewLocation = 
    FMath::VInterpConstantTo(
    CurrentLocation, 
    TargetLocation, 
    DeltaTime, 
    Speed);

	//보간된 값을 이용하여 천천히 Actor의 위치를 Update
    GetOwner()->SetActorLocation(NewLocation);
}

  
void UMover::SetShouldMove(bool NewShouldMove)
{
    ShouldMove = NewShouldMove;
}
```

