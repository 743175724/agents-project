---
description: Create a new Unreal Engine plugin
---

# Create UE Plugin Command

Generate a new UE5 plugin scaffold.

## Steps
```bash
# Navigate to UE project
cd MyProject

# Create plugin directory
mkdir Plugins/MyPlugin

# Generate plugin files
ue4 newplugin MyPlugin
```

## Structure
```
MyPlugin/
├── Source/
│   └── MyPlugin/
│       ├── Private/
│       └── Public/
├── Resources/
└── MyPlugin.uplugin
```
