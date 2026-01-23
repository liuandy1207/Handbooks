# RISC-V Assembly

RISC stands for reduced instruction set computer

## Addition & Subtraction

```assembly
add a, b, c   # equivalent to a = b + c
sub a, b, c   # equivalent to a = b - c
```

- `add` is the mnemonic
- `b` and `c` are source operands
- `a` is the destination operand

## Register Set

RISC-V has 32 registers used to hold the most commonly used operands.
stored in the "register file"
<img width="638" height="542" alt="image" src="https://github.com/user-attachments/assets/3ca72958-30b7-453f-8bfe-2eec6488228b" />

## Immediate Operands

Immediates are constant values that are immediately available from the instruction and do not require registor or memory access. <br>
immediates are 12 bit two's complement numbers (sign extended to 32 bit)

- use `0x` prefix to indicate hex values
- use `0b` prefix to inidicate binary values

```assembly
# "add immediate", adds an immediate to a register
# also used to initialize registers to small constants
addi x, zero, 0     # equivalant to x = 0

# "load upper immediate",loads a 20 bit immediate into the most signficatn 20 bits and zeros elsewhere
# used to create larger constants for addi
lui a, 0x13742     # equivalent to a = 0x13742
# note: if the 12-bit immediate in the subequetn addi is negative, then you must increment the 20-bit immediate by 1
```

(because negative immediate is sign extended which messes with the first 20 bits)

## Memory

larger and slower than the register file. <br>
byte-addressable memory => each byte in memory has a unique address <br>
32-bit word address and the data value in hexadecimal.
<img width="549" height="259" alt="image" src="https://github.com/user-attachments/assets/0aeb24ea-a41c-482a-b4e4-0dc021eaba5d" />

```assembly
# "load word", reads a data word from memory into a register
# memory address is specified by an offset added to a base register
lw s7, 8(zero)    # offset 8 from base register 0 gives you word 2

# "store word", writes a data word from a register into memory
sw s7, 8(zero)

```
