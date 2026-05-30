#personal #low-level 
GDT, or a Global Descriptor Table, is a data structure used by Intel x86 processors and defines the characteristics of various memory areas called segments. Segmentation allow us to implement size and access privileges of these segments.

Note that GDTs are specific to the x86 processors. Therefore, in 64bit mode, we generally opt for paging.

A GDT is essentially an array where the elements are sections of memories, known as entries.

Read more @[osdev.org](https://wiki.osdev.org/Global_Descriptor_Table).

==It is very important to implement the entry struct in the order of the Segment Descriptor, from bottom to top==

Another entry in the gdt is the Task State Segment(TSS). It is used for context switches for kernel function calls, time slice expiration etc. Context switching involves storing the information of the previous process and loading in the new information. Therefore, the TSS stores task related information. The TSS, although mostly used for hardware context switching, provides some performation optimizations when used for software context switching as well as multitasking. 

Read more @[osdev.org](https://wiki.osdev.org/Task_State_Segment)

