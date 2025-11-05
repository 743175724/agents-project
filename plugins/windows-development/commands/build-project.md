---
description: Build the C++ project with specified configuration
---

# Build Project Command

Build the project using CMake and Visual Studio.

## Usage
```bash
cmake -B build -G "Visual Studio 17 2022" -A x64
cmake --build build --config Release -j
```

## Parameters
- Configuration: Debug/Release
- Platform: x86/x64
- Clean: Whether to clean before build

## Output
- Build artifacts in build/bin/
- Build log and errors
