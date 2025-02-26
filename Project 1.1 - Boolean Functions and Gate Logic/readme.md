# **Logic Gates: NOT & OR** 🚀  

This repository contains **HDL implementations** of the **NOT** and **OR** gates using **only NAND gates**, as part of the *Nand2Tetris* course. These gates are essential in digital logic design and serve as building blocks for more complex circuits.  

---

## **1️⃣ NOT Gate (`Not.hdl`)**  
### **Overview**  
The **NOT gate (Inverter)** produces the opposite of its input:  

- If the input is `1`, the output is `0`.  
- If the input is `0`, the output is `1`.  

### **HDL Implementation**  
```hdl
CHIP Not {
    IN in;
    OUT out;

    PARTS:
    Nand(a=in, b=in, out=out);
}
```



### **Simulation Steps in Hardware Simulator**  
1. Open **Hardware Simulator**.  
2. Load the `Not.hdl` file.  
3. Load the `Not.tst` script to test the gate.  
4. Run the test to verify the expected output:  
   - `0 → 1`  
   - `1 → 0`  

---

## **2️⃣ OR Gate (`Or.hdl`)**  
### **Overview**  
The **OR gate** outputs `1` if at least one of its inputs is `1`:  

| A | B | A OR B |
|---|---|--------|
| 0 | 0 | 0      |
| 0 | 1 | 1      |
| 1 | 0 | 1      |
| 1 | 1 | 1      |

### **HDL Implementation (Using NAND)**  
```hdl
CHIP Or {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=a, out=nota);
    Nand(a=b, b=b, out=notb);
    Nand(a=nota, b=notb, out=out);
}
```

### **Simulation Steps in Hardware Simulator**  
1. Open **Hardware Simulator**.  
2. Load the `Or.hdl` file.  
3. Load the `Or.tst` script to test the gate.  
4. Run the test and verify the outputs.  

---

## **📜 Notes**  
✅ These implementations use **only NAND gates**, demonstrating that **NAND is a universal gate**.  
✅ You can extend this project to implement other gates like **AND, XOR, and NOR**.  
