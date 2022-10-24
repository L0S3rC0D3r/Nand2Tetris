# Nand2Tetris
 Build a computer from scratch.
 
 Module 1: Boolean Functions and Gate Logic Roadmap
 
 We will start with a brief introduction of Boolean algebra, and learn how Boolean functions can be physically implemented using logic gates. We will then learn how to specify gates and chips using a Hardware Description Language (HDL), and how to simulate the behaviour of the resulting chip specifications using a hardware simulator. This background will set the stage for Project 1, in which you will build, simulate, and test 15 elementary logic gates. The chipset that you will build this module will be later used to construct the computer's Arithmetic Logic Unit (ALU) and memory system.
 
 IMPORTANT NOTES from Module 1: In order to represent a Truth table to a binary function. We could use, values in which our function is equal to 1, by appendixing expresions between each other with an and for every value 1 on our truth table output (out). In the case that the value of the expression in the variables (a, b or sel) table is zero, then the expresions are negated, this expressions then must be appended each other with an and operation for every variable, and for every value in out, should be joined  with an or operation. Just as shown in here:
 
 * Multiplexor:
 * out = a if sel == 0
 *       b otherwise
 *| sel |  a  |  b  | out |
 *|  0  |  0  |  0  |	 0  |
 *|  0  |  0  |  1  |	 0  |
 *|  0  |  1  |  0  |	 1  |
 *|  0  |  1  |  1  |	 1  |
 *|  1  |  0  |  0  |	 0  |
 *|  1  |  0  |  1  |	 1  |
 *|  1  |  1  |  0  |	 0  |
 *|  1  |  1  |  1  |	 1  |
 * (x1')(x2)x3' + (x1')(x2)(x3) + (x1)(x2')(x3) + (x1)(x2)(x3)
 * (x1')(x2)(x3+x3') + (x1)(x3)(x2+x2')
 * (x1')(x2) + (x1)(x3)
 * (sel')(a) + (sel)(b)

This same principle can be done in therms of zero values, but, they must be sum up and all functions must be appended with an and operation instead of appending each variable with and, we must do or operations, its not a tested method for now, however.

Module 2: Boolean Arithmetic and the ALU Roadmap

 Using the chipset that we've built in the previous module, we will now proceed to build a family of adders -- chips designed to add numbers. We will then take a big step forward and build an Arithmetic Logic Unit. The ALU, which is designed to perform a whole set of arithmetic and logical operations, is the computer's calculating brain. Later in the course we will use this ALU as the centerpiece chip from which we will build the computer's Central Processing Unit, or CPU. Since all these chips operate on binary numbers (0's and 1's), we will start this module with a general overview of binary arithmetic, and only then delve into building the ALU.
 
 Important notes: How a simple abstracion of an ALU is evaluated with subfunctions.
 ![image](https://user-images.githubusercontent.com/36864288/197629944-31dd09c3-59df-4fa0-af44-35489f165ea1.png)

