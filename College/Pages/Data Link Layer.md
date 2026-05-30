#college 

# Cyclic Redundancy Check(CRC)
Cyclic codes are special linear block codes with one extra property. In a cyclic code, if a codeword is cyclically shifted (rotated), the result is another codeword. For example, if 1011000 is a codeword and we cyclically left-shift, then 0110001 is also a codeword.

CRC is used in WANs and LANs.

CRC involves modulo-2 division which is a binary division in which there are no borrows or carries and addition and subtraction are done using XOR. The steps are:
1. If G(x) has n bits, append n - 1  zeroes to the data M(x)
2. XOR n bits of M(x) with G(x)
3. Bring down the next bit
	1. If the sequence starts with 0, XOR with 0s 
	2. Otherwise XOR with G(x)
4. Repeat until no more bits can be brought down
5. The remainder is the required CRC
6. Append the CRC with M(x) to obtain the codeword T(x)

If the CRC is of length less than n - 1, then we prepend zeroes before attaching it to M(x) in order to prevent ambiguity of the reciever. The generator must have 1s in its higher order and lower order bits.