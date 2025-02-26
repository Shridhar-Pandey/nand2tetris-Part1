# **Logic Gates: Multiplexer (MUX) & Demultiplexer (DMUX) using NAND** 🚀  

This repository contains **HDL implementations** of the **Multiplexer (MUX)** and **Demultiplexer (DMUX)** using **only NAND gates**, as part of the *Nand2Tetris* course. These gates are essential in digital logic design and serve as fundamental components in digital circuits.  

---

## **1️⃣ Multiplexer (MUX) (`Mux.hdl`)**  
### **Overview**  
A **Multiplexer (MUX)** selects one of the two input signals based on a control signal (`sel`).  
- If `sel = 0`, the output is `a`.  
- If `sel = 1`, the output is `b`.  

This is also known as a **data selector** since it chooses which input to pass to the output.

### **Truth Table**  
| A | B | Sel | MUX Output |
|---|---|-----|-----------|
| 0 | 0 | 0   | 0         |
| 0 | 1 | 0   | 0         |
| 1 | 0 | 0   | 1         |
| 1 | 1 | 0   | 1         |
| 0 | 0 | 1   | 0         |
| 0 | 1 | 1   | 1         |
| 1 | 0 | 1   | 0         |
| 1 | 1 | 1   | 1         |

### **HDL Implementation (Using NAND)**
```hdl
CHIP Mux {
    IN a, b, sel;
    OUT out;

    PARTS:
    Nand(a=sel, b=a, out=nand1);
    Nand(a=sel, b=sel, out=nand2);
    Nand(a=nand2, b=b, out=nand3);
    Nand(a=nand1, b=nand3, out=out);
}
```
### **Simulation Steps in Hardware Simulator**  
1. Open **Hardware Simulator**.  
2. Load the `Mux.hdl` file.  
3. Load the `Mux.tst` script to test the gate.  
4. Run the test and verify the expected output.  

---

## **2️⃣ Demultiplexer (`DMux.hdl`)**  
### **Overview**  
A **Demultiplexer (DMUX)** takes a **single input** and routes it to one of the **two outputs** based on a control signal (`sel`):  

- If `sel = 0`, the input is directed to output **A**.  
- If `sel = 1`, the input is directed to output **B**.  

### **Truth Table**  

| Input | Sel | A | B |
|-------|-----|---|---|
| 0     | 0   | 0 | 0 |
| 1     | 0   | 1 | 0 |
| 0     | 1   | 0 | 0 |
| 1     | 1   | 0 | 1 |

### **HDL Implementation (Using NAND)**  
```hdl
CHIP DMux {
    IN in, sel;
    OUT a, b;

    PARTS:
    Nand(a=sel, b=sel, out=nand1);
    Nand(a=in, b=nand1, out=a);
    Nand(a=in, b=sel, out=b);
}
```
### **Simulation Steps in Hardware Simulator**  
1. Open **Hardware Simulator**.  
2. Load the `DMux.hdl` file.  
3. Load the `DMux.tst` script to test the gate.  
4. Run the test and verify the expected output.  

---

## **📜 Notes**  
✅ **Multiplexer (MUX)** is used to select one input from multiple sources.  
✅ **Demultiplexer (DMUX)** is used to distribute a single input to multiple outputs.  
✅ These implementations use **only NAND gates**, demonstrating that **NAND is a universal gate**.  
✅ You can extend this project to implement **MUX4Way, DMUX4Way, and MUX8Way** for handling more inputs and outputs.  

**Happy Coding! 🚀**  

