### 기능
---
 Tank와 Tower의 공통 기능 구현

### .h 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#pragma once
#include "CoreMinimal.h"
#include "GameFramework/Pawn.h"
#include "BasePawn.generated.h"

UCLASS()
class TOONTANKS_API ABasePawn : public APawn
{
    GENERATED_BODY()

public:
    // Sets default values for this pawn's properties
    ABasePawn();
    // Pawn 삭제
    void HandleDestruction();

protected:
	// Pawn 회전 처리
    void RotateTurret(FVector LookAtTarget);
    // 총알 발사
    void Fire();

private:
	// 충돌을 처리할 캡슐 콜리전, Private 선언에도 블루프린트에서 볼려면 meta 속성 추가
    UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components", meta = (AllowPrivateAccess = "true"))
	class UCapsuleComponent *CapsuleComp;

	// 몸통 컴포넌트
    UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components", meta = (AllowPrivateAccess = "true"))
    UStaticMeshComponent *BaseMesh;

	//상체 컴포넌트
    UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components", meta = (AllowPrivateAccess = "true"))
    UStaticMeshComponent *TurretMesh;

	//투사체 스폰 위치
    UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = "Components", meta = (AllowPrivateAccess = "true"))
    USceneComponent *ProjectileSpawnPoint;

	//투사체 컴포넌트 -> 이후 사용을 위해 UClass 형태
    UPROPERTY(EditDefaultsOnly, Category = "Combat")
    TSubclassOf<class AProjectile> ProjectileClass;

	//파티클
    UPROPERTY(EditAnywhere, Category = "Combat")
    class UParticleSystem *DeathParticles;

	//사운드
    UPROPERTY(EditAnywhere, Category = "Combat")
    class USoundBase *DeathSound;

	//카메라 떨림
    UPROPERTY(EditAnywhere, Category = "Combat")
    TSubclassOf<class UCameraShake> DeathCameraShakeClass;

};
```

### .cpp 파일
---
```C++
// Fill out your copyright notice in the Description page of Project Settings.
#include "BasePawn.h"
#include "Components/CapsuleComponent.h"
#include "Components/StaticMeshComponent.h"
#include "Projectile.h"
#include "Kismet/GameplayStatics.h"
#include "Particles/ParticleSystem.h"

// Sets default values
ABasePawn::ABasePawn()
{
    // Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
    PrimaryActorTick.bCanEverTick = true;
	//캡슐 컴포넌트 생성 후 Root Component로 설정
    CapsuleComp = CreateDefaultSubobject<UCapsuleComponent>(TEXT("Capsule Collider"));
    RootComponent = CapsuleComp;
	//아래로 각각 컴포넌트 생성 후(이래야 블루프린트에서 설정 가능) Attach
    BaseMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Base Mesh"));
    BaseMesh->SetupAttachment(CapsuleComp);

    TurretMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Turret Mesh"));
    TurretMesh->SetupAttachment(BaseMesh);

    ProjectileSpawnPoint = CreateDefaultSubobject<USceneComponent>(TEXT("Spawn Point"));
    ProjectileSpawnPoint->SetupAttachment(TurretMesh);
}

void ABasePawn::HandleDestruction()
{
    // Pawn삭제 시 사운드/비쥬얼 효과 처리
    if (DeathParticles)
    {
	    //파티클 생성
        UGameplayStatics::SpawnEmitterAtLocation(this, DeathParticles, GetActorLocation(), GetActorRotation());
    }
    if (DeathSound)
    {
	    //사운드 생성
        UGameplayStatics::PlaySoundAtLocation(this, DeathSound, GetActorLocation());
    }
    if (DeathCameraShakeClass)
    {
	    //카메라 떨림 생성성
        GetWorld()->GetFirstPlayerController()->ClientPlayCameraShake(DeathCameraShakeClass);
    }
}
  
void ABasePawn::RotateTurret(FVector LookAtTarget)
{
	//원하는 위치 - 현재 위치로 둘을 잇는 벡터 생성
    FVector ToTarget = LookAtTarget - TurretMesh->GetComponentLocation();
    //Yaw - Z축 기준으로 위아래 회전을 제외한 FRotator 생성
    FRotator LookAtRotation = FRotator(0.f, ToTarget.Rotation().Yaw, 0.f);
    //회전 적용
    TurretMesh->SetWorldRotation(LookAtRotation);
}

void ABasePawn::Fire()
{
	//투사체 스폰 위치의 위치값, 회전값 저장
    FVector Location = ProjectileSpawnPoint->GetComponentLocation();
    FRotator Rotation = ProjectileSpawnPoint->GetComponentRotation();

	//AProjectile 타입의 Actor를 SpawnActor를 통해 생성
    AProjectile* Projectile = GetWorld()->SpawnActor<AProjectile>(ProjectileClass, Location, Rotation);
	//이후 처리를 위해 SetOwner 설정
    Projectile->SetOwner(this);
}
```

