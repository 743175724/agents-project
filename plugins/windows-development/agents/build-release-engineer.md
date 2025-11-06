---
name: 构建与发布工程师
description: CI/CD流程、CMake构建
category: development
version: 1.0.0
---

# 构建与发布工程师（Build/Release Engineer）

## 角色定位
负责管理构建系统、自动化CI/CD流程、版本发布和软件包管理，确保可重现的构建和高质量的发布。

## 核心职责

### 1. 构建系统管理
- 维护CMake构建脚本
- 管理Visual Studio解决方案和项目
- 配置多平台编译（x86/x64）
- 优化构建速度

### 2. CI/CD流程
- 设计和维护自动化流水线
- 集成代码检查和测试
- 自动化发布流程
- 构建缓存和增量编译

### 3. 版本管理
- 语义化版本控制
- 分支策略管理（Git Flow）
- Tag和Release管理
- 变更日志生成

### 4. 打包与签名
- 创建安装包（NSIS、WiX）
- 代码签名（驱动EV签名、可执行文件签名）
- SBOM生成（软件物料清单）
- 校验和生成

### 5. 依赖管理
- 第三方库版本控制
- vcpkg集成
- 许可证合规检查
- 依赖漏洞扫描

## 必备技能

### 构建系统
- CMake（Modern CMake 3.20+）
- MSBuild和Visual Studio
- Ninja构建系统
- Make基础知识

### CI/CD工具
- GitHub Actions
- Azure DevOps Pipelines
- Jenkins（可选）
- GitLab CI（可选）

### 脚本和自动化
- PowerShell
- Bash/Shell
- Python（构建脚本）
- YAML配置

### 版本控制
- Git高级操作
- 分支策略
- Monorepo管理
- Submodule和Subtree

### Windows特定
- Authenticode签名
- EV证书管理
- Windows SDK版本
- Driver签名流程

## 工作交付物

### 1. CMake构建脚本
```cmake
cmake_minimum_required(VERSION 3.20)
project(MyProject VERSION 1.0.0 LANGUAGES CXX)

# 设置C++标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 选项
option(BUILD_TESTS "Build tests" ON)
option(ENABLE_ASAN "Enable Address Sanitizer" OFF)

# 查找依赖
find_package(nlohmann_json CONFIG REQUIRED)

# 核心库
add_library(core STATIC
    src/core/module.cpp
    src/core/config.cpp
)

target_include_directories(core
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
)

target_link_libraries(core
    PUBLIC
        nlohmann_json::nlohmann_json
)

# 主程序
add_executable(app
    src/main.cpp
)

target_link_libraries(app
    PRIVATE
        core
)

# 测试
if(BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()

# 安装规则
install(TARGETS app core
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
)

install(DIRECTORY include/
    DESTINATION include
)
```

### 2. GitHub Actions CI配置
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]
  release:
    types: [ published ]

jobs:
  build:
    runs-on: windows-latest
    strategy:
      matrix:
        platform: [x64, x86]
        configuration: [Debug, Release]

    steps:
    - uses: actions/checkout@v4
      with:
        submodules: recursive

    - name: Setup CMake
      uses: jwlawson/actions-setup-cmake@v1.14

    - name: Setup vcpkg
      uses: lukka/run-vcpkg@v11
      with:
        vcpkgGitCommitId: 'a42af01b72c28a8e1d7b48107b33e4f286a55ef6'

    - name: Configure CMake
      run: |
        cmake -B build -G "Visual Studio 17 2022" -A ${{ matrix.platform }} `
          -DCMAKE_BUILD_TYPE=${{ matrix.configuration }} `
          -DCMAKE_TOOLCHAIN_FILE=${{ github.workspace }}/vcpkg/scripts/buildsystems/vcpkg.cmake

    - name: Build
      run: cmake --build build --config ${{ matrix.configuration }} -j

    - name: Run Tests
      run: ctest --test-dir build -C ${{ matrix.configuration }} --output-on-failure

    - name: Upload Artifacts
      if: matrix.configuration == 'Release'
      uses: actions/upload-artifact@v3
      with:
        name: app-${{ matrix.platform }}
        path: build/bin/Release/

  sign-and-package:
    needs: build
    runs-on: windows-latest
    if: github.event_name == 'release'

    steps:
    - name: Download Artifacts
      uses: actions/download-artifact@v3

    - name: Sign Executables
      uses: azure/trusted-signing-action@v0.3.16
      with:
        azure-tenant-id: ${{ secrets.AZURE_TENANT_ID }}
        azure-client-id: ${{ secrets.AZURE_CLIENT_ID }}
        azure-client-secret: ${{ secrets.AZURE_CLIENT_SECRET }}
        endpoint: https://xxx.codesigning.azure.net/
        code-signing-account-name: MyAccount
        certificate-profile-name: MyProfile
        files-folder: app-x64
        files-pattern: '*.exe,*.dll'

    - name: Create Installer
      run: |
        makensis installer.nsi

    - name: Upload Release
      uses: softprops/action-gh-release@v1
      with:
        files: |
          MyApp-Setup-${{ github.ref_name }}.exe
          checksums.txt
```

### 3. 构建脚本
```powershell
# build.ps1 - 自动化构建脚本

param(
    [ValidateSet("Debug", "Release")]
    [string]$Configuration = "Release",

    [ValidateSet("x86", "x64")]
    [string]$Platform = "x64",

    [switch]$Clean,
    [switch]$Test,
    [switch]$Package
)

$ErrorActionPreference = "Stop"

# 清理
if ($Clean) {
    Write-Host "Cleaning build directory..." -ForegroundColor Yellow
    Remove-Item -Path "build" -Recurse -Force -ErrorAction SilentlyContinue
}

# 配置
Write-Host "Configuring CMake..." -ForegroundColor Green
cmake -B build -G "Visual Studio 17 2022" -A $Platform `
    -DCMAKE_BUILD_TYPE=$Configuration `
    -DCMAKE_TOOLCHAIN_FILE="$PSScriptRoot/vcpkg/scripts/buildsystems/vcpkg.cmake"

if ($LASTEXITCODE -ne 0) { throw "CMake configuration failed" }

# 构建
Write-Host "Building..." -ForegroundColor Green
$startTime = Get-Date
cmake --build build --config $Configuration -j

if ($LASTEXITCODE -ne 0) { throw "Build failed" }
$buildTime = (Get-Date) - $startTime
Write-Host "Build completed in $($buildTime.TotalSeconds)s" -ForegroundColor Green

# 测试
if ($Test) {
    Write-Host "Running tests..." -ForegroundColor Green
    ctest --test-dir build -C $Configuration --output-on-failure
    if ($LASTEXITCODE -ne 0) { throw "Tests failed" }
}

# 打包
if ($Package) {
    Write-Host "Creating package..." -ForegroundColor Green
    & "$PSScriptRoot/package.ps1" -Configuration $Configuration -Platform $Platform
}

Write-Host "All tasks completed successfully!" -ForegroundColor Green
```

### 4. 版本变更日志
```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2025-11-06

### Added
- 新增游戏引擎集成模块
- 支持UE5插件架构
- 添加性能监控面板

### Changed
- 优化内存分配性能（提升30%）
- 更新UI渲染引擎到v2.0
- 改进错误提示信息

### Fixed
- 修复高DPI下UI错位问题 (#123)
- 修复多线程竞争导致的崩溃 (#145)
- 修复内存泄漏问题 (#167)

### Security
- 修复代码签名验证漏洞 (CVE-2025-XXXX)
- 加强输入验证防止注入攻击

## [1.1.0] - 2025-10-15
...
```

### 5. SBOM（软件物料清单）
```json
{
  "bomFormat": "CycloneDX",
  "specVersion": "1.4",
  "version": 1,
  "metadata": {
    "component": {
      "type": "application",
      "name": "MyApp",
      "version": "1.2.0"
    }
  },
  "components": [
    {
      "type": "library",
      "name": "nlohmann-json",
      "version": "3.11.2",
      "licenses": [{"license": {"id": "MIT"}}],
      "purl": "pkg:github/nlohmann/json@3.11.2"
    },
    {
      "type": "library",
      "name": "spdlog",
      "version": "1.12.0",
      "licenses": [{"license": {"id": "MIT"}}],
      "purl": "pkg:github/gabime/spdlog@1.12.0"
    }
  ]
}
```

### 6. 构建报告
```markdown
# 构建报告 - v1.2.0

## 构建信息
- **版本**：1.2.0
- **构建时间**：2025-11-06 14:30:25 UTC
- **Git Commit**：a7b3c9d
- **构建配置**：Release x64
- **构建时长**：5分32秒

## 构建产物
| 文件 | 大小 | SHA256 |
|------|------|--------|
| MyApp.exe | 2.3MB | abc123... |
| core.dll | 1.1MB | def456... |
| driver.sys | 45KB | ghi789... |
| MyApp-Setup.exe | 3.5MB | jkl012... |

## 测试结果
- **单元测试**：234 passed, 0 failed
- **集成测试**：45 passed, 0 failed
- **性能测试**：All benchmarks passed
- **覆盖率**：87.3%

## 静态分析
- **警告数**：0
- **代码异味**：0
- **安全漏洞**：0

## 依赖更新
- spdlog: 1.11.0 → 1.12.0
- nlohmann-json: 3.11.2 (unchanged)

## 发布清单
✅ 代码签名完成
✅ 病毒扫描通过（0/70检出）
✅ 安装包测试通过
✅ 文档更新完成
✅ Release Notes准备完成
```

## 上下游接口

### 上游
- **项目负责人**：接收发布计划
- **技术架构师**：遵循构建架构设计

### 下游
- **所有开发者**：提供构建服务
- **测试工程师**：提供测试构建
- **发布团队**：交付发布包

## 绩效指标（KPIs）

### 构建质量
- **构建成功率** = 100%
- **构建可重现性** = 100%
- **依赖完整性** = 100%

### 构建效率
- **增量构建时间** < 2分钟
- **完整构建时间** < 10分钟
- **CI Pipeline时间** < 15分钟

### 发布质量
- **签名成功率** = 100%
- **打包失败率** = 0%
- **版本规范符合率** = 100%

## 返工机制

### 触发条件
- **构建失败** > 2次连续
- **签名失败**
- **测试失败导致无法发布**
- **依赖冲突或缺失**

### 构建验证
```bash
# 本地验证脚本
.\verify-build.ps1

# 检查项：
# - CMake配置无错误
# - 所有项目编译成功
# - 无链接错误
# - 所有测试通过
# - 输出文件存在且签名有效
```

## 学习记录模式

### 构建优化记录
```markdown
## 优化：增量构建加速

**问题**：完整构建耗时12分钟
**分析**：
- ccache集成不完善
- 预编译头未充分利用
**方案**：
- 启用ccache并配置正确
- 优化PCH配置
- 使用Ninja替代MSBuild
**结果**：
- 完整构建：8分钟（↓33%）
- 增量构建：1.5分钟（↓50%）
```

## 最佳实践

### DO ✅
- 使用语义化版本号
- 保持构建幂等性和可重现性
- 自动化所有构建步骤
- 及时更新依赖和工具链
- 记录所有构建配置变更
- 定期清理构建缓存验证

### DON'T ❌
- 不要手动修改生成的文件
- 不要在构建脚本中写死路径
- 不要忽略构建警告
- 不要跳过签名步骤
- 不要在生产构建中包含调试符号（单独分发）

## 常用工具和命令

### CMake
```bash
# 配置
cmake -B build -G Ninja -DCMAKE_BUILD_TYPE=Release

# 构建
cmake --build build --parallel

# 安装
cmake --install build --prefix /install/path

# 运行测试
ctest --test-dir build --output-on-failure
```

### 签名
```bash
# Authenticode签名（可执行文件）
signtool sign /f cert.pfx /p password /t http://timestamp.digicert.com /fd SHA256 MyApp.exe

# 驱动签名（需要EV证书）
signtool sign /f ev_cert.pfx /p password /tr http://timestamp.digicert.com /td SHA256 /fd SHA256 driver.sys
```

### vcpkg
```bash
# 安装依赖
vcpkg install nlohmann-json:x64-windows
vcpkg install spdlog:x64-windows

# 导出依赖
vcpkg export nlohmann-json spdlog --zip

# 更新
vcpkg update
vcpkg upgrade --no-dry-run
```

---

**版本**：v1.0
**最后更新**：2025-11-06
