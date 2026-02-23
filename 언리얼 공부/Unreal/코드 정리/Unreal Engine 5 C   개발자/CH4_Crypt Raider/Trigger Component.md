### 기능
---
 물체를 이동 여부를 결정하는 역할

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "Components/BoxComponent.h"
#include "Mover.h"
#include "TriggerComponent.generated.h"

UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent) )

class CRYPTRAIDER_API UTriggerComponent : public UBoxComponent
{
    GENERATED_BODY()
  
public:

    // Sets default values for this component's properties
    UTriggerComponent();
  
protected:

    // Called when the game starts
    virtual void BeginPlay() override;

public:

    // Called every frame
    virtual void TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction) override;

	//Trigger에 연결할 Mover 개체를 설정, 블루프린트 협업을 위해 BlueprintCallable 설정
    UFUNCTION(BlueprintCallable)
    void SetMover(UMover* NewMover);

private :

	//Tag를 통한 특정 물체에 대해서만 반응하도록 코딩
    UPROPERTY(EditAnywhere)
    FName AcceptableActorTag = "Unlock1";

	//연결된 Mover
    UMover* Mover;

	//허용된 Actor인지 확인인
    AActor* GetAcceptableActor() const;
  
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.

#include "TriggerComponent.h"

UTriggerComponent::UTriggerComponent()
{
    // Set this component to be initialized when the game starts, and to be ticked every frame.  You can turn these features
    // off to improve performance if you don't need them.
    PrimaryComponentTick.bCanEverTick = true;
}

void UTriggerComponent::BeginPlay()
{
    Super::BeginPlay();
}

void UTriggerComponent::TickComponent(float DeltaTime, ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction)
{
    Super::TickComponent(DeltaTime, TickType, ThisTickFunction);

	//이 Actor는 허용되는가?
    AActor* Actor = GetAcceptableActor();

	//맞다면 실행
    if(Actor)
    {
	    //SimulatePhysics는 UPrimitiveComponent를 사용 이에 Actor의 GetRootComponent
	    //호출 후 Cast로 UPrimitive로
        UPrimitiveComponent* Component = 
        Cast<UPrimitiveComponent>(Actor->GetRootComponent());
        if(Component != nullptr)
        {
	        //Trigger에 들어오면 Mover가 부착된 Actor는 멈추고 Trigger에 붙어야함.
	        //이에 Physics를 끔
            Component->SetSimulatePhysics(false);
        }
        //이후 붙이기
        Actor->AttachToComponent(this, FAttachmentTransformRules::KeepWorldTransform);
        //움직여도 된다.
        Mover->SetShouldMove(true);
    } else //허용되지 않은 Actor 였다면?
    {
	    //움직이면 안된다.
        Mover->SetShouldMove(false);
    }
}

void UTriggerComponent::SetMover(UMover* NewMover)
{
    Mover = NewMover;
}

AActor* UTriggerComponent::GetAcceptableActor() const
{
	//해당 Trigger에 Overlapping된 Actor들이 여러 개일 수 있으니 TArray 사용
    TArray<AActor*> Actors;
    //Overlapping된 모든 Actor를 Tarray에 저장
    GetOverlappingActors(Actors);

	//For each를 사용하여 하나씩 검사
    for (AActor* Actor : Actors)
    {
	    //Actor의 tag를 확인하여 허용된 Actor 검사
        bool AcceptableActor = Actor->ActorHasTag(AcceptableActorTag);
        //유저가 Grab중에는 부착되면 안되므로 Grab 상태 검사
        bool HasGrabbed = Actor->ActorHasTag("Grabbed");
        //허용됐으며 Grab중이 아니라면?
        if(AcceptableActor && !HasGrabbed)
        {
        //이 Actor를 사용해!
            return Actor;
        }  
    }
    return nullptr;
}
```

