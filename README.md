# 专业软件开发智能体团队系统

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/743175724/agents-project)

全栈软件开发AI智能体团队 - 涵盖C++/Windows驱动/UI设计/游戏引擎/Web开发/安全逆向等全技术域的20个专业角色。

## 📋 目录

- [项目简介](#项目简介)
- [核心特性](#核心特性)
- [智能体角色体系](#智能体角色体系)
- [项目结构](#项目结构)
- [快速开始](#快速开始)
- [使用指南](#使用指南)
- [技术栈覆盖](#技术栈覆盖)
- [最佳实践](#最佳实践)
- [贡献指南](#贡献指南)
- [许可证](#许可证)

## 🎯 项目简介

本项目是一个完整的**智能体团队协作系统**，基于Claude Code平台打造，包含20个专业化AI角色，覆盖现代软件开发的全生命周期和全技术栈。

### 适用场景

- ✅ 复杂的C++/Windows系统开发项目
- ✅ 内核驱动程序开发与调试
- ✅ 游戏引擎集成与工具开发（UE5/Unity）
- ✅ 高性能UI开发（ImGui/ExDUIR）
- ✅ Web全栈开发（前端/后端/DevOps）
- ✅ 安全研究与逆向工程（合法合规）
- ✅ 游戏安全与反作弊系统
- ✅ 项目管理与质量保证

## ✨ 核心特性

### 1. 完整的角色体系
- **20个专业角色**，每个角色都有明确的职责边界和专业技能
- 从项目管理到具体实现，从架构设计到质量保证，全覆盖
- 角色间协作流程清晰，接口定义明确

### 2. 项目治理机制
- **项目负责人**：全局统筹、任务分配、进度跟踪、风险控制
- **技术架构师**：技术蓝图、架构评审、性能把控、技术决策
- **返工机制**：自动化质量门禁，确保交付质量
- **学习记录**：知识自动沉淀，经验可追溯复用

### 3. 知识库与模板
- 返工单模板（Rework Ticket）
- 学习记录模板（Learning Record）
- 周报/月报模板（Weekly/Monthly Report）
- 最佳实践文档库
- 代码示例与技术指南

### 4. 多技术栈支持
```
🖥️ Windows开发：C++17/20、WDK、Win32 API
🔧 驱动开发：内核编程、IOCTL、蓝屏调试
🎨 UI开发：ImGui、ExDUIR、DirectX渲染
🎮 游戏引擎：UE5、Unity、起源引擎
🌐 Web开发：React、Go、Node.js、Docker/K8s
🔐 安全逆向：IDA Pro、Ghidra、反作弊系统
📊 质量保证：自动化测试、性能分析、文档工程
```

## 👥 智能体角色体系

### 🧭 项目治理层（2个）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| 项目负责人 | 任务分配、进度跟踪、风险控制、质量把关 | RACI、OKR、返工机制、知识管理 |
| 技术架构师 | 架构设计、接口定义、性能把控、技术决策 | 系统设计、性能分析、安全架构 |

### 🧩 系统与底层开发层（2个）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| C/C++ 系统工程师 | 核心逻辑、性能优化、并发编程、接口实现 | C++17/20、STL、多线程、Win32 |
| 构建与发布工程师 | CI/CD、构建系统、版本管理、代码签名 | CMake、GitHub Actions、vcpkg |

### ⚙️ Windows 驱动与内核层（2个）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| 驱动开发工程师 | 内核模块、IOCTL、蓝屏调试、驱动签名 | WDK、WinDbg、内核编程 |
| Kernel QA工程师 | 稳定性测试、兼容性验证、Driver Verifier | HLK、内核日志分析 |

### 🖥️ UI / 桌面渲染层（3个）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| UI/UX 设计师 | 设计系统、交互体验、视觉规范 | Figma、设计理论 |
| IMGUI 工程师 | ImGui开发、高性能渲染、游戏风格UI | ImGui、DirectX、Shader |
| ExDUIR 工程师 | DirectUI、DPI适配、现代桌面UI | ExDUIR框架、GDI+ |

### 🔍 安全与逆向层（3个）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| 逆向分析工程师 | 二进制分析、脱壳、协议逆向、兼容性研究 | IDA Pro、Ghidra、x64dbg |
| 安全工程师 | 安全架构、漏洞防护、加密签名 | OWASP、密码学、代码签名 |
| 安全测试工程师 | 渗透测试、攻击模拟、漏洞验证 | Metasploit、Fuzzing |

### 🎮 游戏引擎层（3个）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| UE 工程师 | UE插件开发、蓝图扩展、性能优化 | UE5 C++、Slate、GAS |
| Unity 工程师 | Unity开发、IL2CPP优化、原生桥接 | C#、Unity API、P/Invoke |
| 引擎技术总监 | 跨引擎架构、统一接口、性能对齐 | 多引擎架构、设计模式 |

### 🌐 Web / 服务层（3个）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| 前端工程师 | React/Vue开发、状态管理、性能优化 | TypeScript、Vite、Tailwind |
| 后端工程师 | API开发、数据库设计、业务逻辑 | Go/Node.js、SQL、Redis |
| DevOps / SRE | CI/CD、容器化、监控运维、灰度发布 | K8s、Terraform、Prometheus |

### 🎮 安全与反作弊（独立系统）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| 反作弊工程师 | 反作弊系统、检测算法、对抗分析 | 内存扫描、行为分析、ML |

### ✅ 质量与文档（2个）
| 角色 | 核心职责 | 关键能力 |
|------|---------|---------|
| 测试工程师 | 功能/性能/自动化测试、缺陷跟踪 | Pytest、Selenium、JMeter |
| 技术文档工程师 | API文档、架构文档、知识库建设 | Markdown、MkDocs、UML |

## 📁 项目结构

```
my-agents-project/
├── .claude-plugin/
│   └── marketplace.json           # 插件市场清单，列出所有智能体和元数据
│
├── plugins/
│   ├── project-governance/        # 项目治理插件
│   │   ├── agents/
│   │   │   ├── project-orchestrator.md    # 项目负责人
│   │   │   └── system-architect.md        # 技术架构师
│   │   ├── commands/              # 治理相关命令
│   │   └── skills/                # 治理技能包
│   │
│   ├── windows-development/       # Windows开发插件
│   │   ├── agents/
│   │   │   ├── cpp-system-engineer.md
│   │   │   ├── driver-developer.md
│   │   │   ├── build-release-engineer.md
│   │   │   └── kernel-qa-engineer.md
│   │   ├── commands/
│   │   │   ├── build-project.md
│   │   │   └── analyze-performance.md
│   │   └── skills/
│   │       ├── cpp-best-practices.md
│   │       └── windows-kernel-basics.md
│   │
│   ├── reverse-engineering/       # 逆向工程插件
│   │   ├── agents/
│   │   │   └── reverse-engineer.md
│   │   ├── commands/
│   │   │   └── analyze-binary.md
│   │   └── skills/
│   │       └── ida-pro-techniques.md
│   │
│   ├── game-development/          # 游戏开发插件
│   │   ├── agents/
│   │   │   ├── unreal-architect.md
│   │   │   ├── unity-architect.md
│   │   │   └── engine-technical-director.md
│   │   ├── commands/
│   │   │   └── create-ue-plugin.md
│   │   └── skills/
│   │       └── unreal-gameplay-framework.md
│   │
│   ├── ui-design/                 # UI设计与开发插件
│   │   ├── agents/
│   │   │   ├── ui-ux-designer.md
│   │   │   ├── imgui-engineer.md
│   │   │   └── exduir-engineer.md
│   │   ├── commands/
│   │   └── skills/
│   │
│   ├── web-development/           # Web开发插件
│   │   ├── agents/
│   │   │   ├── frontend-engineer.md
│   │   │   ├── backend-engineer.md
│   │   │   └── devops-sre.md
│   │   ├── commands/
│   │   │   └── create-api-endpoint.md
│   │   └── skills/
│   │       └── rest-api-design.md
│   │
│   ├── security-anticheat/        # 安全与反作弊插件
│   │   ├── agents/
│   │   │   ├── anticheat-engineer.md
│   │   │   ├── security-engineer.md
│   │   │   └── blue-team-tester.md
│   │   ├── commands/
│   │   │   └── scan-memory.md
│   │   └── skills/
│   │       └── cheat-detection-patterns.md
│   │
│   └── quality-assurance/         # 质量保证插件
│       ├── agents/
│       │   ├── test-engineer.md
│       │   └── documentation-engineer.md
│       ├── commands/
│       └── skills/
│
├── templates/                     # 工作流程模板
│   ├── rework-ticket.md           # 返工单模板
│   ├── learning-record.md         # 学习记录模板
│   └── weekly-report.md           # 周报模板
│
├── knowledge/                     # 知识库（自动生成）
│   ├── monthly/                   # 月度知识汇总
│   ├── perf_tuning/               # 性能优化案例
│   └── bugfix_patterns/           # Bug修复模式
│
├── docs/                          # 项目文档
│   ├── usage-guide.md             # 使用指南
│   └── agent-roles.md             # 角色详细说明
│
└── README.md                      # 项目说明（本文件）
```

## 🚀 快速开始

### 方法1：克隆到本地使用

```bash
# 1. 克隆仓库
git clone https://github.com/743175724/agents-project.git
cd agents-project

# 2. 在Claude Code中打开项目
# 智能体会自动识别 .claude-plugin/marketplace.json

# 3. 开始使用智能体
# 在Claude Code中输入：
# "我需要开发一个Windows内核驱动，请项目负责人帮我分配任务"
```

### 方法2：安装为全局插件（推荐）

```bash
# 1. 复制到Claude Code插件目录
# Windows:
cp -r my-agents-project %USERPROFILE%\.claude\plugins\professional-agents

# macOS/Linux:
cp -r my-agents-project ~/.claude/plugins/professional-agents

# 2. 重启Claude Code
# 插件会自动加载
```

## 📖 使用指南

### 基础使用

#### 1. 调用单个智能体
```
请C++系统工程师帮我优化这段代码的性能

请驱动开发工程师解释下这个蓝屏dump文件

请前端工程师创建一个React组件
```

#### 2. 多智能体协作
```
我需要开发一个游戏反外挂系统：
1. 请项目负责人制定开发计划
2. 分配给驱动工程师开发内核模块
3. 分配给反作弊工程师设计检测算法
4. 分配给测试工程师进行验证
```

#### 3. 使用Commands
```
/build-project --config Release --platform x64
/analyze-binary target.exe
/create-ue-plugin MyGamePlugin
```

#### 4. 学习Skills
```
请教我C++最佳实践

展示Windows内核基础知识

解释UE的Gameplay框架
```

### 高级使用

#### 项目治理流程

```
1. 新项目启动
   → 项目负责人：创建项目计划和任务分解
   → 技术架构师：设计技术架构和接口规范
   → 分配任务给各专业角色

2. 开发过程
   → 各角色按职责完成任务
   → 提交代码 → 自动触发CI/CD（构建工程师）
   → 代码评审 → 架构师和负责人审核
   → 测试验证 → 测试工程师执行

3. 质量门禁
   → 性能不达标 → 触发返工单 → C++工程师优化
   → 蓝屏问题 → 驱动工程师修复 → Kernel QA验证
   → 安全漏洞 → 安全工程师修复 → Blue Team验证

4. 知识沉淀
   → 每次重要变更 → 自动生成学习记录
   → 月度汇总 → 导出到knowledge/目录
   → 最佳实践 → 更新到skills/
```

#### 返工机制示例

```markdown
# 场景：性能基准测试失败

触发条件：
- 测试工程师报告：UI帧率仅40 FPS（目标144 FPS）

自动流程：
1. 项目负责人自动创建返工单 RW-20251106-001
2. 分配给 C++工程师 和 IMGUI工程师
3. 技术架构师参与根因分析

分析结果：
- C++工程师：发现数据处理逻辑有O(n²)复杂度
- IMGUI工程师：发现每帧重建大量UI元素

解决方案：
- C++工程师：优化算法到O(n log n)
- IMGUI工程师：实现UI元素缓存和批处理

验证：
- 测试工程师：回归测试 → 帧率提升到150 FPS ✅
- 返工单关闭，经验自动记录到knowledge/perf_tuning/
```

## 🛠️ 技术栈覆盖

### Windows 系统开发
```cpp
// C++ Modern Features
auto players = GetPlayers() | std::views::filter([](const auto& p) {
    return p.isActive;
}) | std::ranges::to<std::vector>();

// Windows API
HANDLE hDevice = CreateFileW(L"\\\\.\\MyDriver", ...);
DeviceIoControl(hDevice, IOCTL_QUERY, ...);

// 内核驱动
NTSTATUS DriverEntry(PDRIVER_OBJECT DriverObject, PUNICODE_STRING RegistryPath);
```

### 游戏引擎集成
```cpp
// UE5 Plugin
UCLASS()
class UMySubsystem : public UGameInstanceSubsystem {
    GENERATED_BODY()
    // ...
};

// Unity Native Plugin
[DllImport("MyPlugin")]
private static extern int Initialize(string config);
```

### Web 全栈
```typescript
// React Frontend
const UserList: React.FC = () => {
    const [users, setUsers] = useState<User[]>([]);
    // ...
};

// Go Backend
func GetUsers(c *gin.Context) {
    var users []User
    db.Find(&users)
    c.JSON(200, gin.H{"data": users})
}
```

### 安全与逆向
```python
# IDAPython自动化
for func_ea in idautils.Functions():
    if is_crypto_function(func_ea):
        idc.set_name(func_ea, "crypto_" + hex(func_ea))
```

## 📊 最佳实践

### 1. 任务分配原则
- ✅ 明确任务边界和验收标准
- ✅ 一个任务分配给最合适的角色
- ✅ 跨角色协作需要明确接口
- ✅ 设置合理的截止时间

### 2. 代码质量标准
- ✅ 所有代码必须通过代码评审
- ✅ 单元测试覆盖率 ≥80%
- ✅ 性能基准必须达标
- ✅ 安全扫描无严重漏洞

### 3. 文档要求
- ✅ API接口必须有文档
- ✅ 架构设计必须有文档
- ✅ 重要决策必须有ADR记录
- ✅ 代码注释清晰准确

### 4. 知识管理
- ✅ 每次重要变更记录学习经验
- ✅ Bug修复总结根因和预防措施
- ✅ 性能优化记录前后对比数据
- ✅ 定期整理和分类知识库

## 🤝 贡献指南

欢迎贡献新的智能体角色、命令、技能或改进现有内容！

### 贡献流程
1. Fork本仓库
2. 创建特性分支 (`git checkout -b feature/new-agent`)
3. 提交更改 (`git commit -m 'Add new agent: XXX'`)
4. 推送到分支 (`git push origin feature/new-agent`)
5. 创建Pull Request

### 添加新智能体

1. 在适当的插件目录创建agent文件
2. 更新 `.claude-plugin/marketplace.json`
3. 添加相关的commands和skills
4. 更新README.md

### 代码规范
- Markdown文件使用UTF-8编码
- 遵循现有的文档结构和风格
- 提供清晰的示例代码
- 包含实用的最佳实践

## 📄 许可证

本项目采用 [MIT License](LICENSE) 许可证。

## 🔗 相关链接

- [Claude Code 官方文档](https://docs.claude.com/claude-code)
- [项目 Issue Tracker](https://github.com/743175724/agents-project/issues)
- [讨论区](https://github.com/743175724/agents-project/discussions)

## ⚠️ 免责声明

### 逆向工程和安全研究
本项目中的逆向工程和安全相关内容**仅用于合法合规的场景**：
- ✅ 授权的安全研究和漏洞发现
- ✅ 合法的互操作性开发
- ✅ 教育和学术研究
- ✅ CTF竞赛和安全培训

**严禁用于**：
- ❌ 软件盗版和破解
- ❌ 未授权的渗透测试
- ❌ 游戏作弊（违反ToS）
- ❌ 其他非法活动

使用者需自行承担法律责任，项目维护者不对滥用行为负责。

### 游戏安全
反作弊系统和游戏安全相关内容仅供游戏开发者和安全研究人员使用，用于：
- ✅ 开发自己的游戏保护系统
- ✅ 研究和防御作弊技术
- ✅ 教育和培训目的

**禁止用于**：
- ❌ 开发游戏作弊工具
- ❌ 破坏游戏公平性
- ❌ 违反游戏服务条款

---

## 📞 联系方式

- GitHub: [@743175724](https://github.com/743175724)
- Email: your-email@example.com

---

**最后更新**：2025-11-06
**版本**：v1.0.0

如果这个项目对你有帮助，请给个 ⭐ Star！
