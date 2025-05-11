```asm
include Irvine32.inc

.data
    num dword ?
    m1 byte "Enter a number (0=Sat to 6=Fri): ",0
    d1 byte "Saturday ",0
       byte "Sunday   ",0
       byte "Monday   ",0
       byte "Tuesday  ",0
       byte "Wednesday",0
       byte "Thursday ",0
       byte "Friday   ",0

.code
main PROC

    mov edx, offset m1
    call WriteString

    call ReadInt
    mov num, eax

    mov ecx, 10
    imul eax, ecx

    mov edx, offset d1
    add edx, eax

    mov ecx, 9  ; Number of characters in the day name (excluding the null terminator)
print_loop:
    mov al, [edx]
    call WriteChar
    inc edx
    loop print_loop

    call Crlf

    exit
main ENDP
END main
```