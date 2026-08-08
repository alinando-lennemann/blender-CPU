---
---
[Back](Arithmetic%20Logic%20Unit.md)

# Opcode Table

|Opcode|M-Low|M-High|
|------|-----|------|
|`0000`|Pass Through A|Bitwise NOT A|
|`0001`|Pass Through B|Bitwise NOT B|
|`0010`|Add|Add|
|`0011`|Subtract|Subtract|
|`0100`|Right Arithmetic Shift|Left Arithmetic Shift|
|`0101`|Right Logical Shift|Left Logical Shift|
|`0110`|Right Rotate|Left Rotate|
|`0111`|Right Rotate through Carry|Left Rotate through Carry|
|`1000`|Decrement|Increment|
|`1001`|Bitwise AND|Bitwise NAND|
|`1010`|Bitwise OR|Bitwise NOR|
|`1011`|Bitwise XOR|Bitwise XNOR|
|`1100`|Two's Complement of A|Two's Complement of B|
|`1101`|A \< B|A > B|
|`1110`|A == B|A == B|
|`1111`|Clear|Set All|

# Notes

These opcode assignments are *not* the same as the opcodes in the [Instruction Set](../Control%20Unit/Instruction%20Set.md). Raw machine code is translated to an appropriate ALU opcode using multiplexers, before being sent to the ALU itself.

Operations are assigned to optimize for circuitry reuse. For example, bitwise logical operators are complements of each others depending on the value of M. However, efficiency wasn't a priority concern for me - it's only a 4-bit CPU, and the PC I'm running the blender file on is powerful enough to reuse things a bit. A more organized node setup was a higher priority.
