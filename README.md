# Hacking using C-Language
To look at the machine code of a gcc compiled program(Simple Program that prints Hello World! 10 times), we can use objdump
Example command:
objdump -D {filename} | grep -A20 main.:
Example output:
![image](https://user-images.githubusercontent.com/42641723/171374873-26c895fb-0d4f-40a0-aacf-8722fd2a1bae.png)


The objdump program displays alot of instructions thats why we just grep the useful information inside the main() function.
Each bytes is represented in hexadecimal notation(base-16 numbering system), This is a convenient notation because a byte contains 8 bits. Each of which can be either true or false.
This means that a byte has 256 possible values so each byte can be described with 2 hexadecimal digits.
The hexadecimal numbers on the far left are memory adresses. The machine language instructions are put on the memory(A collection of bytes of temporary storage space that are numbered with addresses).
You can think of memory as a row of bytes, each with its own memory address. Each byte of memory can be access by its address, Here the CPU accesses this part of memory to retrieve the machine language instructions for the compiled program.
Older Intel x86 processors use a 32-bit addressing scheme, while newwer ones use a 64-bit one. 32-bit processors have 2^32 possible adresses(4,294,967,296), 64 bit ones have 2^64(1.84467441x10^19)addresses.
64-bit processors can run in 32-bit compatibility mode which allows them to run 32-bit code quickly.

How to use GDB to show the state of the processor registers before the program starts.
gdb -q ./a.out
![image](https://i.ibb.co/jwrD1Mz/image.png)
Explanation:
A breakpoint is set on the main() function so execution will stop right
before our code is executed. Then GDB runs the program, stops at the
breakpoint, and is told to display all the processor registers and their
current states.
EAX(Accumulator), ECX(Counter), EDX(Data), EBX(Base) are general purpose registers. They are used for a variety of purposes, but they mainly
act as temporary variables for the CPU when it is executing machine
instructions.
ESP(Stack Pointer), EBP(Base Pointer), ESI(Source Index), EDI(Destination Index)are also general-purpose indexes but they are sometimes known as pointers and indexes. 
The first two registers are called pointers because they store 32-bit addressses,which essentially point to that location in memory. These registers
are fairly important to program execution and memory management.
EIP(Instruction Pointer) register points to the current instruction the processor is reading. This register is quite important and will be used a lot while debugging.
EFLAGS register consists of several bit flags that are used for comparisons and memory segmentations.
I will be using Intel syntax assembly language, our tools must be configured to use this syntax. To set gdb to use Intel Syntax we can put a simple command in the gdbinit file.
Commands:
echo "set disassembly intel" > ~/.gdbinit

