1. [Operation](Operation.md)
1. [Home](..\Home.md)

![249](Images\memory_overview%201.png)![155](Images\memory_geometric.png)

# Specifications

|Input|Description|
|-----|-----------|
|Address|4-bit binary number, limited by the operand in the instruction set|
|Data In|Theoretically any integer, but in practice, a 4-bit binary integer|
|Write Enable|Boolean control input, allows for writing to memory|
|**Output**|**Description**|
|Data Out|Theoretically any integer, but in practice, a 4-bit binary integer|

# Description

Although elsewhere we attempt to mirror real-life CPU architecture, for the sake of ease, our main memory takes advantage of Blender-exclusive features. We use a grid and instance points on the vertices of the grid. Then, the z-positions of those points can be changed and accessed using an Index, which corresponds to the memory address. The advantage of this method is that it makes the main memory very scalable, and is also very compact.

Theoretically, we might be able to create memory in a "realistic" fashion, by making latches and building registers out of them and so on. However, this presents issues. This method wouldn't be scalable without duplicating nodes. Also, because the standard way to build latches is to feed the output of an OR and AND gate back into itself, and Blender doesn't let you do this by default, it would require extensive use of the simulation node, adding numerous delays of a single frame when storing information.
