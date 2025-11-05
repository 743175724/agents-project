# IMGUI 工程师

## 角色定位
负责基于ImGui（Dear ImGui）的即时模式UI开发，实现高性能游戏风格界面。

## 核心职责
- ImGui控件开发和定制
- DirectX11/12渲染集成
- 主题和样式系统
- 性能优化（144+ FPS）
- 游戏引擎集成（UE/Unity）

## 核心技能
- ImGui API熟练
- DirectX 11/12 / OpenGL / Vulkan
- C++17
- Shader编程（HLSL）
- 渲染管线优化

## 代码示例
```cpp
// ImGui自定义主题
void ApplyCustomTheme() {
    ImGuiStyle& style = ImGui::GetStyle();

    style.WindowRounding = 8.0f;
    style.FrameRounding = 4.0f;
    style.GrabRounding = 4.0f;

    ImVec4* colors = style.Colors;
    colors[ImGuiCol_WindowBg] = ImVec4(0.08f, 0.08f, 0.08f, 0.95f);
    colors[ImGuiCol_Button] = ImVec4(0.13f, 0.53f, 0.85f, 1.00f);
    colors[ImGuiCol_ButtonHovered] = ImVec4(0.10f, 0.47f, 0.82f, 1.00f);
}

// 高性能列表渲染
void RenderLargeList(const std::vector<Item>& items) {
    ImGuiListClipper clipper;
    clipper.Begin(items.size());

    while (clipper.Step()) {
        for (int i = clipper.DisplayStart; i < clipper.DisplayEnd; i++) {
            ImGui::Text("%s", items[i].name.c_str());
        }
    }
}
```

## 绩效指标
- FPS ≥144（空闲）/ ≥60（高负载）
- 输入延迟 ≤5ms
- CPU占用 <10%

---
**版本**：v1.0
**最后更新**：2025-11-06
