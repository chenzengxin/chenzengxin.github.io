---
title: "虚幻引擎学习2"
author: "Chenzengxin"
date: 2019.09.04
---

## StaticMesh
- headpath
``` cpp
#include "Engine/StaticMesh.h"
```

# camera-control
## APlayerController
<!-- ``` cpp -->
- GetViewTarget() // Get the actor the controller is looking at
- SetViewTarget() // 立即切换
- SetViewTargetWithBlend() // 缓慢切换
<!-- ``` -->
``` cpp
	if ((OurPlayerController->GetViewTarget() != CameraOne) && (CameraOne != nullptr))
	{
		// Cut instantly to camera one.
		OurPlayerController->SetViewTarget(CameraOne);
	}
	else if ((OurPlayerController->GetViewTarget() != CameraTwo) && (CameraTwo != nullptr))
	{
	    // Blend smoothly to camera two.
	    OurPlayerController->SetViewTargetWithBlend(CameraTwo, SmoothBlendTime);
    }
```
---
# ConstructorHelpers
## ConstructorHelpers::FObjectFinder
- headpath
``` cpp
#include "UObject/ConstructorHelpers.h"
```
``` cpp
struct FObjectFinder : public FGCObject
{
	T* Object;
	FObjectFinder(const TCHAR* ObjectToFind)
	{
	    CheckIfIsInConstructor(ObjectToFind);
		FString PathName(ObjectToFind);
		StripObjectClass(PathName,true);

		Object = ConstructorHelpersInternal::FindOrLoadObject<T>(PathName);
		ValidateObject( Object, PathName, ObjectToFind );
	}
	bool Succeeded() const
	{
		return !!Object;
	}

	virtual void AddReferencedObjects( FReferenceCollector& Collector )
	{
		Collector.AddReferencedObject(Object);
	}
}; 
```
---

## UGameplayStatics
- headpath
``` cpp
#include "Kismet/GameplayStatics.h"
```
``` cpp
UGameplayStatics::GetPlayerController(const UObject* WorldContextObject, int32 PlayerIndex )
//获取本地玩家
class APlayerController* UGameplayStatics::GetPlayerController(const UObject* WorldContextObject, int32 PlayerIndex ) 
{
	if (UWorld* World = GEngine->GetWorldFromContextObject(WorldContextObject, EGetWorldErrorMode::LogAndReturnNull))
	{
		uint32 Index = 0;
		for (FConstPlayerControllerIterator Iterator = World->GetPlayerControllerIterator(); Iterator; ++Iterator)
		{
			APlayerController* PlayerController = Iterator->Get();
			if (Index == PlayerIndex)
			{
				return PlayerController;
			}
			Index++;
		}
	}
	return nullptr;
}
```
---
# Components and Collision

## USphereComponent
- headpath
``` cpp
#include "Components/SphereComponent.h"
```
- A sphere generally used for simple collision. Bounds are rendered as lines in the editor.
``` cpp
USphereComponent* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent"));
SphereComponent->InitSphereRadius(40.0f);//设置半径
SphereComponent->SetCollisionProfileName(TEXT("Pawn"));//
```

---


## 改变鼠标样式




## AI移动

	加入AI模块：

``` Csharp
PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore" ,"AIModule"});
```
```cpp

```


## DecalComponent 贴花组件