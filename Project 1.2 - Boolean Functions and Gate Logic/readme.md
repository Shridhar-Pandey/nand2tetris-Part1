# **Logic Gates: AND & XOR** 🚀  

This repository contains **HDL implementations** of the **AND** and **XOR** gates using **only NAND gates**, as part of the *Nand2Tetris* course. These gates are essential in digital logic design and serve as building blocks for more complex circuits.  

---

## **1️⃣ AND Gate (`And.hdl`)**  
### **Overview**  
The **AND gate** outputs `1` only if both inputs are `1`:  

| A | B | A AND B |
|---|---|---------|
| 0 | 0 | 0       |
| 0 | 1 | 0       |
| 1 | 0 | 0       |
| 1 | 1 | 1       |

### **HDL Implementation (Using NAND)**  
```hdl
CHIP And {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=b, out=nandOut);
    Not(in=nandOut, out=out);
}
```
### **Simulation Steps in Hardware Simulator**  
1. Open **Hardware Simulator**.  
2. Load the `And.hdl` file.  
3. Load the `And.tst` script to test the gate.  
4. Run the test and verify the expected output.  

---

## **2️⃣ XOR Gate (`Xor.hdl`)**  
### **Overview**  
The **XOR gate (Exclusive OR)** outputs `1` if exactly **one** input is `1`:  

| A | B | A XOR B |
|---|---|--------|
| 0 | 0 | 0      |
| 0 | 1 | 1      |
| 1 | 0 | 1      |
| 1 | 1 | 0      |

### **HDL Implementation (Using NAND)**  
```hdl
CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=b, out=nand1);
    Nand(a=a, b=nand1, out=nand2);
    Nand(a=b, b=nand1, out=nand3);
    Nand(a=nand2, b=nand3, out=out);
}
```
### **Simulation Steps in Hardware Simulator**  
1. Open **Hardware Simulator**.  
2. Load the `Xor.hdl` file.  
3. Load the `Xor.tst` script to test the gate.  
4. Run the test and verify the outputs.  

---

## **📜 Notes**  
✅ These implementations use **only NAND gates**, demonstrating that **NAND is a universal gate**.  
✅ You can extend this project to implement other gates like **MUX, DMUX, and NOR**.  

