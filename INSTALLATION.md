# 安装指南

## 方法 1：从 GitHub 克隆使用（推荐）

```bash
# 克隆仓库
git clone https://github.com/743175724/agents-project.git

# 进入目录
cd agents-project

# 在 Claude Code 中打开此目录
# Claude Code 会自动识别 plugins/ 目录中的智能体
```

## 方法 2：作为 Claude Code 插件安装

### 选项 A：复制到用户插件目录

```bash
# Windows
xcopy /E /I agents-project "%USERPROFILE%\.claude\plugins\professional-agents"

# macOS/Linux
cp -r agents-project ~/.claude/plugins/professional-agents
```

### 选项 B：链接方式（便于开发）

```bash
# Windows (需要管理员权限)
mklink /D "%USERPROFILE%\.claude\plugins\professional-agents" "C:\path\to\agents-project"

# macOS/Linux
ln -s /path/to/agents-project ~/.claude/plugins/professional-agents
```

## 方法 3：直接使用项目中的智能体

如果你的项目已经在使用 Claude Code，可以将 `plugins/` 目录复制到你的项目根目录：

```bash
# 从 agents-project 复制 plugins 目录到你的项目
cp -r agents-project/plugins /path/to/your/project/
```

## 验证安装

安装后，在 Claude Code 中你应该能够：

1. **调用智能体**
   ```
   请项目负责人帮我制定开发计划
   请C++工程师优化这段代码
   ```

2. **使用命令**
   ```
   /build-project --config Release
   /analyze-binary target.exe
   ```

3. **查看技能**
   ```
   展示C++最佳实践
   讲解Windows内核基础
   ```

## 文件结构说明

安装后的目录结构：

```
.claude/plugins/professional-agents/  (或 your-project/plugins/)
├── project-governance/
│   ├── agents/
│   │   ├── project-orchestrator.md
│   │   └── system-architect.md
│   ├── commands/
│   └── skills/
├── windows-development/
│   ├── agents/
│   ├── commands/
│   └── skills/
├── game-development/
├── ui-design/
├── web-development/
├── reverse-engineering/
├── security-anticheat/
└── quality-assurance/
```

## 智能体清单

安装完成后，你将拥有以下 **21个专业智能体**：

### 项目治理 (2)
- 项目负责人
- 技术架构师

### Windows开发 (4)
- C/C++ 系统工程师
- 驱动开发工程师
- 构建与发布工程师
- Kernel QA工程师

### UI设计 (3)
- UI/UX 设计师
- IMGUI 工程师
- ExDUIR 工程师

### 安全与逆向 (3)
- 逆向分析工程师
- 安全工程师
- 安全测试工程师

### 游戏开发 (3)
- UE 工程师
- Unity 工程师
- 引擎技术总监

### Web开发 (3)
- 前端工程师
- 后端工程师
- DevOps/SRE 工程师

### 安全反作弊 (1)
- 反作弊工程师

### 质量保证 (2)
- 测试工程师
- 技术文档工程师

## 使用示例

### 完整项目流程

```
1. "请项目负责人为我的驱动项目制定开发计划"
   → 项目负责人会拆解任务并分配给各角色

2. "请技术架构师设计系统架构"
   → 架构师提供架构文档和接口设计

3. "请驱动开发工程师实现内核模块"
   → 驱动工程师编写.sys驱动代码

4. "请C++工程师实现用户态接口"
   → C++工程师实现应用层代码

5. "请构建工程师配置CI/CD"
   → 构建工程师设置自动化构建

6. "请测试工程师进行验证"
   → 测试工程师执行测试用例

7. "请文档工程师编写API文档"
   → 文档工程师生成完整文档
```

## 故障排除

### 智能体无法识别

1. **检查文件格式**
   - 确保所有 `.md` 文件包含 YAML frontmatter
   - frontmatter 格式：
     ```yaml
     ---
     name: 智能体名称
     description: 描述
     category: 分类
     version: 1.0.0
     ---
     ```

2. **检查目录结构**
   - 确保 `plugins/` 目录在正确位置
   - 每个插件必须有 `agents/`, `commands/`, `skills/` 子目录

3. **重启 Claude Code**
   - 有时需要重启以重新加载插件

### Commands 无法执行

Commands 需要以 `/` 开头，例如：
```
/build-project
```
而不是：
```
build-project
```

## 更新

保持智能体系统最新：

```bash
cd agents-project
git pull origin main
```

## 卸载

删除插件目录：

```bash
# Windows
rmdir /S "%USERPROFILE%\.claude\plugins\professional-agents"

# macOS/Linux
rm -rf ~/.claude/plugins/professional-agents
```

## 支持

- 问题反馈: https://github.com/743175724/agents-project/issues
- 讨论区: https://github.com/743175724/agents-project/discussions

---

**版本**: v1.0.0
**最后更新**: 2025-11-06
