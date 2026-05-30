#personal #low-level 
Introducing C code brings about two main challenges:
1. Requirement of a compiler which can compile 16bit ASM
2. Unavailability of standard C libraries

Therefore, we have to use a mixture of C and ASM to implement these from scratch. The first step is to update the Makefile for it to compile C code. We use the open source C compiler _open-watcom_ for this, since it is compatible with older versions of C that support 16bit compilation. It is available at `https://github.com/open-watcom/open-watcom-v2/releases/tag/Current-build`.

The `linker.lnk` is a linker file which defines how the binary is produced from the linker file. The linker file is below:

```
FORMAT RAW BIN
OPTION QUIET,
        NODEFAULTLIBS,
        START=entry,
        VERBOSE,
        OFFSET=0
        STACK=0x200
ORDER
	CLNAME CODE
		SEGMENT _ENTRY
		SEGMENT _TEXT
	CLNAME DATA
```

 - `START`=entry is a convention
 - `STACK` address must be consistent wit that provided in the _boot.asm_ file
 - `SEGMENT _ENTRY` defines the entry point for the application

==The `main.c` and `print.h` may show a "expected a ;" error. This is not a C syntax error and is instead cause by the VSCode Intellisense. It may be safely ignored.==
