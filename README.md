# **Nand2Tetris - Hardware Simulator** 🖥️  

This repository contains **HDL implementations of fundamental logic gates (NOT, OR, AND, XOR)** using only NAND gates for the *Nand2Tetris* course. The **Hardware Simulator** is used to test and validate these implementations, ensuring correctness before progressing to more advanced circuit designs.

---

## **📌 Overview**  
The **Nand2Tetris Hardware Simulator** is an essential tool in digital logic design that allows users to **test, debug, and visualize hardware components** before integrating them into a full-fledged computer system. It is part of the *Nand2Tetris* course and helps students and engineers understand the inner workings of digital logic.  

---

## **🎯 Key Functions**  
✅ **Loads HDL files**: Allows loading `.hdl` files containing hardware descriptions of logic gates and circuits.  
✅ **Runs test scripts**: Uses `.tst` files to simulate various input conditions and verify expected outputs.  
✅ **Compares results**: Checks against `.cmp` files to ensure correctness of gate implementations.  
✅ **Visualizes logic operations**: Displays real-time execution of logical operations through a **timing diagram**.  
✅ **Debugging tool**: Helps identify errors in gate logic and implementation.  

---

## **🛠️ Features**  
🔹 **Graphical Interface**: Displays input and output pins clearly for easy debugging.  
🔹 **Step-by-step Simulation**: Run tests at different speeds to analyze logic flow.  
🔹 **Support for Built-in and Custom Gates**: Works with **primitive gates (NAND, NOT, AND, OR, XOR, etc.)** and custom gates.  
🔹 **Script Execution**: Automates testing using `.tst` scripts for systematic validation.  
🔹 **Multiple Viewing Modes**: Displays results in **binary or decimal format**.  

---

## **🚀 How to Use the Hardware Simulator**  
1️⃣ **Launch the Simulator**  
   - Open `HardwareSimulator.exe` (Windows) or `HardwareSimulator.sh` (Linux/macOS).  

2️⃣ **Load an HDL File**  
   - Click **File > Load Chip** and select the `.hdl` file.  

3️⃣ **Load a Test Script**  
   - Click **File > Load Script** and select the `.tst` file for automated testing.  

4️⃣ **Run the Simulation**  
   - Click the **Run** button to execute the test.  
   - Use the **Slow/Fast slider** to control execution speed.  

5️⃣ **Verify Output**  
   - Check the **output pins** in the UI.  
   - If the result differs from expectations, use the `.cmp` file to debug.  

---

## **📈 Advantages of the Hardware Simulator**  
✔ **No Physical Hardware Required**: Simulate circuits without needing real components.  
✔ **Step-by-Step Debugging**: Run tests interactively to identify logic errors.  
✔ **Universal Logic Validation**: Works with any HDL design following *Nand2Tetris* syntax.  
✔ **Educational Tool**: Helps students grasp fundamental digital logic concepts.  
✔ **Supports Hierarchical Designs**: Enables testing of both elementary and complex gates.  

---

## **💡 Why is the Hardware Simulator Important?**  
1. **Fundamental in Learning Computer Architecture** 📚  
   - Helps understand how transistors and logic gates form the foundation of CPUs.  

2. **Bridges Theory and Practical Application** 🔄  
   - Allows students to implement **theory-based circuits** in a **realistic simulation environment**.  

3. **Essential for Nand2Tetris Projects** 🏗️  
   - Used in *Project 1* to test **basic gates** and later for **CPU architecture** design.  

4. **Error Detection & Debugging** 🛠️  
   - Ensures correctness before moving to hardware or FPGA implementation.  

---

## **📸 Screenshot of Hardware Simulator**  
![image](https://github.com/user-attachments/assets/c90fb482-94bb-434d-9077-9e0c2c04b6c2)


---

## **📩 Contributing**  
🔹 If you find issues or have improvements, feel free to **fork this repository** and submit a **pull request**!  

---

🚀 **Start building your own CPU from scratch using this powerful simulation tool!**  
