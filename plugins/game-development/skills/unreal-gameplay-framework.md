# Unreal Engine Gameplay Framework

## Core Classes
- **AActor**: Base class for placeable objects
- **APawn**: Actors that can be possessed
- **ACharacter**: Humanoid pawns with movement
- **APlayerController**: Player input and control
- **AGameMode**: Game rules and logic

## Component Pattern
```cpp
UCLASS()
class AMyCharacter : public ACharacter {
    GENERATED_BODY()

    UPROPERTY(VisibleAnywhere)
    UStaticMeshComponent* MeshComp;

    UPROPERTY(VisibleAnywhere)
    UBoxComponent* TriggerBox;

public:
    AMyCharacter() {
        MeshComp = CreateDefaultSubobject<UStaticMeshComponent>("Mesh");
        TriggerBox = CreateDefaultSubobject<UBoxComponent>("Trigger");
    }
};
```

## Gameplay Ability System
- Attributes and AttributeSets
- GameplayEffects for buffs/debuffs
- GameplayAbilities for skills
- GameplayTasks for async operations

## Best Practices
- Use Blueprintable C++ classes
- Leverage UProperty for reflection
- Minimize Tick usage
- Use Object Pooling for frequently spawned actors
