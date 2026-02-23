### 기능
---
 물체를 잡고 이동 관련 동작을 처리

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "Components/SceneComponent.h"
#include "PhysicsEngine/PhysicsHandleComponent.h"
#include "Grabber.generated.h"

UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent) )

class CRYPTRAIDER_API UGrabber : public USceneComponent
{
    GENERATED_BODY()
   
public:
    // Sets default values for this component's properties
    UGrabber();

protected:
    // Called when the game starts
    virtual void BeginPlay() override;

public:
    // Called every frame
    virtual void TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction) override;

	//잡았다
    UFUNCTION(BlueprintCallable)
    void Grab();

	//놓쳤다
    UFUNCTION(BlueprintCallable)
    void Release();

private:

	//최대 그랩 가능 길이
    UPROPERTY(EditAnywhere)
    float MaxGrabDistance = 400;

	//최대 그랩 반지름(원통형 트레이싱)
    UPROPERTY(EditAnywhere)
    float GrabRadius = 100;    

	//Grab 시 물건의 위치(Pawn 기준 어느정도 앞에?)
    UPROPERTY(EditAnywhere)
    float HoldDistance = 200;

	//PhysicsHandle 불러오기
    UPhysicsHandleComponent* GetPhysicsHandle() const;

	//잡았나?
    bool GetGrabbableInReach(FHitResult& OutHitResult) const;
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "Grabber.h"
#include "Engine/World.h"
#include "DrawDebugHelpers.h"
// Sets default values for this component's properties
UGrabber::UGrabber()
{
    // Set this component to be initialized when the game starts, and to be ticked every frame.  You can turn these features
    // off to improve performance if you don't need them.
    PrimaryComponentTick.bCanEverTick = true;
    // ...
}

// Called when the game starts
void UGrabber::BeginPlay()
{
    Super::BeginPlay();
}

// Called every frame
void UGrabber::TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction)
{
    Super::TickComponent(DeltaTime, TickType, ThisTickFunction);

	//PhysicHandle 불러오기
    UPhysicsHandleComponent *PhysicsHandle = GetPhysicsHandle();
    //PhysicHandle이 있고, 뭔가 잡히는게 있다면
    if (PhysicsHandle && PhysicsHandle->GetGrabbedComponent())
    {
	    //Pawn의 위치(GetComponentLocation)에서 HoldDistance 정도 앞에 위치시키기
        FVector TargetLocation = 
        GetComponentLocation() + GetForwardVector() * HoldDistance

        PhysicsHandle->SetTargetLocationAndRotation(
        TargetLocation, 
        GetComponentRotation()
        );
    }
}

void UGrabber::Grab()
{
    UPhysicsHandleComponent *PhysicsHandle = GetPhysicsHandle();
    if (PhysicsHandle == nullptr)
    {
        return;
    }
    //Hit 결과를 저장할 변수
    FHitResult HitResult;
    //잡히는게 있나? 있다면 HitResult에 저장(레퍼런스 전달)
    bool HasHit = GetGrabbableInReach(HitResult);
    //있다면
    if (HasHit)
    {
	    //잡은 Component 불러와서 Physics 키고, RigidBodie 키고
        UPrimitiveComponent* HitComponent = HitResult.GetComponent();
        HitComponent->SetSimulatePhysics(true);
        HitComponent->WakeAllRigidBodies();
        //잡은 Actor 불러와서 Tag추가하고, Trigger로부터 떼어내고고
        AActor* HitActor = HitResult.GetActor();
        HitActor->Tags.Add("Grabbed");
        HitActor->DetachFromActor(FDetachmentTransformRules::KeepWorldTransform);
        //물건 잡기
        PhysicsHandle->GrabComponentAtLocationWithRotation(
            HitComponent,
            NAME_None,
            HitResult.ImpactPoint,
            GetComponentRotation());
    }
}

void UGrabber::Release()
{
    UPhysicsHandleComponent* PhysicsHandle = GetPhysicsHandle();
    if (PhysicsHandle && PhysicsHandle->GetGrabbedComponent())
    {
	    //Grabbed 태그 삭제후 놓아주기
        AActor* GrabbedActor = PhysicsHandle->GetGrabbedComponent()->GetOwner();
        GrabbedActor->Tags.Remove("Grabbed");
        PhysicsHandle->ReleaseComponent();
    }
}

UPhysicsHandleComponent* UGrabber::GetPhysicsHandle() const
{
    UPhysicsHandleComponent* Result = 
    GetOwner()->FindComponentByClass<UPhysicsHandleComponent>();
    if (Result == nullptr)
    {
        UE_LOG(LogTemp, Error, TEXT("Grabber requires a UPhysicsHandleComponent."));
    }

    return Result;
}

bool UGrabber::GetGrabbableInReach(FHitResult& OutHitResult) const
{
	//Tracing 시작 위치와 종료 위치 설정
    FVector Start = GetComponentLocation();
    FVector End = Start + GetForwardVector() * MaxGrabDistance;
    //시각적 확인을 위해 Debug 함수 사용
    DrawDebugLine(GetWorld(), Start, End, FColor::Red);
    DrawDebugSphere(GetWorld(), End, 10, 10, FColor::Blue, false, 5);
    FCollisionShape Sphere = FCollisionShape::MakeSphere(GrabRadius);

	//Sweep 되면 해당 결과를 HitResult에 저장 이후 return
    return GetWorld()->SweepSingleByChannel(
        OutHitResult,
        Start, End,
        FQuat::Identity,
        ECC_GameTraceChannel2,
        Sphere);
}
```

