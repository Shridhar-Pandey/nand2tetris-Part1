# **Project 2.2 - Boolean Arithmetic and the ALU** 🔢🚀  

This project is a continuation of **Project 2.1** and focuses on **building multi-bit arithmetic circuits**, which are essential for the design of an **ALU (Arithmetic Logic Unit)**. These circuits include:

1️⃣ **Add16** → A 16-bit adder that adds two 16-bit binary numbers.  
2️⃣ **Inc16** → A 16-bit incrementer that adds `1` to a 16-bit value.  
3️⃣ **ALU** → The **Arithmetic Logic Unit**, which performs various arithmetic and logical operations, forming the computational core of the CPU.  

---

## **1️⃣ Add16 (`Add16.hdl`)**  
### **What is Add16?**  
The **Add16 chip** performs **16-bit binary addition**, meaning it takes two **16-bit inputs (`A` and `B`)** and computes their sum, outputting a **16-bit result**. It is built by **cascading multiple Full Adders**, where each bit addition considers a **carry-in from the previous bit**.

### **How It Works**  
- **Each bit** in `A` and `B` is added using a **Full Adder**, which also considers a carry from the previous stage.  
- The **first bit (LSB) does not have a carry-in** (assumed to be `0`).  
- The **carry-out** from one bit position is fed as the carry-in for the next higher bit.  

### **HDL Implementation**  
```hdl
CHIP Add16 {
    IN a[16], b[16];
    OUT out[16];

    PARTS:
    FullAdder(a=a[0], b=b[0], cin=false, sum=out[0], carry=c1);
    FullAdder(a=a[1], b=b[1], cin=c1, sum=out[1], carry=c2);
    FullAdder(a=a[2], b=b[2], cin=c2, sum=out[2], carry=c3);
    FullAdder(a=a[3], b=b[3], cin=c3, sum=out[3], carry=c4);
    FullAdder(a=a[4], b=b[4], cin=c4, sum=out[4], carry=c5);
    FullAdder(a=a[5], b=b[5], cin=c5, sum=out[5], carry=c6);
    FullAdder(a=a[6], b=b[6], cin=c6, sum=out[6], carry=c7);
    FullAdder(a=a[7], b=b[7], cin=c7, sum=out[7], carry=c8);
    FullAdder(a=a[8], b=b[8], cin=c8, sum=out[8], carry=c9);
    FullAdder(a=a[9], b=b[9], cin=c9, sum=out[9], carry=c10);
    FullAdder(a=a[10], b=b[10], cin=c10, sum=out[10], carry=c11);
    FullAdder(a=a[11], b=b[11], cin=c11, sum=out[11], carry=c12);
    FullAdder(a=a[12], b=b[12], cin=c12, sum=out[12], carry=c13);
    FullAdder(a=a[13], b=b[13], cin=c13, sum=out[13], carry=c14);
    FullAdder(a=a[14], b=b[14], cin=c14, sum=out[14], carry=c15);
    FullAdder(a=a[15], b=b[15], cin=c15, sum=out[15], carry=carryOut);
}
```
### **Where is Add16 Used?**  
✅ 16-bit Arithmetic Operations (Addition in ALU)  
✅ Memory Address Calculation  
✅ Multi-bit Binary Counters  

---

## **2️⃣ Inc16 (`Inc16.hdl`)**  
### **What is Inc16?**  
The **Inc16 chip** increments a 16-bit binary number by `1`. It is a special case of **Add16**, where the second operand is always `0000 0000 0000 0001`.

### **HDL Implementation**  
```hdl
CHIP Inc16 {
    IN in[16];
    OUT out[16];

    PARTS:
    Add16(a=in, b[0]=true, b[1:15]=false, out=out);
}
```
### **Where is Inc16 Used?**  
✅ Program Counters (PC)  
✅ Memory Addressing in CPUs  
✅ Loop Iteration in Processors  

---

## **3️⃣ ALU (`ALU.hdl`)**  
### **What is an ALU?**  
The **Arithmetic Logic Unit (ALU)** is the core component of a CPU that performs both **arithmetic and logical operations**.

### **Functions of an ALU**  
- **Arithmetic operations**: Addition, subtraction, increment, etc.  
- **Logical operations**: AND, OR, NOT, XOR, etc.  
- **Condition checking**: Setting flags for zero (`zr`), negative (`ng`), or overflow.  

### **HDL Implementation**  
```hdl
CHIP ALU {
    IN x[16], y[16], zx, nx, zy, ny, f, no;
    OUT out[16], zr, ng;

    PARTS:
    Mux16(a=x, b=false, sel=zx, out=x1);
    Not16(in=x1, out=x2);
    Mux16(a=x1, b=x2, sel=nx, out=xFinal);

    Mux16(a=y, b=false, sel=zy, out=y1);
    Not16(in=y1, out=y2);
    Mux16(a=y1, b=y2, sel=ny, out=yFinal);

    Add16(a=xFinal, b=yFinal, out=addOut);
    And16(a=xFinal, b=yFinal, out=andOut);
    Mux16(a=andOut, b=addOut, sel=f, out=aluOut);

    Not16(in=aluOut, out=notAluOut);
    Mux16(a=aluOut, b=notAluOut, sel=no, out=out);

    Or8Way(in=out[0:7], out=o1);
    Or8Way(in=out[8:15], out=o2);
    Or(a=o1, b=o2, out=o3);
    Not(in=o3, out=zr);

    Mux(a=false, b=true, sel=out[15], out=ng);
}
```
### **Where is an ALU Used?**  
✅ CPU Processing Unit  
✅ Digital Signal Processing (DSP)  
✅ Condition Checking for Branching  

---

## **📜 Notes**  
✅ **Add16** is built using Full Adders.  
✅ **Inc16** is a special case of Add16.  
✅ **ALU** is programmable and supports multiple operations.  

## **📩 Contributing**  
🔹 If you find issues or have improvements, feel free to **fork this repository** and submit a pull request!  


