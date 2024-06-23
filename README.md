# VSDSquadron-internship
This is the VSDSquadron research internship program which is done using RISC-V development board. This board is powered by CH32VOO3F4U6 chip with 32 bit RISC-V core based tool. It includes a built-in factory-trimmed 24MHz RC oscillator, 128KHz RC oscillator and a 24MHz oscillator for varing clock requirements. It offers multiple communication protocol including US-ART, 12C and SPI for versatile connectivity. It is eqipped with 2KB SRAM for volatile data storage, 16KB flash memory and 1920B for bootloader functionalities.
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

STEP 5:
In the previous case we used -O1 as the optional condition to compile the code whereas now we use -Ofast conditon and the command is as follows:

        riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
Now on obtaing the output of the main section we get,

               



         




     


