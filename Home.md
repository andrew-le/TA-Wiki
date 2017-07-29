# The Palette

Reso programs are n\*m arrays of pixels from a palette of 64 colors. Pixels are the primary functional element of a Reso program. There are 64 valid pixel colors. There are three sections of this palette: **Primary Reso**, **whitespace**, and **Extended Reso.**

Convention note: Hex color values are given in short form. #0f0 signifies #00ff00, *not* #00f000.

A lot of situations are currently undefined. The goal is to pack a lot of functionality into each color, so these undefined situations are ample spots to throw in extra functionality!

## Primary Reso palette

There are 24 colors in the primary Reso palette. These are divided by function into six hues, each with four shades.

The six hues are **Red**, **Yellow**, **Green**, **Cyan**, **Blue**, and **Magenta**. The four shades are **Saturated**, **Dark**, **Light**, and **Unsaturated**.

| Hue             | Saturated (1)    | Dark (2)  | Light (3)     | Unsaturated (4)   |
| ---             | ---              | ---       | ---           | ---               |
| **Red (R)**     | ```#f00```       | ```#800```| ```#f88```    | ```#844```        |
| **Yellow (Y)**  | ```#ff0```       | ```#880```| ```#ff8```    | ```#884```        |
| **Green (G)**   | ```#0f0```       | ```#080```| ```#8f8```    | ```#484```        |
| **Cyan (C)**    | ```#0ff```       | ```#088```| ```#8ff```    | ```#488```        |
| **Blue (B)**    | ```#00f```       | ```#008```| ```#88f```    | ```#448```        |
| **Magenta (M)** | ```#f0f```       | ```#808```| ```#f8f```    | ```#848```        |

Colors will be referred to in abbreviated form. For example, "Light Cyan" will be referred to as C3, while "Saturated Green" will be referred to as G1.

The 24 pixels in the Reso palette are divided into three types: **Wires** (red, blue, and Y1), **Input** (M2 and M3), and nodes (every other color in this palette).,

The functions of each color are as follows:

### Red:

Sections of red pixels represent wires. Wires are controlled via output (M3) pixels. Wires interact with most nodes via input pixels. Red wires interfere with adjacent red wires, but do not interfere with adjacent blue wires.

 - R1: Active wire. A wire with an active signal. Turns into R2 if no connected M3 pixels are active. Makes any connected M2 pixels active.
    - **Design decision:** Should R1 wires have resistance, similar to Minecraft redstone?
    - When R1 wires interfere, if one is active, all connected wires are turned active.
 - R2: Inactive wire. A wire with no signal. Turns into R1 if any connected M2 are active.
 - R3: *Currently undefined*
 - R4: Bridge. Propogates red wires orthogonally, allowing wires to criss-cross without interfering with one another.

### Yellow:

Yellow pixels are used to represent and transmit data. 

 - Y1: A yellow bus wire. Can carry to/from Y2 pixels.
    - When two multiple Y1 busses interfere, they take on the value of the OR of all interfering busses.
 - Y2: Marks the beginning of a data segment, defined by a chain of Y3/Y4 pixels.
    - Y3/Y4 pixels must be one dimensional, but can be bent.
    - The least significant bit is the Y3/Y4 pixel nearest the Y2 pixel.
    - Y2 can take two inputs, one from a signal wire and another from a signal wire.
        - When Y2 has an active signal (R1 or B1) connected , transform the data based off the value in the connected Y1 bus. See "actions" below.
 - Y3: Represents a "1". Can be used as a flip-flop or in a data segment with a Y2 block.
    - Outputs an active signal to any nearby M3 blocks.
    - Changes to a Y4 if it receives an active signal from an M2 block.
 - Y4: Represents a "0". Can be ysed as a flip flop or in a data segment with a Y2 block.
    - Changes to Y3 if it receives an active signal from an M2 block.

#### Actions:

These are the actions associated with each value of Y1. Note that overflow is handled by wrapping around to 0.

 - 0: Do nothing
 - 1 or none conencted: DATA ++
 - 2: DATA --
 - 3: DATA = DATA + WIRE
 - 4: DATA = DATA - WIRE
 - 5: DATA = DATA OR WIRE
 - 6: DATA = DATA AND WIRE
 - 7: DATA = DATA XOR WIRE

### Green:

Currently not defined. We're going to wait to see what would be useful to add, then fill green with it. We might make "green" pixels contain a built-in flip flop or clock. With the currently available pixels, a clock requires 6 pixels to make; a green pixel would make that less!

### Cyan:

Cyan pixels are used for logical operations on signals and busses.

When a signal and a bus is mixed for input, signals represent a bus of the same length, with an active signal representing all 1-s. If the output of such an operation is a signal, it represents the least significant bit of the result of the operation.

 - C1: "XOR", or "NOT"; represents the logical XOR of all the inputs. If there is only one input, then the output is the inverse of that input.
 - C2: "AND"; return the logical AND of all the inputs.
 - C3: *As of yet undefined.*
 - C4: *As of yet undefined.*

### Blue: 

Sections of blue pixels represent blue wires. Blue wires work similarly to red wires, with exceptions noted here. Blue wires interfere with adjacent blue wires, but do not interfere with adjacent red wires.

 - B1: Active wire. Works as red wires do.
    - Note that an active signal in a red or blue wire are both the same kind of signal.
 - B2: Inactive wire. Works as red wires do.
 - R3: Undefined.
 - R4: Bridge. Propogates red, blue and yellow wires orthogonally, allowing wires to criss-cross without interfering with one another. Note that red bridges only propogate red wires.

### Magenta:

Magenta pixels are IO pixels, allowing wires to interface with nodes or with the outside environment.

 - M1: IO node. This node interfaces with the outside program. When an active signal and a bus is input to this, the bits from the bus are streamed to a buffer, which outputs to the running environment in multiples of 8 bits.
 - M2: Node input. An active wire against this node will change the state of any adjacent nodes (or output pixels) in the next cycle.
 - M3: Node output. Any active node wil propogate its value to any adjacent output pixels, which will in turn propogate its value to any adjacent wires or input pixels.
 - M4: Control node. If this receives a signal, the program quits.


**Design question:** If a string of Y3/Y4 is connected at both ends to a Y2 pixel, what should happen?

**Design question:** If a string of Y3/Y4 has a Y2 pixel connected in the middle of the string, or even multiple ones, what should happen?

**Design question:** If a Y2 pixel is connected to a block of Y3/Y4 pixels, what should happen?

## Whitespace

Whitespace has no functional value, but can be useful for recording comments or designating sections.

There are 16 monochrome whitespace values. These are ```#000```, ```#111```, ```#222```, ```#333```, ```#444```, ```#555```, ```#666```, ```#777```, ```#888```, ```#999```, ```#aaa```, ```#bbb```, ```#ccc```, ```#ddd```, ```#eee```, and ```#fff```. Any color outside of the 64 colors is regarded as whitespace, and any image outputs will not preserve these colors, instead turning them into any one of the 16 monochrome whitespace values.

## Secondary Reso palette

There are 24 colors reserved in the secondary Reso palette. These are divided by function into six hues, each with four shades, just like the Primary palette.

These colors are reserved for extensions, but currently have no functionality associated with them.

| Hue               | Saturated (1)    | Dark (2)  | Light (3)     | Unsaturated (4)   |
| ---               | ---              | ---       | ---           | ---               |
| **Orange (O)**    | ```#f80```       | ```#840```| ```#fc8```    | ```#864```        |
| **Lime (L)**      | ```#8f0```       | ```#480```| ```#cf8```    | ```#684```        |
| **Teal (T)**      | ```#0f8```       | ```#084```| ```#8fc```    | ```#486```        |
| **Sapphire (S)**  | ```#08f```       | ```#048```| ```#8cf```    | ```#468```        |
| **Purple (P)**    | ```#80f```       | ```#408```| ```#c8f```    | ```#648```        |
| **Violet (V)**    | ```#f08```       | ```#804```| ```#f8c```    | ```#846```        |

### Secondary Color Palette Functionality

Potential future functionality that these colors could enable include:

 - More interaction outside of the circuit
 - Raspberry Pi GPIO interaction
 - Convenience nodes, such as clocks
 - 3D functionality enabled by vertical "contact" nodes
 - Automota such as Conway's Game of Life nodes
 - Special functionality nodes such as random signal generators
 - A wire that propogates a signal very slowly
 - A wire that is resistive (similar to Minecraft redstone)