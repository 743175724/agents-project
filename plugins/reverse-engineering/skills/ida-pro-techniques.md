---
name: IDA Pro高级技巧
description: IDAPython自动化、结构恢复
version: 1.0.0
---

# IDA Pro Advanced Techniques

## IDAPython Automation
```python
import idaapi
import idc
import idautils

# Find all cross-references to a function
def find_xrefs(func_name):
    func_ea = idc.get_name_ea_simple(func_name)
    for xref in idautils.XrefsTo(func_ea):
        print(f"Called from: 0x{xref.frm:X}")

# Rename based on pattern
for func_ea in idautils.Functions():
    flags = idc.get_func_attr(func_ea, FUNCATTR_FLAGS)
    if flags & FUNC_LIB:
        continue  # Skip library functions
    # Custom renaming logic
```

## Struct Recovery
1. Identify repeated offset patterns
2. Create struct in Structures window
3. Apply struct to decompiled code
4. Refine based on usage

## Debugging Integration
- Set up remote debugging
- Attach to IDA debugger
- Use breakpoints and watches
- Analyze runtime behavior

## Tips
- Use Lumina server for function signatures
- Export/import type libraries
- Script repetitive tasks
- Keep notes in comments
