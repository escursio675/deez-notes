#personal #low-level  
`printf()` in C has a number of different formats. To parse these formats, we use a state machine. These are defined withing `stdio.h`

Note that there may be several errors that appear in the printf implementation due to lack of backwards compatibility of redundant C concepts like `far`, `_cdecl` etc. These may be safely ignored.