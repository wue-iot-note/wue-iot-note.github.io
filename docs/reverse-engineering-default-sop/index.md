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
