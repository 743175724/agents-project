---
name: Windows内核基础
description: IRQL、内存池、同步机制
version: 1.0.0
---

# Windows Kernel Development Basics

## IRQL Levels
- PASSIVE_LEVEL (0): Normal execution
- APC_LEVEL (1): Asynchronous Procedure Calls
- DISPATCH_LEVEL (2): DPC and scheduler
- DEVICE_IRQL (3+): Hardware interrupts

## Memory Pools
```c
// NonPagedPool: Always resident, use at DISPATCH_LEVEL
PVOID buffer = ExAllocatePool2(POOL_FLAG_NON_PAGED, size, 'Tag1');

// PagedPool: Can be paged out, use at PASSIVE_LEVEL
PVOID buffer = ExAllocatePool2(POOL_FLAG_PAGED, size, 'Tag2');

// Don't forget to free
ExFreePoolWithTag(buffer, 'Tag1');
```

## Synchronization
- Spin Lock: High IRQL, short duration
- Mutex: PASSIVE_LEVEL only
- Fast Mutex: Similar to kernel mutex
- Event: Signal/Wait mechanism

## Common Pitfalls
- Accessing paged memory at DISPATCH_LEVEL
- Forgetting to dereference objects
- Not handling IRP cancellation
- Memory leaks (use Driver Verifier)
