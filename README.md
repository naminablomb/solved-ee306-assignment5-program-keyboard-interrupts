Download Link: https://assignmentchef.com/product/solved-ee306-assignment5-program-keyboard-interrupts
<br>
The purpose of this assignment is to program keyboard interrupts in LC-3 assembly language. The application detects the coding sequence (CDS) of a messenger RNA.

Starter Code

You can find the starter code on Canvas.

<h1>Details</h1>

This assignment will be written in two parts: ● the main program (Main.asm)

<ul>

 <li>the interrupt service routine (ISR.asm)</li>

</ul>

Background

<u><a href="https://en.wikipedia.org/wiki/Messenger_RNA">Messenger RNA (mRNA)</a>​</u> is a large family of RNA molecules that convey genetic information from DNA to the ribosome, where they specify the amino acid sequence of the protein products of gene expression. The mRNA genetic information is in the form of a sequence of nucleotides which are arranged into codons consisting of 3 bases each. Valid bases that make up codons are ​<strong>A</strong>​ (Adenine), ​<strong>C </strong>​(Cytosine), ​<strong>G</strong> (Guanine), and ​<strong>U</strong>​ (Uracil). As the picture shows, the “coding sequence” of an mRNA starts with START codon and ends with a STOP codon. A START codon is always an ​<strong>AUG</strong>​ sequence, and the STOP codon can be one of three possible sequences, ​<strong>UAG</strong>​, <strong>UAA</strong>​​, or ​<strong>UGA.</strong>

Interrupt Service Routine (ISR)

In this assignment, we will use the keyboard as the input device for interrupting the main program. This ISR will start at ​x2600​. The ISR simply reads the character typed and accepts only the symbols ‘A’, ‘C’, ‘G’, or ‘U’. Any other symbol will be ignored. Once it detects a valid symbol, it places it at location ​x3600​.

The main program will constantly check this location to see if there is a valid input character there and writes a ​0 when it processes it. Processing a valid character follows a simple algorithm which can be​    described by the above incomplete finite state machine (FSM). It is incomplete in that, it does not account for all inputs in all states but only presents some of the relevant inputs. You are welcome to solve the problem without the FSM as long as you implement the expected functionality.




Main Program

The Main program will start at x3000​​ and will write to the screen the character it reads from x3600​​ , making sure it does this only once for each input entered. Also, it checks to see if a START codon (AUG) is detected. If so, it prints the pipe symbol ‘|’. After this point, it looks for a STOP codon (UAG, UAA, or UGA) so the program can terminate. (Note that for this program, the coding sequence itself does not need to be aligned in groups of 3 bases per codon. This is unlike real mRNA.)

<strong><u>VERY IMPORTANT</u></strong><u>​</u>: You are not allowed to use any TRAP instructions in your interrupt service routine. To read a character that the user entered, you may not call ​TRAP x20​ (​GETC​) or ​TRAP x23​ (​IN​), or use any of the other TRAP routines. If you use TRAP in the interrupt service, your program is not correct and will fail our testing <em>even though it may appear to work when you test it</em>​  ​. You are free to use TRAPs in the main program.

Hint: Do not forget to save and restore any registers that you use in the interrupt service routine.




The user program must be named ​<strong>Main.asm</strong>​ and will be of the form:

.ORIG x3000

—     —     ; initialize the stack pointer (needed on the old simulator)

…

—     —

—     —     ; set up the keyboard interrupt vector table entry

…

—     —

—     —     ; enable keyboard interrupts

…

—     —

—     —     ; start of actual program

…

—     —

.END




The interrupt service routine must be named ​<strong>ISR.asm</strong>​ and will be of the form:

.ORIG x2600

—     —     ; the code

…

—     —

RTI

—     —

…

—     —

.END




Here is a screenshot as an example of how the console should look when you run the program. The first and the last three cases show an empty coding sequence. Also, note that the user could have typed other invalid characters (including lowercase ‘a’, ‘c’, ‘g’, and ‘u’) which are ignored by the ISR and therefore not displayed by the main.