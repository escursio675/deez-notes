#personal #low-level 
We need a map of the memory in our system which we have to retrieve through the BIOS. In the case of grub/multiboot, the process of retrieval involves the 'flags' word in the multiboot header. The process involves retrieving the info from multiboot and then passing it on to the kernel. If not using grub, we have to turn to BIOS interrupts to handle this.

Read more @ [gnu.org](https://www.gnu.org/software/grub/manual/multiboot/multiboot.html)
