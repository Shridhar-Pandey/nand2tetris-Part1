# **Project 3.1 - Memory** 🗂️💾  

This project focuses on **building fundamental memory circuits** that serve as the foundation for storing and retrieving data in a computing system. These include:

1️⃣ **Bit Circuit** → The smallest memory unit that stores a single bit.  
2️⃣ **Register** → A 16-bit memory unit that stores a multi-bit value.  
3️⃣ **RAM8** → An 8-register memory unit capable of storing 8 different 16-bit words.  
4️⃣ **RAM64** → A hierarchical memory structure with 64 memory locations.  

These components form the **building blocks of larger memory architectures**, eventually leading to **RAM and storage systems used in modern computers**.

---

## **1️⃣ Bit Circuit (`Bit.hdl`)**  
### **What is a Bit Circuit?**  
The **Bit circuit** is the **smallest memory unit** that can store **a single bit (0 or 1)**. It utilizes a **D Flip-Flop (DFF)** to hold the value across clock cycles.

### **How It Works**  
- The input `in` determines the value to store.  
- The `load` signal controls whether the bit should update.  
- The **D Flip-Flop (DFF)** maintains the stored value across clock cycles.  

### **HDL Implementation**  
```hdl
CHIP Bit {
    IN in, load;
    OUT out;

    PARTS:
    Mux(a=dffOut, b=in, sel=load, out=muxOut);
    DFF(in=muxOut, out=dffOut);
    Or(a=false, b=dffOut, out=out);
}
```
### **Where is a Bit Circuit Used?**  
✅ Building blocks of memory (Registers, RAM, Cache)  
✅ Flip-Flops in sequential circuits  
✅ Storage of temporary computation results  

---

## **2️⃣ Register (`Register.hdl`)**  
### **What is a Register?**  
A **Register** is a **16-bit storage unit** made up of 16 Bit circuits. It stores one 16-bit word, which can be loaded when the `load` signal is enabled.

### **How It Works**  
- The input (`in[16]`) is stored when `load = 1`.
- The stored value is retained across clock cycles.
- The output (`out[16]`) holds the stored value until the next load operation.

### **HDL Implementation**  
```hdl
CHIP Register {
    IN in[16], load;
    OUT out[16];

    PARTS:
    Bit(in=in[0], load=load, out=out[0]);
    Bit(in=in[1], load=load, out=out[1]);
    Bit(in=in[2], load=load, out=out[2]);
    Bit(in=in[3], load=load, out=out[3]);
    Bit(in=in[4], load=load, out=out[4]);
    Bit(in=in[5], load=load, out=out[5]);
    Bit(in=in[6], load=load, out=out[6]);
    Bit(in=in[7], load=load, out=out[7]);
    Bit(in=in[8], load=load, out=out[8]);
    Bit(in=in[9], load=load, out=out[9]);
    Bit(in=in[10], load=load, out=out[10]);
    Bit(in=in[11], load=load, out=out[11]);
    Bit(in=in[12], load=load, out=out[12]);
    Bit(in=in[13], load=load, out=out[13]);
    Bit(in=in[14], load=load, out=out[14]);
    Bit(in=in[15], load=load, out=out[15]);
}
```
### **Where is a Register Used?**  
✅ CPU registers (AX, BX, CX, etc.)  
✅ Cache memory in processors  
✅ Storage of temporary values during computations  

---

## **3️⃣ RAM8 (`RAM8.hdl`)**  
### **What is RAM8?**  
RAM8 is an **8-location memory unit** where each location stores a **16-bit value**. It consists of 8 Registers, each storing a separate word.

### **How It Works**  
- **Addressing**: Uses a 3-bit address to select a memory location (`2³ = 8 locations`).
- **Storage**: Uses Registers to hold values.
- **Loading**: The `load` signal determines whether a value should be stored in the selected register.

### **HDL Implementation**  
```hdl
CHIP RAM8 {
    IN in[16], load, address[3];
    OUT out[16];

    PARTS:
    DMux8Way(in=load, sel=address, a=sel0, b=sel1, c=sel2, d=sel3, e=sel4, f=sel5, g=sel6, h=sel7);
    Register(in=in, load=sel0, out=r0);
    Register(in=in, load=sel1, out=r1);
    Register(in=in, load=sel2, out=r2);
    Register(in=in, load=sel3, out=r3);
    Register(in=in, load=sel4, out=r4);
    Register(in=in, load=sel5, out=r5);
    Register(in=in, load=sel6, out=r6);
    Register(in=in, load=sel7, out=r7);
    Mux8Way16(a=r0, b=r1, c=r2, d=r3, e=r4, f=r5, g=r6, h=r7, sel=address, out=out);
}
```
### **Where is RAM8 Used?**  
✅ Small-scale memory units  
✅ Buffers and caches in embedded systems  
✅ Registers inside larger memory systems  

---

## **4️⃣ RAM64 (`RAM64.hdl`)**  
### **What is RAM64?**  
RAM64 is a **64-location memory unit**, built using **8 RAM8 units**, allowing it to store **64 different 16-bit words**.

### **How It Works**  
- Uses a **6-bit address** to select a memory location (`2⁶ = 64 locations`).
- **Hierarchical structure**:
  - The **first 3 bits** select a RAM8 unit.
  - The **last 3 bits** select a register inside that RAM8 unit.

### **HDL Implementation**  
```hdl
CHIP RAM64 {
    IN in[16], load, address[6];
    OUT out[16];

    PARTS:
    DMux8Way(in=load, sel=address[3..5], a=sel0, b=sel1, c=sel2, d=sel3, e=sel4, f=sel5, g=sel6, h=sel7);
    RAM8(in=in, load=sel0, address=address[0..2], out=r0);
    RAM8(in=in, load=sel1, address=address[0..2], out=r1);
    RAM8(in=in, load=sel2, address=address[0..2], out=r2);
    RAM8(in=in, load=sel3, address=address[0..2], out=r3);
    RAM8(in=in, load=sel4, address=address[0..2], out=r4);
    RAM8(in=in, load=sel5, address=address[0..2], out=r5);
    RAM8(in=in, load=sel6, address=address[0..2], out=r6);
    RAM8(in=in, load=sel7, address=address[0..2], out=r7);
    Mux8Way16(a=r0, b=r1, c=r2, d=r3, e=r4, f=r5, g=r6, h=r7, sel=address[3..5], out=out);
}
```
### **Where is RAM64 Used?**  
✅ Larger memory storage  
✅ Cache and temporary storage in processors  
✅ Building blocks for main memory  


## **📩 Contributing
Feel free to fork this repository, add new memory units, and submit a pull request! 🚀
