# **Project 3.2 - Memory** 🗂️💾  

This project focuses on **expanding the memory hierarchy** from smaller storage units to larger memory architectures. These include:

1️⃣ **RAM512** → 512 memory locations, built from RAM64.  
2️⃣ **RAM4K** → 4096 memory locations, built from RAM512.  
3️⃣ **RAM16K** → 16,384 memory locations, built from RAM4K.  
4️⃣ **PC (Program Counter)** → A register that stores the memory address of the next instruction to be executed.  

These components serve as the **building blocks of RAM modules** in modern computing systems.

---

## **1️⃣ RAM512 (`RAM512.hdl`)**  
### **What is RAM512?**  
**RAM512 is a 512-location memory unit**, capable of storing 512 different **16-bit words**. It is constructed using **8 RAM64 units**, meaning it follows a **hierarchical design**.

### **How It Works**  
- Uses a **9-bit address** to select a memory location (**2⁹ = 512 locations**).  
- The **top 3 bits (`address[6..8]`)** determine which **RAM64 unit** to use.  
- The **lower 6 bits (`address[0..5]`)** select a specific register within that RAM64 unit.  

### **HDL Implementation**  
```hdl
CHIP RAM512 {
    IN in[16], load, address[9];
    OUT out[16];

    PARTS:
    DMux8Way(in=load, sel=address[6..8], a=load0, b=load1, c=load2, d=load3, e=load4, f=load5, g=load6, h=load7);
    RAM64(in=in, load=load0, address=address[0..5], out=out0);
    RAM64(in=in, load=load1, address=address[0..5], out=out1);
    RAM64(in=in, load=load2, address=address[0..5], out=out2);
    RAM64(in=in, load=load3, address=address[0..5], out=out3);
    RAM64(in=in, load=load4, address=address[0..5], out=out4);
    RAM64(in=in, load=load5, address=address[0..5], out=out5);
    RAM64(in=in, load=load6, address=address[0..5], out=out6);
    RAM64(in=in, load=load7, address=address[0..5], out=out7);
    Mux8Way16(a=out0, b=out1, c=out2, d=out3, e=out4, f=out5, g=out6, h=out7, sel=address[6..8], out=out);
}
```
### **Where is RAM512 Used?**  
✅ Buffer storage in processors  
✅ Hierarchical memory structures  
✅ Building larger RAM modules (RAM4K, RAM16K)  

---

## **2️⃣ RAM4K (`RAM4K.hdl`)**  
### **What is RAM4K?**  
RAM4K is a **4096-location memory unit**, built using **8 RAM512 units**.

### **How It Works**  
- Uses a **12-bit address** to select a memory location (**2¹² = 4096 locations**).  
- The **top 3 bits (`address[9..11]`)** determine which **RAM512 unit** to use.  
- The **lower 9 bits (`address[0..8]`)** select a specific register within that RAM512 unit.  

### **HDL Implementation**  
```hdl
CHIP RAM4K {
    IN in[16], load, address[12];
    OUT out[16];

    PARTS:
    DMux8Way(in=load, sel=address[9..11], a=load0, b=load1, c=load2, d=load3, e=load4, f=load5, g=load6, h=load7);
    RAM512(in=in, load=load0, address=address[0..8], out=out0);
    RAM512(in=in, load=load1, address=address[0..8], out=out1);
    RAM512(in=in, load=load2, address=address[0..8], out=out2);
    RAM512(in=in, load=load3, address=address[0..8], out=out3);
    RAM512(in=in, load=load4, address=address[0..8], out=out4);
    RAM512(in=in, load=load5, address=address[0..8], out=out5);
    RAM512(in=in, load=load6, address=address[0..8], out=out6);
    RAM512(in=in, load=load7, address=address[0..8], out=out7);
    Mux8Way16(a=out0, b=out1, c=out2, d=out3, e=out4, f=out5, g=out6, h=out7, sel=address[9..11], out=out);
}
```
### **Where is RAM4K Used?**  
✅ Cache memory in modern CPUs  
✅ Multi-level memory architectures  
✅ Data storage in computing systems  

---

## **3️⃣ RAM16K (`RAM16K.hdl`)**  
### **What is RAM16K?**  
RAM16K is a **16,384-location memory unit**, built using **4 RAM4K units**.

### **HDL Implementation**  
```hdl
CHIP RAM16K {
    IN in[16], load, address[14];
    OUT out[16];

    PARTS:
    DMux4Way(in=load, sel=address[12..13],
      a=sel0,
      b=sel1,
      c=sel2,
      d=sel3
    );
    
    RAM4K(in=in, load=sel0, address=address[0..11], out=r0);
    RAM4K(in=in, load=sel1, address=address[0..11], out=r1);
    RAM4K(in=in, load=sel2, address=address[0..11], out=r2);
    RAM4K(in=in, load=sel3, address=address[0..11], out=r3);
    
    Mux4Way16(
      a=r0,
      b=r1,
      c=r2,
      d=r3,
      sel=address[12..13],
      out=out);
}
```

### **How It Works**  
- Uses a **14-bit address** to select a memory location (**2¹⁴ = 16,384 locations**).  
- The **top 2 bits (`address[12..13]`)** determine which **RAM4K unit** to use.  
- The **lower 12 bits (`address[0..11]`)** select a specific register within that RAM4K unit.  

### **Where is RAM16K Used?**  
✅ Main memory (RAM) in embedded systems  
✅ Primary storage in small-scale computing devices  
✅ Multi-level memory hierarchies in modern CPUs  

---

## **4️⃣ PC (Program Counter) (`PC.hdl`)**  
### **What is a PC (Program Counter)?**  
The **Program Counter (PC)** is a specialized **register** that keeps track of the **memory address of the next instruction** to execute.
### **HDL Implementation**  
```hdl
CHIP PC {
    IN in[16],load,inc,reset;
    OUT out[16];

    PARTS:
    Inc16(in=out5,out=out1);
    Mux16(a=out5,b=out1,sel=inc,out=out2);
    Mux16(a=out2,b=in,sel=load,out=out3);
    Mux16(a=out3,b=false,sel=reset,out=out4);
    Register(in=out4,load=true,out=out5,out=out);

}
```

### **Where is the PC Used?**  
✅ Instruction execution sequencing  
✅ Handling loops and jumps in programs  
✅ CPU control flow management  

---

## **📩 Contributing**  
If you find issues or have improvements, feel free to **fork this repository** and submit a **pull request!** 🚀

