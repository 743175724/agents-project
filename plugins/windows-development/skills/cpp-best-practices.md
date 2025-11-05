# C++ Best Practices Skill

## Overview
Modern C++ programming best practices for high-performance Windows development.

## Key Principles

### RAII (Resource Acquisition Is Initialization)
```cpp
class FileHandle {
    HANDLE handle_;
public:
    FileHandle(const wchar_t* path) {
        handle_ = CreateFileW(path, ...);
    }
    ~FileHandle() {
        if (handle_ != INVALID_HANDLE_VALUE) {
            CloseHandle(handle_);
        }
    }
    // Disable copying, enable moving
    FileHandle(const FileHandle&) = delete;
    FileHandle(FileHandle&& other) noexcept
        : handle_(other.handle_) {
        other.handle_ = INVALID_HANDLE_VALUE;
    }
};
```

### Smart Pointers
- Use `std::unique_ptr` for exclusive ownership
- Use `std::shared_ptr` sparingly
- Avoid `std::weak_ptr` unless breaking cycles

### Modern C++ Features
- Range-based for loops
- Auto type deduction
- Lambda expressions
- Structured bindings (C++17)
- Concepts (C++20)

## Performance Tips
1. Avoid unnecessary copying (use std::move)
2. Reserve container capacity
3. Use string_view for read-only strings
4. Inline hot functions
5. Profile before optimizing
