# Space ~ HTB ~ Pwn Challenge
## Solver: Eyal Asulin
I started with basic checks on the ELF file:
- There are not any security techniques enabled. (Cannary, NX, ASLR)
- i386 | 32 bit -> little indian
- Since there is no flag function, I will inject a shellcode into the binary.

First I tried to use JMP ESP gadget to run a shell, but then I realized that the program first takes the input on the main function. So, the vuln function call overwrites my shellcode.

Then I read about Multi-Staging exploit. By this method, I write my shellcode in an empty memory piece, and exploit the vuln function twice actually.
First time to call the read function again and the second time for executing my shellcode, which was injected by the re-reading.

**Settings:**<br>
shellcode_addr = 0x0804b427 (include nopsled)<br>
read_addr      = 0x08049217<br>
shellcode_len  = 0x000000ff (255[dec])<br>

|Stage 1|
|--|
|offset 14|
|set $ebp to shellcode_addr|
|set $eip to read_addr|
|set length of shellcode to shellcode_len|
|padding 5 bytes|

|Stage 2|
|--|
|offset 18|
|set $eip to shellcode_addr|
|nopsled- 20 bytes|
|shellcode|

Exploit code included, for running just set HOST and PORT.


*Written by Eyal Asulin©*
