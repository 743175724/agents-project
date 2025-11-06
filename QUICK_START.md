# 快速开始指南

## 🚀 安装方法

### 方法 1: 通过 Claude Code Marketplace（推荐）

```bash
# 在 Claude Code 中运行:
/plugin marketplace add 743175724/agents-project
```

这将自动安装所有8个插件和21个专业智能体。

### 方法 2: 手动克隆

```bash
git clone https://github.com/743175724/agents-project.git
cd agents-project
# 在 Claude Code 中打开此目录
```

### 方法 3: 复制到插件目录

```bash
# Windows
xcopy /E /I agents-project "%USERPROFILE%\.claude\plugins\professional-agents"

# macOS/Linux
cp -r agents-project ~/.claude/plugins/professional-agents
```

---

## 📦 8个可用插件

安装后，你将获得以下插件包：

| 插件名 | Agents数 | Commands | Skills | 用途 |
|--------|---------|----------|--------|------|
| **project-governance** | 2 | 0 | 0 | 项目管理与架构 |
| **windows-development** | 4 | 2 | 2 | C++/驱动开发 |
| **reverse-engineering** | 1 | 1 | 1 | 二进制分析 |
| **game-development** | 3 | 1 | 1 | UE/Unity开发 |
| **ui-design** | 3 | 0 | 0 | ImGui/ExDUIR |
| **web-development** | 3 | 1 | 1 | 前后端/DevOps |
| **security-anticheat** | 3 | 1 | 1 | 安全与反作弊 |
| **quality-assurance** | 2 | 0 | 0 | 测试与文档 |
| **总计** | **21** | **6** | **6** | - |

---

## 💡 使用示例

### 调用智能体

```
# 项目治理
请项目负责人为我的驱动项目制定开发计划
请技术架构师设计系统架构

# Windows开发
请C++工程师优化这段代码性能
请驱动开发工程师分析这个蓝屏dump
请构建工程师配置CI/CD流程

# 游戏开发
请UE工程师创建一个虚幻引擎插件
请Unity工程师优化IL2CPP性能

# Web开发
请前端工程师创建React组件
请后端工程师设计REST API
请DevOps工程师配置Kubernetes部署

# 安全与逆向
请逆向工程师分析这个二进制文件
请反作弊工程师设计检测算法
请安全工程师审查代码安全性

# 质量保证
请测试工程师编写自动化测试
请文档工程师生成API文档
```

### 执行命令

```bash
# Windows开发
/build-project --config Release --platform x64
/analyze-performance

# 逆向工程
/analyze-binary target.exe

# 游戏开发
/create-ue-plugin MyGameFeature

# Web开发
/create-api-endpoint users

# 安全
/scan-memory --process game.exe
```

### 学习技能

```
# Windows开发技能
展示C++最佳实践
讲解Windows内核基础知识

# 逆向技能
教我IDA Pro的高级技巧

# 游戏开发技能
解释UE的Gameplay Framework

# 安全技能
说明常见的作弊检测模式

# Web开发技能
讲解REST API设计原则
```

---

## 🎯 完整工作流示例

### 场景: 开发一个Windows驱动程序

```
1. 规划阶段
   "请项目负责人为驱动项目制定开发计划"
   → 任务分解、时间线、资源分配

2. 架构设计
   "请技术架构师设计驱动架构和接口"
   → 架构文档、IOCTL接口定义

3. 驱动开发
   "请驱动开发工程师实现内核模块"
   → .sys驱动代码、IOCTL实现

4. 应用层开发
   "请C++工程师实现用户态接口"
   → DeviceIoControl调用、数据结构

5. UI开发
   "请IMGUI工程师创建控制界面"
   → 高性能UI界面

6. 构建部署
   "请构建工程师配置自动化构建"
   → CMake、CI/CD、代码签名

7. 质量保证
   "请测试工程师进行稳定性测试"
   → Driver Verifier、兼容性测试

8. 文档编写
   "请文档工程师生成完整文档"
   → API文档、用户手册
```

---

## 🔧 高级用法

### 多智能体协作

```
项目负责人，请协调以下任务:
1. 驱动工程师开发内核模块
2. C++工程师开发应用层
3. 测试工程师进行验证
请制定并行开发计划
```

### 技能组合使用

```
请结合以下技能帮我:
1. C++最佳实践
2. Windows内核基础
优化这段驱动代码的性能
```

---

## ❓ 常见问题

### Q: 如何验证安装成功？

A: 在 Claude Code 中输入:
```
请项目负责人自我介绍
```

如果能正常响应，说明安装成功。

### Q: 智能体无法识别？

A: 检查:
1. marketplace.json 是否在正确位置
2. 所有 .md 文件是否有 YAML frontmatter
3. 尝试重启 Claude Code

### Q: 如何更新到最新版本？

A: 
```bash
cd agents-project
git pull origin main
```

---

## 📖 更多资源

- **完整文档**: [README.md](./README.md)
- **安装指南**: [INSTALLATION.md](./INSTALLATION.md)
- **验证报告**: [VERIFICATION_REPORT.md](./VERIFICATION_REPORT.md)
- **GitHub**: https://github.com/743175724/agents-project
- **反馈**: https://github.com/743175724/agents-project/issues

---

## 🎉 开始使用

现在你可以:

1. ✅ **安装插件**: `/plugin marketplace add 743175724/agents-project`
2. ✅ **调用智能体**: `请C++工程师帮我...`
3. ✅ **执行命令**: `/build-project`
4. ✅ **学习技能**: `展示C++最佳实践`

**版本**: v1.0.1
**最后更新**: 2025-11-06

🤖 Generated with [Claude Code](https://claude.com/claude-code)
