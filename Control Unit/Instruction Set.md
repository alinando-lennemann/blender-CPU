---
---
This instruction set is very loosely based on the instruction set for a 4-bit CPU project I found online, [The Nibbler](https://www.bigmessowires.com/nibbler/). However, the Nibbler uses 4-bit instructions, while our CPU has one 4-bit instruction and one control bit, allowing for 32 instructions (of which 16 are actually used). This allows us to take full advantage of the various operations in our ALU. All operations affect register A by default.

|Instruction|Control LOW|Control HIGH|Description|ALU Opcode|
|-----------|-----------|------------|-----------|----------|
|`0x0`|LDA|LDI|Load - either data from a RAM address, or a direct specified value.|*n/a*|
|`0x1`|STA|MOV|Store/Move - Save data from register A to RAM, or move data from register A to register B.|*n/a*|
|`0x2`|ADD|SUB|Add or Subtract values in registers A and B|`0010`/`0011`|
|`0x3`|DEC|INC|Increment or decrement|`1000`|
|`0x4`|AND|NAN|Bitwise logic operations|`1001`|
|`0x5`|ORR|NOR|Bitwise logic operations|`1010`|
|`0x6`|XOR|XNO|Bitwise logic operations|`1011`|
|`0x7`|SHR|SHL|Bit shifting (logical shift)|`0101`|
|`0x8`|ROR|ROL|Bit shifting (rotate)|`0110`|
|`0x9`|ALT|AGT|A vs. B comparisons, less than or greater than|`1101`|
|`0xA`|EQQ|*n/a*|Test for equality between A and B|`1110`|
|`0xB`|JMP|*n/a*|Unconditional jump to a new line of code|*n/a*|
|`0xC`|JIZ|JNZ|Jump if the zero output of the ALU is active/not active|*n/a*|
|`0xD`|JIC|JNC|Jump if the carry output of the ALU is active/not active|*n/a*|
|`0xE`|INP|OUT|Read inputs or write outputs. Inputs are written to Register A|*n/a*|
|`0xF`|CLR|SET|Clear or set register A to `0000` or `1111`|`1111`|

The format of an instruction is as follows:

$$
\underbrace{\text{XXX}}_{\text{Mnemonic }} \space \underbrace{\text{####}}_{\text{Operand }} \space ;
$$

If an instruction does not require an operand (as many do not), the user *must still put* a four-digit operand. It will not affect the result, but is required for the human-to-machine translation. The first instruction *must* be a blank line; when the text file is converted to a string, the newline character is assumed before every instruction.

Then, the system will translate this into binary machine-code using this format:

$$
\underbrace{\text{Control}}_{\text{Bit } [8]} \quad \underbrace{\text{Opcode}}_{\text{Bits } [7:4]} \quad \underbrace{\text{Operand}}_{\text{Bits } [3:0]}
$$

For example, the command `LDI 1001;` will be translated to `1 0000 1001`, where the instruction is 0x0, the control bit is set to HIGH, and the operand is 1001.

 > 
 > Example Code
 > 
 > ````
 > (newline)
 > LDA 1001;
 > MOV 0001;
 > ADD 0000;
 > EQQ 1101;
 > ````
