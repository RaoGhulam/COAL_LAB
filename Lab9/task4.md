```asm
INCLUDE Irvine32.inc

.data
    numA SDWORD 100
    numB SDWORD 20
    numC SDWORD 5
    labelA BYTE "numA = ", 0

.code
main PROC
    mov eax, numB
    cdq
    mov ecx, numC
    idiv ecx
    mov ebx, eax

    mov eax, numA
    cdq
    mov ecx, numB
    idiv ecx
    imul ebx

    mov numA, eax

    call Crlf
    mov edx, OFFSET labelA
    call WriteString
    mov eax, numA
    call WriteInt

    call Crlf
    exit
main ENDP

END main
```