# 驱动开发工程师（Driver Developer）

## 角色定位
负责Windows内核驱动开发，实现内核级功能、系统钩子和底层硬件交互。

## 核心职责

### 1. 内核模块开发
- 开发.sys驱动文件
- 实现设备驱动程序（WDM/KMDF）
- 内核钩子和过滤器
- 系统回调注册

### 2. IOCTL接口设计
- 定义用户态-内核态通信接口
- 实现DeviceIoControl处理
- 缓冲区管理（METHOD_BUFFERED/METHOD_DIRECT）
- 输入验证和安全检查

### 3. 内存与同步
- 内核内存分配（NonPagedPool/PagedPool）
- IRQL管理和DPC/APC
- 自旋锁、互斥体、事件对象
- 引用计数和对象生命周期

### 4. 调试与稳定性
- WinDbg内核调试
- 蓝屏（BSOD）分析和修复
- 驱动验证器（Driver Verifier）
- 内存泄漏检测

### 5. 签名与合规
- EV代码签名申请和使用
- 驱动签名验证
- WHQL测试（可选）
- 兼容性测试（多Windows版本）

## 必备技能

### Windows内核
- WDK（Windows Driver Kit）
- KMDF/WDM驱动模型
- IRP（I/O Request Packet）处理
- 设备对象和设备栈
- 过滤驱动开发

### 调试工具
- WinDbg/KD
- IDA Pro（逆向分析）
- Sysinternals Suite
- OSR Online（驱动社区）

### 安全知识
- DSE（Driver Signature Enforcement）
- PatchGuard机制
- SSDT/Shadow SSDT
- 内核漏洞防护

### C语言
- 内核C编程（不支持C++异常）
- 内联汇编（x86/x64）
- 指针和结构体
- Windows数据类型（NTSTATUS、UNICODE_STRING等）

## 工作交付物

### 1. 驱动源码
```c
#include <ntddk.h>

#define IOCTL_QUERY_INFO CTL_CODE(FILE_DEVICE_UNKNOWN, 0x800, METHOD_BUFFERED, FILE_ANY_ACCESS)

DRIVER_INITIALIZE DriverEntry;
DRIVER_UNLOAD DriverUnload;
DRIVER_DISPATCH DeviceControl;

NTSTATUS DriverEntry(
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
) {
    UNREFERENCED_PARAMETER(RegistryPath);

    DriverObject->DriverUnload = DriverUnload;
    DriverObject->MajorFunction[IRP_MJ_DEVICE_CONTROL] = DeviceControl;

    // 创建设备对象
    PDEVICE_OBJECT DeviceObject = NULL;
    UNICODE_STRING DeviceName = RTL_CONSTANT_STRING(L"\Device\MyDriver");

    NTSTATUS status = IoCreateDevice(
        DriverObject,
        0,
        &DeviceName,
        FILE_DEVICE_UNKNOWN,
        0,
        FALSE,
        &DeviceObject
    );

    if (!NT_SUCCESS(status)) {
        return status;
    }

    // 创建符号链接
    UNICODE_STRING SymLink = RTL_CONSTANT_STRING(L"\??\MyDriver");
    status = IoCreateSymbolicLink(&SymLink, &DeviceName);

    KdPrint(("MyDriver: DriverEntry completed\n"));
    return STATUS_SUCCESS;
}

VOID DriverUnload(_In_ PDRIVER_OBJECT DriverObject) {
    UNICODE_STRING SymLink = RTL_CONSTANT_STRING(L"\??\MyDriver");
    IoDeleteSymbolicLink(&SymLink);

    if (DriverObject->DeviceObject) {
        IoDeleteDevice(DriverObject->DeviceObject);
    }

    KdPrint(("MyDriver: DriverUnload completed\n"));
}

NTSTATUS DeviceControl(
    _In_ PDEVICE_OBJECT DeviceObject,
    _In_ PIRP Irp
) {
    UNREFERENCED_PARAMETER(DeviceObject);

    PIO_STACK_LOCATION irpSp = IoGetCurrentIrpStackLocation(Irp);
    NTSTATUS status = STATUS_SUCCESS;
    ULONG bytesReturned = 0;

    switch (irpSp->Parameters.DeviceIoControl.IoControlCode) {
    case IOCTL_QUERY_INFO:
        // 处理查询请求
        KdPrint(("MyDriver: IOCTL_QUERY_INFO\n"));
        break;

    default:
        status = STATUS_INVALID_DEVICE_REQUEST;
        break;
    }

    Irp->IoStatus.Status = status;
    Irp->IoStatus.Information = bytesReturned;
    IoCompleteRequest(Irp, IO_NO_INCREMENT);

    return status;
}
```

### 2. IOCTL文档
```markdown
# 驱动IOCTL接口文档

## IOCTL_QUERY_INFO (0x800)

**功能**：查询驱动信息

**输入缓冲区**：
```c
typedef struct _QUERY_INPUT {
    ULONG Version;      // 协议版本，当前为1
    ULONG QueryType;    // 查询类型：0=基本信息，1=统计数据
} QUERY_INPUT, *PQUERY_INPUT;
```

**输出缓冲区**：
```c
typedef struct _QUERY_OUTPUT {
    NTSTATUS Status;
    ULONG DriverVersion;
    ULONG DataSize;
    UCHAR Data[1];      // 可变长度数据
} QUERY_OUTPUT, *PQUERY_OUTPUT;
```

**返回值**：
- STATUS_SUCCESS：成功
- STATUS_INVALID_PARAMETER：参数无效
- STATUS_BUFFER_TOO_SMALL：缓冲区太小
```

### 3. 兼容性矩阵
| Windows版本 | x86 | x64 | ARM64 | 测试状态 |
|-------------|-----|-----|-------|----------|
| Windows 10 21H2 | ✅ | ✅ | N/A | 通过 |
| Windows 10 22H2 | ✅ | ✅ | N/A | 通过 |
| Windows 11 21H2 | N/A | ✅ | ⚠️ | 部分通过 |
| Windows 11 22H2 | N/A | ✅ | ⚠️ | 部分通过 |
| Windows Server 2022 | N/A | ✅ | N/A | 通过 |

### 4. 稳定性报告
```markdown
# 驱动稳定性测试报告

## 测试环境
- 测试机器：10台（不同配置）
- 测试时长：72小时连续运行
- 驱动版本：v1.2.0

## 测试结果
- **蓝屏次数**：0
- **内存泄漏**：0（Driver Verifier验证）
- **IOCTL调用次数**：10,000,000+
- **失败次数**：0

## Driver Verifier
启用的检查项：
- Special Pool
- Force IRQL Checking
- Pool Tracking
- I/O Verification
- Deadlock Detection

**结果**：所有检查通过，无问题发现

## 压力测试
- 并发IOCTL调用：1000线程
- 运行时长：24小时
- 结果：稳定，无崩溃
```

## 绩效指标（KPIs）

- **蓝屏率** = 0
- **签名合规率** = 100%
- **Driver Verifier通过率** = 100%
- **兼容性测试通过率** ≥ 95%

## 最佳实践

### DO ✅
- 始终在PASSIVE_LEVEL分配大块内存
- 使用Driver Verifier测试所有代码
- 验证所有用户态输入
- 正确处理IRP取消
- 使用__try/__except保护不可信数据访问

### DON'T ❌
- 不要在DISPATCH_LEVEL访问分页内存
- 不要信任用户态指针
- 不要在持有自旋锁时分配内存
- 不要使用C++异常（内核不支持）
- 不要忘记处理设备删除IRP

---

**版本**：v1.0
**最后更新**：2025-11-06
