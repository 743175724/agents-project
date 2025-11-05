---
description: Scan process memory for suspicious patterns
---

# Scan Memory Command

Scan target process memory for cheat signatures.

## Implementation
```cpp
void ScanMemory(HANDLE hProcess) {
    MEMORY_BASIC_INFORMATION mbi;
    LPVOID addr = 0;

    while (VirtualQueryEx(hProcess, addr, &mbi, sizeof(mbi))) {
        if (mbi.State == MEM_COMMIT && mbi.Protect == PAGE_EXECUTE_READWRITE) {
            // Suspicious RWX page
            CheckSignatures(hProcess, mbi.BaseAddress, mbi.RegionSize);
        }
        addr = (LPBYTE)addr + mbi.RegionSize;
    }
}
```
