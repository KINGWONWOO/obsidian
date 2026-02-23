### 기능
---
 총기 디자인, 데미지, 최대 거리, 드레이스 등 총 사용에 필요한 기능들을 구현현

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Gun.generated.h"

UCLASS()
class SIMPLESHOOTER_API AGun : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	AGun();

	// 사격 함수
	void PullTrigger();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

private:
	//총기에 필요한 Component들 선언
	UPROPERTY(VisibleAnywhere)
	USceneComponent* Root;

	UPROPERTY(VisibleAnywhere)
	USkeletalMeshComponent* Mesh;

	//총기에 필요한 사운드 및 파티클 선언언
	UPROPERTY(EditAnywhere)
	UParticleSystem *MuzzleFlash;

	UPROPERTY(EditAnywhere)
	USoundBase* MuzzleSound;

	UPROPERTY(EditAnywhere)
	UParticleSystem *ImpactEffect;

	UPROPERTY(EditAnywhere)
	USoundBase *ImpactSound;

	//최대 사정거리
	UPROPERTY(EditAnywhere)
	float MaxRange = 1000;

	//기본 데미지
	UPROPERTY(EditAnywhere)
	float Damage = 10;

	//트레이스 시스템
	bool GunTrace(FHitResult &Hit, FVector& ShotDirection);

	//총을 소유한 Character의 Controller
	AController* GetOwnerController() const;
};

```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.


#include "Gun.h"

#include "Components/SkeletalMeshComponent.h"
#include "Kismet/GameplayStatics.h"
#include "DrawDebugHelpers.h"

// Sets default values
AGun::AGun()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;
	
	//선언한 Component들을 설정하는 과정정
	Root = CreateDefaultSubobject<USceneComponent>(TEXT("Root"));
	SetRootComponent(Root);

	Mesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("Mesh"));
	Mesh->SetupAttachment(Root);

}

void AGun::PullTrigger() 
{
	//총기 사격시 해당 사운드 및 파티클 실행
	UGameplayStatics::SpawnEmitterAttached(MuzzleFlash, Mesh, TEXT("MuzzleFlashSocket"));
	UGameplayStatics::SpawnSoundAttached(MuzzleSound, Mesh, TEXT("MuzzleFlashSocket"));

	//Hit결과를 저장할 변수
	FHitResult Hit;
	//사격 진행방향을 나타내는 Vector
	FVector ShotDirection;
	//GunTrace를 통해 Hit된 무언가가 있는가?
	bool bSuccess = GunTrace(Hit, ShotDirection);
	//있다면
	if (bSuccess)
	{
		//타격 사운드 및 파티클 실행
		UGameplayStatics::SpawnEmitterAtLocation(GetWorld(), ImpactEffect, Hit.Location, ShotDirection.Rotation());
		UGameplayStatics::PlaySoundAtLocation(GetWorld(), ImpactSound, Hit.Location);

		//맞은 Actor 불러오기
		AActor* HitActor = Hit.GetActor();
		if (HitActor != nullptr)
		{
			//맞은 Actor에 데미지 발생
			FPointDamageEvent DamageEvent(Damage, Hit, ShotDirection, nullptr);
			AController *OwnerController = GetOwnerController();
			HitActor->TakeDamage(Damage, DamageEvent, OwnerController, this);
		}
	}

}

// Called when the game starts or when spawned
void AGun::BeginPlay()
{
	Super::BeginPlay();
	
}

// Called every frame
void AGun::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}

bool AGun::GunTrace(FHitResult &Hit, FVector& ShotDirection) 
{
	AController *OwnerController = GetOwnerController();
	if (OwnerController == nullptr)
		return false;

	FVector Location;
	FRotator Rotation;
	//사용자의 View를 가져와 위치와 회전 설정
	OwnerController->GetPlayerViewPoint(Location, Rotation);
	// 사격방향은 Rotation의 역방향
	ShotDirection = -Rotation.Vector();

	//최종 사격 위치 설정(장애물이 없을 시 가능한 최대 사거리)
	FVector End = Location + Rotation.Vector() * MaxRange;
	//구조체를 정의해서 Trace를 무시할 Actor들을 설정
	FCollisionQueryParams Params;
	Params.AddIgnoredActor(this);
	Params.AddIgnoredActor(GetOwner());
	//LineTrace 실행 결과는 Hit 변수에 저장
	return GetWorld()->LineTraceSingleByChannel(Hit, Location, End, ECollisionChannel::ECC_GameTraceChannel1, Params);
}

AController* AGun::GetOwnerController() const
{
	APawn *OwnerPawn = Cast<APawn>(GetOwner());
	if (OwnerPawn == nullptr)
		return nullptr;
	return OwnerPawn->GetController();
}


```

