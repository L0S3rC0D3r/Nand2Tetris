# Nand2Tetris
 Build a computer from scratch.
 
 Module 1: Boolean Functions and Gate Logic Roadmap
 
 We will start with a brief introduction of Boolean algebra, and learn how Boolean functions can be physically implemented using logic gates. We will then learn how to specify gates and chips using a Hardware Description Language (HDL), and how to simulate the behaviour of the resulting chip specifications using a hardware simulator. This background will set the stage for Project 1, in which you will build, simulate, and test 15 elementary logic gates. The chipset that you will build this module will be later used to construct the computer's Arithmetic Logic Unit (ALU) and memory system.
 
 IMPORTANT NOTES from Module 1: In order to represent a Truth table to a binary function. We could use, values in which our function is equal to 1, by appendixing expresions between each other with an and for every value 1 on our truth table output (out). In the case that the value of the expression in the variables (a, b or sel) table is zero, then the expresions are negated, this expressions then must be appended each other with an and operation for every variable, and for every value in out, should be joined  with an or operation. Just as shown in here:
 ```
 /* Computes the sum of three bits.
 |  a  |  b  |  c  |   sum   |  carry  |
 |  0  |  0  |  0  |    0    |    0    |
 |  0  |  0  |  1  |    1    |    0    |
 |  0  |  1  |  0  |    1    |    0    |
 |  0  |  1  |  1  |    0    |    1    |
 |  1  |  0  |  0  |    1    |    0    |
 |  1  |  0  |  1  |    0    |    1    |
 |  1  |  1  |  0  |    0    |    1    |
 |  1  |  1  |  1  |    1    |    1    |

    x1    x2    x3      y1       y2

 y1 = (x1')(x2')(x3) + (x1')(x2)(x3') + (x1)(x2')(x3') + (x1)(x2)(x3)
 y1 =  (x1')(x2'*x3 + x2x3') + (x1)(x2'*x3'+x2*x3)
 INVERSE BOOLEAN LAW:  A + A' = 1
 y1= (x1')(xor(b, c)) + (x1)(1)
 y1= (x1')(x2'*x3 + x2x3') + x1
sum = a'(b'*c + b*c') + a

 y2 = (x1')(x2)(x3) + (x1)(x2')(x3) + (x1)(x2)(x3') + (x1)(x2)(x3)
 y2 = (x2*x3)(x1 + x1') + x1(x2'*x3 + x2*x3')
 y2 = (x2*x3)(1) + x1(x2'x3 + x2*x3')
     c  And  b  Or  a And HalfAdder(a=b, b=c, sum=sumOfbc, carry=carryOfbc)
                          Xor(a=b, b=c, out= x2'x3 + x2*x3')  And(a=b. b=c, out=carryOfbc)
carry = c And b   Or  a and Xor(b, c,  )
        carryOfcb  Or carryOfabc
carry = b*c + a(b'*c + b*c')
*/
```
This same principle can be done in therms of zero values, but, they must be sum up with or operations and all functions must be appended with an and operation instead of appending each variable with and or operation. This method is not tested for now, however.

Module 2: Boolean Arithmetic and the ALU Roadmap

 Using the chipset that we've built in the previous module, we will now proceed to build a family of adders -- chips designed to add numbers. We will then take a big step forward and build an Arithmetic Logic Unit. The ALU, which is designed to perform a whole set of arithmetic and logical operations, is the computer's calculating brain. Later in the course we will use this ALU as the centerpiece chip from which we will build the computer's Central Processing Unit, or CPU. Since all these chips operate on binary numbers (0's and 1's), we will start this module with a general overview of binary arithmetic, and only then delve into building the ALU.
 
 Important notes: 
```
/**
 * Computes the sum of three bits.
 |  a  |  b  |  c  |   sum   |  carry  |
 |  0  |  0  |  0  |    0    |    0    |
 |  0  |  0  |  1  |    1    |    0    |
 |  0  |  1  |  0  |    1    |    0    |
 |  0  |  1  |  1  |    0    |    1    |
 |  1  |  0  |  0  |    1    |    0    |
 |  1  |  0  |  1  |    0    |    1    |
 |  1  |  1  |  0  |    0    |    1    |
 |  1  |  1  |  1  |    1    |    1    |

    x1    x2    x3      y1       y2

 y1 = (x1')(x2')(x3) + (x1')(x2)(x3') + (x1)(x2')(x3') + (x1)(x2)(x3)
 y1 = (x3)(x1'*x2'+x1*x2) + (x2)(x1*x3+x1'*x3')
 INVERSE BOOLEAN LAW:  A + A' = 1
 y1 = (x3)(1) + (x2)(1)
 y1 = x3 + x2

 y2 = (x1')(x2)(x3) + (x1)(x2')(x3) + (x1)(x2)(x3') + (x1)(x2)(x3)
 y2 = (x2*x3)(x1 + x1') + x1(x2'*x3 + x2*x3')
 y2 = (x2*x3)(1) + x1(x2'x3 + x2*x3')
     b  And  c  Or  a And HalfAdder(a=b, b=c, sum=sumOfbc, carry=carryOfbc)
                          Xor(a=b, b=c, out= x2'x3 + x2*x3')  And(a=b. b=c, out=carryOfbc)
*/
```
Images: (1) How a simple abstracion of an ALU is evaluated with subfunctions. (2) quick overview, (3) Truth table

![image](https://user-images.githubusercontent.com/36864288/197653284-1047a268-782d-4c99-9542-4c61a2dada8a.png)
(1)
![image](https://user-images.githubusercontent.com/36864288/197629944-31dd09c3-59df-4fa0-af44-35489f165ea1.png)
(2)
![image](https://user-images.githubusercontent.com/36864288/198144741-430ca0ad-5750-4e70-83b7-b2398dfbf896.png)
(3)


Literally, hands down to the the most important function of all boolean functions: Multiplexing. It involves data, and can be intertwined for desition making in programming:

   Mux16(a=x, b=false, sel=zx, out=zxOut);        // (1) if (zx == 1) set x = 0        // 16-bit constant

   Not16(in=zxOut, out=notzxOut);                 // (2) if (nx == 1) set x = !x       // bitwise not
   Mux16(a=zxOut, b=notzxOut, sel=nx, out=nxOut); // (3)

   Mux16(a=y, b=false, sel=zy, out=zyOut);        // (4) if (zy == 1) set y = 0        // 16-bit constant

   Not16(in=zyOut, out=notnyOut);                 // (5) if (ny == 1) set y = !y       // bitwise not
   Mux16(a=zyOut, b=notnyOut, sel=ny, out=nyOut); // (6)

Its REALLY INTERESTING, how a computer makes calculations before the task at hand... This makes the process of simulation and abstract thought harder to implement? What does it means? And what did just happend in here!!:
```
Mux16(a=outF, b=notoutF, sel=no, out=out, out[0..7]= tryhard1, out[8..15]=tryhard2, out[15] = ng);     // WHAT THE H-A-CK (11) if (out < 0) set ng = 1
```
