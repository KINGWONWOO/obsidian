### 기능
---
 날라가는 투사체(총알) 관련 변수 및 함수 정의

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Projectile.generated.h"

//전방 선언은 한 번만 하면 된다. 이에 이렇게 아예 앞에 미리 선언하는 방식도 가능
class USoundBase;

UCLASS()
class TOONTANKS_API AProjectile : public AActor
{
    GENERATED_BODY()

public:
    // Sets default values for this actor's properties
    AProjectile();

protected:
    // Called when the game starts or when spawned
    virtual void BeginPlay() override;

private:
	//투사체 Mesh 선언
    UPROPERTY(EditDefaultsOnly, Category = "Combat")
    UStaticMeshComponent *ProjectileMesh;

	//투사체 움직임 Component 선언
    UPROPERTY(VisibleAnywhere, Category = "Movement")
    class UProjectileMovementComponent *ProjectileMovementComponent;

	//투사체가 부딪힐 시(Hit 발생 시) 콜백할 함수
    UFUNCTION()
    void OnHit(UPrimitiveComponent *HitComp, AActor *OtherActor, UPrimitiveComponent *OtherComp, FVector NormalImpulse, const FHitResult &Hit);

	//투사체 데미지
    UPROPERTY(EditAnywhere)
    float Damage = 50.f;

	//투사체 파티클(한 번 발생)
    UPROPERTY(EditAnywhere, Category = "Combat")
    class UParticleSystem *HitParticles;

	//투사체 파티클 컴포넌트(지속 발생)
    UPROPERTY(VisibleAnywhere, Category = "Combat")
    class UParticleSystemComponent *TrailParticles;

	//발사 사운드
    UPROPERTY(EditAnywhere, Category = "Combat")
    USoundBase *LaunchSound;

	//Hit 사운드
    UPROPERTY(EditAnywhere, Category = "Combat")
    USoundBase *HitSound;

	//카메라 떨림 이후 처리를 위해 Uclass로 선언
    UPROPERTY(EditAnywhere, Category = "Combat")
    TSubclassOf<class UCameraShake> HitCameraShakeClass;

public:
    // Called every frame
    virtual void Tick(float DeltaTime) override;
};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "Projectile.h"
#include "Components/StaticMeshComponent.h"
#include "GameFramework/ProjectileMovementComponent.h"
#include "GameFramework/DamageType.h"
#include "Kismet/GameplayStatics.h"
#include "Particles/ParticleSystemComponent.h"

// Sets default values
AProjectile::AProjectile()
{
	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = false;

	//Projectile Mesh 생성 후 Rootcomponent로 설정
	ProjectileMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Projectile Mesh"));
	RootComponent = ProjectileMesh;

	//움직임 Component도 생성 후 최대 속도, 최초 속도 설정
	ProjectileMovementComponent = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("Projectile Movement Component"));
	ProjectileMovementComponent->MaxSpeed = 1300.f;
	ProjectileMovementComponent->InitialSpeed = 1300.f;

	//Particle Component의 경우도 다른 Component와 같이 생성 필요
	TrailParticles = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("Smoke Trail"));
	TrailParticles->SetupAttachment(RootComponent);
}

// Called when the game starts or when spawned
void AProjectile::BeginPlay()
{
	Super::BeginPlay();

	//Hit 발생 시 Broadcast되는 Invocation 함수 리스트에 사용자 정의 On Hit 함수를 추가
	ProjectileMesh->OnComponentHit.AddDynamic(this, &AProjectile::OnHit);
	if (LaunchSound)
	{
		//사운드 재생
		UGameplayStatics::PlaySoundAtLocation(this, LaunchSound, GetActorLocation());
	}
}

// Called every frame
void AProjectile::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);
}

void AProjectile::OnHit(UPrimitiveComponent *HitComp, AActor *OtherActor, UPrimitiveComponent *OtherComp, FVector NormalImpulse, const FHitResult &Hit)
{
	//ApplyDamage에 필요한 입력값들 설정
	AActor* MyOwner = GetOwner();
	if (MyOwner == nullptr)
	{
		Destroy();
		return;
	}

	AController* MyOwnerInstigator = MyOwner->GetInstigatorController();
	UClass* DamageTypeClass = UDamageType::StaticClass();

	//자기 자신과 충돌 금지
	if (OtherActor && OtherActor != this && OtherActor != MyOwner)
	{
		//데미지 발생, 이를 통해 DamageTaken함수 실행
		UGameplayStatics::ApplyDamage(OtherActor, Damage, MyOwnerInstigator, this, DamageTypeClass);
		if (HitParticles)
		{
			//파티클 생성
			UGameplayStatics::SpawnEmitterAtLocation(this, HitParticles, GetActorLocation(), GetActorRotation());
		}
		if (HitSound)
		{
			//사운드 재생
			UGameplayStatics::PlaySoundAtLocation(this, HitSound, GetActorLocation());
		}
		if (HitCameraShakeClass)
		{
			//카메라 떨림 발생생
			// UE 4.25 - ClientPlayCameraShake; UE 4.26+ ClientStartCameraShake
			GetWorld()->GetFirstPlayerController()->ClientPlayCameraShake(HitCameraShakeClass);
		}
	}
	//모든 처리 후 삭제
	Destroy();
}

```

