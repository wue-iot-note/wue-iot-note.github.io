# Reverse Engineering default SOP

## PE header fields
### Machine type
useful for identifying plateform of the executable</br>
```
+-------------------------+-------+-----------+
| Constant                | Value | Plateform |
+-------------------------+-------+-----------+
| IMAGE_FILE_MACHINE_I386 | 0x14C | 32        |
+-------------------------+-------+-----------+
```
The reference values can be found at [https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#machine-types](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format#machine-types)

## Hexdump
View executeable or output files in hex. Look for charasteristics such as
* Repeating sequence of bytes

## IDA
start of entry point - ctrl + E
return - ESC
jump to segment - ctrl + S
view function stack - ctrl + k when cursor at function 
view stack variable reference - ctrl + x, after select stack address

## CFF Explorer
* examine basic file info. Check to see if the file is packed (UPX, etc). 
* If is packed, the segments should have UPX1, UPX0. ctrl+s

## Unpacking
* RWX native memory code segments in PE
  * Automodification of the code
  * Fix IAT
  * Jump in it
* Allocate new RWX code segment
  * Fill with code
  * Fix IAT
  * Jump in it
* Process hollowing aka RunPE
  * create new "suspended" process
  * unmap and replace all segments
  * set original EIP
  * run
  * exit

CreateProcess, CREATE_SUSPENDED</br>
GetThreadContext: EBX->PEB</br>
NtUnmapViewOfSection</br>
VirtuallAllocEx</br>
WriteProcessMemroy</br>
SetThreadContext</br>
ResumeThread

* Unpack in another process (process injection)
Create a new "thread" in another process</br>
VirtualAllocEx</br>
WriteProcessMemory</br>
ResumeThread</br>
