### 기능
---
 플랫폼을 간단하게 움직여보는 코드

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "MovingPlatform.generated.h"

UCLASS()

class OBSTACLEASSAULT_API AMovingPlatform : public AActor
{
    GENERATED_BODY()
    
public:
    // Sets default values for this actor's properties
    AMovingPlatform();

protected:
    // Called when the game starts or when spawned
    virtual void BeginPlay() override;
  
public:
    // Called every frame
    virtual void Tick(float DeltaTime) override;

	//움직임 계산을 위한 시작 위치
    FVector StartLocation;
    
	//플랫폼 이동 속도를 FVector로 표현
    UPROPERTY(EditAnywhere, Category = "Moving")
    FVector FlatformVelocity = FVector(100, 0, 0);

	//이동 거리
    UPROPERTY(EditAnywhere, Category = "Moving")
    float MoveDistance = 100;

	//회전 속도
    UPROPERTY(EditAnywhere, Category = "Rotation")
    FRotator RotationVelocity;

	//플랫폼 이동 함수
    void MovePlatform(float DeltaTime);

	//플랫폼 회전 함수수
    void RotatePlatform(float DeltaTime);

};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "MovingPlatform.h"
// Sets default values
AMovingPlatform::AMovingPlatform()
{
    // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
    PrimaryActorTick.bCanEverTick = true;
}

// Called when the game starts or when spawned
void AMovingPlatform::BeginPlay()
{
    Super::BeginPlay();
	//초기 위치 저장
    StartLocation = GetActorLocation();
}

// Called every frame
void AMovingPlatform::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);

	//매 Tick마다 이동 또는 회전 실행
    MovePlatform(DeltaTime);
    RotatePlatform(DeltaTime);
}

void AMovingPlatform::MovePlatform(float DeltaTime)
{
	//새로운 위치를 계산 후 SetActorLocation을 통해 위치 이동
    FVector CurrentLocation = GetActorLocation();
    CurrentLocation += FlatformVelocity * DeltaTime;
    SetActorLocation(CurrentLocation);

	//이동 거리 계산
    float DistanceMoved = FVector::Dist(StartLocation,CurrentLocation);

	//이동 거리가 설정한 값보다 커질 시 반대로 이동동
    if(DistanceMoved > MoveDistance)
    {
        FVector MoveDirection = FlatformVelocity.GetSafeNormal();
        StartLocation = StartLocation + MoveDirection * MoveDistance;
        SetActorLocation(StartLocation);
        FlatformVelocity *= -1;
    }
}

void AMovingPlatform::RotatePlatform(float DeltaTime)
{
	//회전값 계산후 새로운 Rotation 설정
    FRotator CurrentRotation = GetActorRotation();
    CurrentRotation += RotationVelocity * DeltaTime;
    SetActorRotation(CurrentRotation);
    AddActorLocalRotation(RotationVelocity * DeltaTime);
}
```

