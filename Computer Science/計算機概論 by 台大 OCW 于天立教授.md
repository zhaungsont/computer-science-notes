| Instructor | Institution | Course | Lecture |
|: --- :|: --- :|: --- :|: --- :|
| 于天立 助理教授 | NTU | 計算機概論 | Data Storage (1) |

---
## Binary World
- Why Use Binary? Because it's simple, logical, & unambiguous
	- As opposed to 0 ~ 9, we only have to worry about whether it's 0 or 1 in binary.
	- 0 is falsy and 1 is truthy.
	- Is 4.5 volts closer to 4 volts or 5 volts? It's ambiguous.
- Boolean operation & gates
	- Gates: 
		```
		# AND
		0 0 | -> 0
		0 1 | -> 0
		1 0 | -> 0
		1 1 | -> 1

		# OR
		0 0 | -> 0
		0 1 | -> 1
		1 0 | -> 1
		1 1 | -> 1

		# XOR (Exclusive OR, i.e., "or" in real-life meaning. Returns true only when **one** of the expression is truthy)
		0 0 | -> 0
		0 1 | -> 1
		1 0 | -> 1
		1 1 | -> 0 

		# NOT
		0 | -> 1
		1 | -> 0

		# NAND (Not AND. Flips the result of AND)
		0 0 | -> 0 -> 1
		0 1 | -> 0 -> 1
		1 0 | -> 0 -> 1
		1 1 | -> 1 -> 0
		```

### Flip-flop (正反器) [[https://en.wikipedia.org/wiki/Flip-flop_(electronics) | Wiki]]
- Purpose: stores a 0 / 1.
- Methods: A Flip-flop has two inputs.
	- Set to 0.
	- Set to 1.
	Preserve current state (0 or 1) if no input is detected.

Suppose we have a flip-flop machine (FF) with two inputs and an output: input $x$ sets FF to `1`, while input $y$ sets FF to `0`; finally $z$ will be the output. This is the chart of which every combination FF will have.

|$x$|$y$|$z$ *(output)*|
|-|-|-|
|0|0|`unchanged`|
|0|1|`0`|
|1|0|`1`|
|1|1|`undefined`|

**Explaination**
$x=0$ and $y=0$ resultsin $z$ being *unchanged* since no input is detected, and therefore $z$ should retain the last value it was given to.

`0|1` and `1|0`  are pretty self-explainatory.

`1|1` returns **undefined** because the spec does not state the expected outcome, but rather leave this to the developers to decide based on their own needs. **The result depends on how you design your circuit**.  

All diagrams below will follow the rules shown on the table above with the circuit ultimately returning to a stable state.
![[IMG_1691.jpg]]![[IMG_1692.jpg]]

**Additional Info**
- These circuit board designs are a high-level abstraction of what actually involves in a lot more components wiring. For instance, all circuits illustrated above requires constant powering, or else the state could not be preserved.
- Memorizing the diagrams above isn't necessary. The point of them is to help us understand the relationship between different input combinations.

---

## Hexadecimal
### Frequently Used Hex Value Cheat Sheet
> 前期不熟悉怎麼辦？查表就對了。

| BI | HEX | 
|: --- :|: --- :|
| 0000 | 0 | 
| 0001 | 1 | 
| 0010 | 2 | 
| 0011 | 3 | 
| 0100 | 4 | 
| 0101 | 5 | 
| 0110 | 6 | 
| 0111 | 7 | 
| 1000 | 8 | 
| 1001 | 9 | 
| 1010 | A | 
| 1011 | B | 
| 1100 | C | 
| 1101 | D | 
| 1110 | E |
| 1111 | F |


### Converting Values from Binary to Hex
Converting a string of binary value to hexadecimal is surprisingly easy.
1. Chunk every 4 binary values into a group.
2. Convert the 4-digit binary value to a Hex value.
```
0010111010110101
👇
0010 | 1110 | 1011 | 0101
👇
2 | E | B | 5
👇
2EB5
```

## Main Memory & Address
### Main Memory Cells
A bit is too small for being a memory unit, so we have **memory cells**.
- A memory cell consists of **8 bits == 1 byte**.
- When looking at the binary code of a memory cell, the leftmost digit is the **most significant**; the rightmost digit is the **least significant**.

### Memory
- Memory can be thought of as an 1 dimensional array, or drawer.
- Each memory slot has an **address** and a **value**, which are in hex notation.
- Random accessible -- you can directly point to a certain memory slot that you want to access, without having to go through other slots first (早期使用錄音帶，要播第三首歌你就要先跳過第一首和第二首)
- Access the content by the **address** (practically in binary).
- Recall the **pointer** in C/C++.

## Memory Techniques
- Random Access Memory (RAM): Memory in which individual cells can be easily accessed in any order
	- Static Memory (SRAM): like flip-flop. State will be lost if the power stops supplying.
	- Dynamic Memory (DRAM): Tiny capacitors (電容) replenished regularly by refresh circuit.
	  DRAM is the opposite of static memory: it retains state even without power. However DRAM can still suffer memory loss due to volts dropping, so the refresh circuit is introduced to replenish the capacitor as long as it detects the capacitor has volts.
	- Synchronous DRAM (SDRAM)
	- Double Data Rate (DDR)
	- Dual / Triple channel

- Capacity
	- Kilobyte = $2^{10}$ bytes = 1,024 bytes ≈ $10^3$ bytes.
	- Megabyte = $2^{20}$ bytes = 1,048,576 bytes ≈ $10^6$ bytes.
	- Gigabyte = $2^{30}$ bytes = 1,073,741,824 bytes ≈ $10^9$ bytes.
	- Terabyte = $2^{40}$ bytes

## Mass Storage
- Properties (compared with main memory)
	- Larger capacity
	- Less volatitity (較不易揮發 aka 資料比較不容易忘)
	- Slower
	- On-line or off-line (電腦是否開機)

- Types
	- Magnetic systems (hard disk, tape)
	- Optical systems (CD, DVD)
	- Flash drives

**Magnetic Disk Storage System**
![[Screen Shot 2023-01-26 at 10.23.10 PM.png]]
- Access time = seek time + rotation delay or latency time

## Buffer (緩衝區)
- Purpose: to synchronize (or to make compatible) different Read / Write mechanisms and rates.
	- Rationale: CPUs are extremely fast compared to everything else in the environment (human input, storage R/W... etc.). If CPUs were to wait for every bit of data it needs, its operation time will be dramatically slowed down as well. Therefore we'd want the storage system to batch a bunch of data and send them to the CPU once at a time, and this is where buffer comes in (一次把所有 buffer 的資料一卡車的送去給 CPU) 
- A memory area used for the temporary storage of data (ususaly as a step in transferring the data).
- Blocks of data compatible with physical records can be transferred between buffers and the mass storage system.
- Data in buffer can be referenced in terms of logical records.

## Representing Text
- ASCII (American Standard Code for Information Interchange by ANSI): **7 bits (or 8 bits with a leading `0`)**.![[Screen Shot 2023-01-26 at 10.48.51 PM.png]]
- Unicode: **16 bits**.
- ISO standard (International Organization of Standardization): **32 bits**.

## Binary ⇔ Decimal
### From Binary to Decimal
![[Screen Shot 2023-01-26 at 10.50.21 PM.png]]

### From Decimal to Binary
- Just as in decimal, keep dividing the number by 2 and record the remainders.
- **Do be careful about the order!**
![[Screen Shot 2023-01-26 at 10.52.07 PM.png]]
![[IMG_1693.jpg]]

## Representing Images
- Bit map techniques
	- Pixel: picture element
	- Colors: RGB, HSV, ...etc.
	- LCD, scanner, digital cameras, ...etc.
- Vector techniques
	- Scalable
	- TrueType, Postscript, SVG (scalable vector graphics), ...etc.
	- CAD, printers