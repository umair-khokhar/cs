# Computer Architecture
## Different Architectures
- **AMD64 (x86-64)**: Dominant in desktops and servers, 64-bit extension of x86.
- **ARM**: RISC architecture prevalent in mobile and embedded devices.
- **RISC-V**: Open ISA gaining traction in research and industry.
- **POWER**: IBM's enterprise server architecture.

## Memory Layout
+------------------+ 
| Text (Code)      | 0x4f0000 - 0x4fffff    // Your function code
|------------------|
| Data            | 0x500000 - 0x5fffff    // Constants and static variables
|------------------|
| BSS             | 0x600000 - 0x6fffff    // Uninitialized data
|------------------|
| Heap            | 0x40000000 - up        // Dynamic allocations
|        ↓        |
|        ↑        |
| Stack           | Top of memory
+------------------+