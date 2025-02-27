# **Project 2.1 - Boolean Arithmetic and the ALU** 🔢🚀  

This repository contains **HDL implementations of the Half Adder and Full Adder** as part of *Nand2Tetris - Project 2.1*. These are essential building blocks in **Boolean Arithmetic** and are used in designing **ALUs (Arithmetic Logic Units)** for computing systems.

---

## **📌 Overview**  
A **Half Adder** and **Full Adder** are combinational circuits used in digital logic to **perform binary addition**. They form the fundamental components of **multipliers, CPUs, and ALUs** in modern computing.

1️⃣ **Half Adder**: Adds two binary digits but **does not handle carry input**.  
2️⃣ **Full Adder**: Adds two binary digits **with a carry input**, making it suitable for multi-bit addition.

---

## **1️⃣ Half Adder (`HalfAdder.hdl`)**  
### **What is a Half Adder?**  
A **Half Adder** adds two binary inputs (`A` and `B`) and produces:  
- A **Sum (S)** bit  
- A **Carry (C)** bit  

### **Truth Table**  
| A | B | Sum (S) | Carry (C) |
|---|---|--------|-----------|
| 0 | 0 | 0      | 0         |
| 0 | 1 | 1      | 0         |
| 1 | 0 | 1      | 0         |
| 1 | 1 | 0      | 1         |

### **HDL Implementation (Using NAND)**  
```hdl
CHIP HalfAdder {
    IN a, b;
    OUT sum, carry;

    PARTS:
    Xor(a=a, b=b, out=sum);
    And(a=a, b=b, out=carry);
}
```
## **📌 Where is a Half Adder Used?**  
✅ Basic digital circuits for simple binary addition  
✅ ALU (Arithmetic Logic Unit) design  
✅ Multipliers for computing applications  

---

## **2️⃣ Full Adder (`FullAdder.hdl`)**  
### **What is a Full Adder?**  
A **Full Adder** extends a **Half Adder** by including a **Carry-in (Cin)** input, enabling **multi-bit binary addition**.  

### **Truth Table**  

| A | B | Cin | Sum (S) | Carry (Cout) |
|---|---|-----|---------|-------------|
| 0 | 0 |  0  |    0    |      0      |
| 0 | 0 |  1  |    1    |      0      |
| 0 | 1 |  0  |    1    |      0      |
| 0 | 1 |  1  |    0    |      1      |
| 1 | 0 |  0  |    1    |      0      |
| 1 | 0 |  1  |    0    |      1      |
| 1 | 1 |  0  |    0    |      1      |
| 1 | 1 |  1  |    1    |      1      |

---

### **HDL Implementation (Using NAND)**  
```hdl
CHIP FullAdder {
    IN a, b, cin;
    OUT sum, carry;

    PARTS:
    HalfAdder(a=a, b=b, sum=s1, carry=c1);
    HalfAdder(a=s1, b=cin, sum=sum, carry=c2);
    Or(a=c1, b=c2, out=carry);
}
```

## **📌 Where is a Full Adder Used?**  
✅ **Multi-bit binary addition** (used in **CPUs and ALUs**)  
✅ **Ripple Carry Adder** (cascading multiple Full Adders for **multi-bit addition**)  
✅ **Digital signal processing (DSP)**  

---

## **🛠️ How to Run the Project in Hardware Simulator**  

### **1️⃣ Launch the Simulator**  
- Open **HardwareSimulator.exe** (Windows) or **HardwareSimulator.sh** (Linux/macOS).  

### **2️⃣ Load an HDL File**  
- Click **File > Load Chip** and select `HalfAdder.hdl` or `FullAdder.hdl`.  

### **3️⃣ Load a Test Script**  
- Click **File > Load Script** and select `HalfAdder.tst` or `FullAdder.tst`.  

### **4️⃣ Run the Simulation**  
- Click the **Run** button to execute the test.  
- Use the **Slow/Fast** slider to control execution speed.  

### **5️⃣ Verify Output**  
- Check the **output pins** in the UI.  
- If the result differs from expectations, use the `.cmp` file to debug.  

---

## **📈 Advantages of Half Adder & Full Adder**  
✔ **Efficient Binary Arithmetic**: Core component of all digital computation.  
✔ **Expandable for Multi-bit Addition**: Full Adders can be cascaded for **4-bit, 8-bit, 16-bit adders**.  
✔ **Fundamental to ALU Design**: Used in **CPU arithmetic operations**.  
✔ **Fast and Reliable**: Used in **high-speed digital processors**.  

---

## **💡 Why are Adders Important?**  

### **📟 Core of Computational Devices**  
Used in **microprocessors, ALUs, and embedded systems**.  

### **🖥️ Used in Complex Digital Circuits**  
Essential for **subtraction (via 2's complement), multiplication, and division**.  

### **⚡ Optimized for Low-Power Applications**  
Used in **battery-operated devices and low-energy DSP systems**.  

