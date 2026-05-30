#personal #low-level 
One way to implement interrupts is the Interrupt Descriptor Table(IDT). 

Interrupts are mainly handles in two parts: Interrupt Requests(IRs) and Interrupt Service Routines(ISRs). IRs typically come through the hardware, eg keyboard, serial ports etc. ISRs run when an interrupt is recieved by an OS, eg a Divide the Zero error.

Read more @[osdev.org](https://wiki.osdev.org/Interrupt_Descriptor_Table).

Some programming is involved relating to the Programmable Interrupt Computer(PIC).Generally a computer has a Master(or Main) PIC chip and a Secondary(or Slave) PIC chip. One of them sits at 0x20 for commands and 0x21 for data and the other at 0xA0 for commands and 0xA1 for data. They need to be initialized to use interrupts. Therefore, we need to send data to them through special command outPortB defined in `util.c`