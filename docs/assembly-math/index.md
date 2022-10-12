# Random Assembly Math 
### Divide/Multiply by 2
```assembly
shr eax, 1 ; eax = eax >> 1  (divide by 2)
shl eax, 1 ; eax = eax << 1 (multiply by 2)
```
### Setting negative 1
```assembly
or eax, 0FFFFFFFFh ; two's compliment
```
