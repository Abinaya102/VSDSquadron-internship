# VSDSquadron-internship
This is the VSDSquadron research internship program which is done using RISC-V development board. This board is powered by CH32VOO3F4U6 chip with 32 bit RISC-V core based tool. It includes a built-in factory-trimmed 24MHz RC oscillator, 128KHz RC oscillator and a 24MHz oscillator for varing clock requirements. It offers multiple communication protocol including US-ART, 12C and SPI for versatile connectivity. It is eqipped with 2KB SRAM for volatile data storage, 16KB flash memory and 1920B for bootloader functionalities.
# TASK 1
# C code to RISC-V tool
In this section, we'll explore how C code is reprsented in the instruction set of the RISC-V tool. We'll start by testing the GCC compiler with a simple program that counts the sum of numbers from 1 to n.
STEP 1:
Write the C program that counts the sum of numbers from 1 to n in the Leafpad editor(open source graphical text editor) and save the code.
![code](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/d5af9602-97e7-4516-8395-c12af510e131)
Compile the code using GCC editor and ouput is generated using "./a.out" command.
![VirtualBox_vsdworkshop_23_06_2024_23_22_19](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/4025d860-66c0-4584-8072-3ee1d7a0e023)
The sum of the numbers from 1 to 5 is 15 and it is obtained successfully.

The next step is to convert the C code according to RISC-V tool instruction set we have seperate steps which are as follows.

STEP 2:
Now to run the same program which counts the sum from 1 to n is run through RISC-V by the following command:

        riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
        
where lp is the long point integer of 64 bit
     -O1 is the options to compile the code using gcc compiler
     march is the architecture type
     -o is the output file
     rv64 is the RISC-V of 64 bit

![command](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/f44df7ea-9a57-4b8f-b7b9-4009d214ada4)

STEP 3:
Now this will provide the output. Then go to another tab to check the assembly code for the given C program and the command is as follows

        riscv64-unknown-elf-objdump -d sum1ton.o
Then open the output with the less editor, with the command
        
         riscv64-unknown-elf-objdump -d sum1ton.o | less
To check the output of the main section use command /main
![main](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/6fc70654-16fb-4422-8ef2-96cdd0cb30bc)

Now we can see that the address of the main section is 10184 but the quick way to find the number of instructions are by using a hexadecimal calculater and subracting the address numbers of the left most ends and dividing the result by 4, since each consecutive address value varies by 4.

![WhatsApp Image 2024-06-24 at 1 43 32 AM](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/f3b985b6-4950-472b-b9b8-5db032e5ddd3)
Thus the number of instruction set is found to be 15 both theoretically and practically.

STEP 4:
In the previous case we used -O1 as the optional condition to compile the code whereas now we use -Ofast conditon and the command is as follows:

        riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
Now on obtaing the output of the main section we get,
![WhatsApp Image 2024-06-24 at 1 53 17 AM](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/66aee74e-18db-42ff-bf17-6f653b467fda)
Thus we can see that on changing the option condition the number of instruction set is reduced to 12 respectively.

# TASK 2
Task 2 is to write a C program for the project "Clock cycle Divider" and compile it using RISC-V GCC
A clock divider circuit creates a low frequency clock signals from the input clock source. The divider circuit counts input clock cycles, and drive the output clock low and then high for some of the input clock cycle.

The code which I have used to implement the clock cycle divider is:
![clockcode](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/01443400-7e7c-4dd6-93fa-29767bd907c9)

The output of this C code is:
![clockop](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/c3a63be4-131d-417e-a2d2-a649dc335969)

Now, we are implementing the code in RISC-V GCC compiler:
![risc ss](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/8a6e669b-e1fa-4634-9748-fc8ab8d7fe4d)

The next step is to implement and get the output for the assembly code same as we did in task 1.
![prefinal](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/43b9ea92-d6fc-45fe-a24e-63c94dc00937)

![finalopt](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/8a259514-0bab-4a8d-bb8b-4415a26fa0c4)

# TASK 3
Task 3 is to compile the C code and find the spike simpulation and further we have to compare the   -Ofast   and   -O1 conditions seperately.
The entire process of task 3 is basically to debug using spike command.

STEP 1:
The first step is to compile the C code using "gcc clockcycledivider.c" and  "./a.out" command and compile the same code in RISC-V GCC compiler using
    
    spike pk clockcycledivider.o
command and get the same output.
![task 3la1](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/dfb85a3b-3546-42f4-b29b-287f49c82f00)

STEP 2:
In this step we are opening the object dump elements of this code using

    riscv64-unknown-elf-objdump -d clockcycledivider.o | less
command as we saw earlier.
![task3la2](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/67558822-57e5-41b2-9c2d-81317abbdeb9)

STEP 3:
Now to debug all these object dump lines we need to open a debugger using the following command:

    spike pk -d clockcycledivider.o
Lets say now we have to run the debugger till program counter 100b0, fpr this we are using the command

    until pc 0 100b0
where pc denotes the program counter and after these counter values the program runs manually. Then before modifing the values we are going to find the contents of first counter value a1 using command:

    reg 0 a1
Thus the contents are displayed and we can observe that the obtained output of this command is of 64 bits denoting the 64 bit RISC-V simulation. Then on pressing enter we get the next instruction and the "lui" in each instruction is denoted as load upper immediate.
![task3la3](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/37c5aaee-3b1f-4d43-8fee-fa390d1a34aa)


STEP 4:
![task3la4](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/bd0a2a07-5c8a-453d-b2bd-79110789c218)
In this step we can see that the hexadecimal value of the stack pointer is reduced by 10

# TASK 4
# RISC-V instruction type

RISC-V instructions can be categorized into several types based on their format:

R-type: Register-Register operations
I-type: Immediate operations
S-type: Store operations
B-type: Branch operations
U-type: Upper immediate operations
J-type: Jump operations
Below are the instructions with their types and 32-bit instruction codes in the format for each type:

1. ADD r6, r2, r1
* Type: R
* Format: funct7 rs2 rs1 funct3 rd opcode
* Binary: 0000000 00001 00010 000 00110 0110011
* 32-bit Pattern: 0x0020B033

  
2. SUB r7, r1, r2
* Type: R
* Format: funct7 rs2 rs1 funct3 rd opcode
* Binary: 0100000 00010 00001 000 00111 0110011
* 32-bit Pattern: 0x4020A033

  
3. AND r8, r1, r3
* Type: R
* Format: funct7 rs2 rs1 funct3 rd opcode
* Binary: 0000000 00011 00001 111 01000 0110011
* 32-bit Pattern: 0x0030F033

  
4. OR r9, r2, r5
* Type: R
* Format: funct7 rs2 rs1 funct3 rd opcode
* Binary: 0000000 00101 00010 110 01001 0110011
* 32-bit Pattern: 0x0050D033

  
5. XOR r10, r1, r4
* Type: R
* Format: funct7 rs2 rs1 funct3 rd opcode
* Binary: 0000000 00100 00001 100 01010 0110011
* 32-bit Pattern: 0x0040A833
6. SLT r11, r2, r4
* Type: R
* Format: funct7 rs2 rs1 funct3 rd opcode
* Binary: 0000000 00100 00010 010 01011 0110011
* 32-bit Pattern: 0x0040D233
  
7. ADDI r12, r4, 5
* Type: I
* Format: imm[11:0] rs1 funct3 rd opcode
* Binary: 000000000101 00100 000 01100 0010011
* 32-bit Pattern: 0x00520613
  
8. SW r3, r1, 2
* Type: S
* Format: imm[11:5] rs2 rs1 funct3 imm[4:0] opcode
* Binary: 0000000 00010 00001 010 00011 0100011
* 32-bit Pattern: 0x0020A023
  
9. SRL r16, r14, r2
* Type: R
* Format: funct7 rs2 rs1 funct3 rd opcode
* Binary: 0000000 00010 01110 101 10000 0110011
* 32-bit Pattern: 0x0020F933
  
10. BNE r0, r1, 20
* Type: B
* Format: imm[12|10:5] rs2 rs1 funct3 imm[4:1|11] opcode
* Binary: 000001 00001 00000 001 0010 1100011
* 32-bit Pattern: 0x01406063
  
11. BEQ r0, r0, 15
* Type: B
* Format: imm[12|10:5] rs2 rs1 funct3 imm[4:1|11] opcode
* Binary: 000000 00000 00000 000 1111 1100011
* 32-bit Pattern: 0x00F06063
  
12. LW r13, r1, 2
* Type: I
* Format: imm[11:0] rs1 funct3 rd opcode
* Binary: 000000000010 00001 010 01101 0000011
* 32-bit Pattern: 0x0020A203
  
13. SLL r15, r1, r2
* Type: R
* Format: funct7 rs2 rs1 funct3 rd opcode
* Binary: 0000000 00010 00001 001 01111 0110011
* 32-bit Pattern: 0x0020A533

# TASK 5
Task 5 is to use this RISC-V core verilog netlist and testbench for the functional simulation experiment
Since we are not building a RISC-V core in this project instead we are using a prebuilt micro architecture and test bench. Let us start this by installing the tools:
 * iverilog
 * gtkwave
 ,using the command:

               sudo apt update
               sudo apt install iverilog gtkwave
   After installing the tools, we have to clone a repo containing the verilog codes for the RISC-V core. Using the command:

           git clone https://github.com/vinayrayapati/rv32i.git
   And it is also necessary to create a new directory and move the verilog files to the new directory. This is done using:

          mkdir vys_rv32
          cd vys_rv32
          cp ../rv32i/iiitb_rv32i.v .
          cp ../rv32i/iiitb_rv32i_tb.v .
![task5la1](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/8e79c552-00cc-442d-867d-8fce29b70594)
![task 5 la 2](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/93a0e3e8-fa67-4fef-a4cc-878fd1f68e5b)
![task5la3](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/d998a548-2f68-4d6a-84a3-492f292d7cae)
![task5laadd](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/e0da8627-6f78-4823-b551-ef891e6ade6f)
![task3ins3](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/0c57f661-64a4-4667-ae95-33fe7b9a0e77)
![task5ins4](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/08ad350d-a75f-4126-9ee8-8ea38a6c8108)
![task5ins5](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/10d5b1c8-619a-4e95-879d-fd6f8c04adf7)
![task5ins6](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/c63dacb4-3524-4c06-992e-bb940cdb0dcf)
![task5ins7](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/23bd0bf0-b781-40a1-8afe-32f4dddc87f7)
![task5ins8](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/0797d1a2-5f54-4130-9068-60742ab1121f)
![task5ins9](https://github.com/Abinaya102/VSDSquadron-internship/assets/173627993/9bffcd3e-04f9-49d4-9b51-96984968c75b)




















               



         




     


