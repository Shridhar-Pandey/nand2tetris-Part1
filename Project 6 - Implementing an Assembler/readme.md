# **Project 6 - Implementing an Assembler** 🎮💾  

This project focuses on understanding how **assembly language and machine code** work by playing and analyzing the **Pong game** in **Hack Assembly Language**. This allows us to appreciate the complexity of low-level programming and the advancements in modern computing.

---

## **📌 Project Overview**  
The Pong game is written in **Hack Assembly Language**, which was **translated from Jack code**. This project provides hands-on experience with **low-level programming** and highlights the process of translating high-level code into machine-executable instructions.

---

## **🎮 Pong Game in Hack Assembly**  
The game is available in the **nand2tetris project directory**:  
### **How to Play the Pong Game**
1️⃣ Open **CPU Emulator** from the nand2tetris tools:  
2️⃣ Load `pong.asm` into the emulator.  
3️⃣ Run the emulator and play the game.  
4️⃣ Take a **screenshot** of your highest score!  

🎯 **Objective**:  
- Observe the complexity of writing a game in assembly.  
- Appreciate how high-level languages simplify development.  

---

## **📜 Hack Assembly Code (Excerpt from `Pong.asm`)**  
```asm
// This Pong game code was originally written in the high-level Jack language.
// The Jack code was then translated by the Jack compiler into VM code.
// The VM code was then translated by the VM translator into the Hack
// assembly code shown here.

@256
D=A
@SP
M=D
@133
0;JMP

@R15
M=D
@SP
AM=M-1
D=M
A=A-1
D=M-D
M=0
@R15
M=D
@SP
AM=M-1
D=M
A=A-1
D=M-D
M=0
@END_GT
D;JLE
@SP
A=M-1
M=-1
(END_GT)
@R15
A=M
0;JMP

@R15
M=D
@SP
AM=M-1
.
.
.
@122
D=A
@SP
AM=M+1
A=A-1
M=D
@SP
M=M+1
A=M-1
M=0
@SP
M=M+1
A=M-1
M=0
@SP
M=M+1
A=M-1
M=0
@63
D=A
@SP
AM=M+1
A=A-1
M=D
@27
D=A
@SP
AM=M+1
A=A-1
M=D
@12
D=A
@SP
AM=M+1
A=A-1
M=D
.
.
.
so on...
```

📌 This is just a small portion of the Pong Assembly Code. The full code is in pong.asm.

## 📂 Steps for Project Submission

### 1️⃣ Upload Pong Assembly File
- Navigate to the GitHub repository: `nand2tetris-Part1`
- Upload the `pong.asm` file.

### 2️⃣ Take a Screenshot of Your Pong Score
- Play the Pong game in the CPU Emulator.
- Capture a screenshot of your highest score.
- Upload the screenshot to the GitHub repository.

### 3️⃣ Upload the Project 6 Screenshot
- Take a screenshot of the CPU Emulator running the game.
- Upload it to the GitHub repository.

### 4️⃣ Submit Your GitHub Link
- Click **Start Assignment** in your course portal.
- Submit your GitHub repository link containing:
  - `pong.asm`
  - Screenshot of Pong score
  - Screenshot of Project 6 in CPU Emulator

---

## 🚀 Learning Outcomes
✅ Hands-on experience with Hack Assembly Language  
✅ Understanding of compilation and translation processes  
✅ Playing a game in Assembly and seeing how low-level code works  
✅ Appreciating modern programming languages  

---

## 📩 Contributing
🔹 If you find improvements or optimizations, feel free to **fork this repository** and submit a **pull request**! 🚀


