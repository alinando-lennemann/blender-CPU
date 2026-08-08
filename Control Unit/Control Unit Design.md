# The 3-Step Cycle
A two-bit counter is used in order to track what step of the instruction cycle the CPU is on. The assignments are as follows:

| Counter Output | CPU Step |
| -------------- | -------- |
| 00             | Decode   |
| 01             | Execute  |
| 10             | Jump     |
This two-bit synchronous counter is built of JK flip-flops wired together. A JK flip flop is wired up using [the truth table](https://www.geeksforgeeks.org/digital-logic/what-is-jk-flip-flop/), the result of which is fed into a switch node that only switches if it is the rising edge of the clock cycle. Otherwise, the previous state is stored.

Because these JK Flip-flops are not designed with reset pins, the wiring for the clock is slightly different in order to make it count from 00 to 10 and reset.

![[control_stepconditionals.png]]
# Instruction Decoding
Instructions are uploaded in the form of a .txt file. We slice this text file at designated increments to isolate individual lines, storing a character index in order to iterate through the lines (synced to the rising edge of the clock AND the appropriate clock cycle from our counter.) Then, we slice that line further to isolate the 3-character instruction mnemonic, before matching it with appropriate binary instruction code output.

![[control_decoder.png]]

Then, recombining the strings, we have successfully converted human-readable code into binary machine code. 

# Registers and Memory
Registers are designed identically to the [[memory.md]], just with one single storage point instead of multiple addresses. Register A is our primary accumulator. Most instructions load things into Register A or use Register A's value. In fact, the only time Register B is written to or read from is through two-operand ALU operations and when loading it (which can only be done through Register A).

We load registers using switch nodes, that switch outputs based on a Boolean logical selection. If the opcode matches the appropriate instruction (checked using multiplexers) and the clock is at the appropriate state, then the existing register value is overridden for the new one.

![[control_registers.png|518]]

# Jump Instructions
Jump instructions override the existing stored [[Control Unit Design.md#Instruction Decoding|character index]], sometimes based on conditionals (like whether the carry signal is active), and sometimes unconditionally. Again, this is done with a switch node that only activates when the opcode matches the appropriate instruction.

![[control_jump.png|514]]