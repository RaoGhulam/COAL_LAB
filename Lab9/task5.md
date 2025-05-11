```asm
INCLUDE Irvine32.inc

.data
    loA SDWORD 0x12345678
    hiA SDWORD 0x9ABCDEF0
    loB SDWORD 0x23456789
    hiB SDWORD 0xABCDEF01
    loRes SDWORD 0
    hiRes SDWORD 0
    msgLow BYTE "Lower Result: ", 0
    msgHigh BYTE "Upper Result: ", 0

.code
main PROC
    call Add64

    call Crlf
    mov edx, OFFSET msgLow
    call WriteString
    mov eax, loRes
    call WriteHex

    call Crlf
    mov edx, OFFSET msgHigh
    call WriteString
    mov eax, hiRes
    call WriteHex

    call Crlf
    exit
main ENDP

Add64 PROC
    mov eax, loA
    add eax, loB
    mov loRes, eax

    jc hasCarry
    mov eax, hiA
    add eax, hiB
    mov hiRes, eax
    ret

hasCarry:
    mov eax, hiA
    add eax, hiB
    inc eax
    mov hiRes, eax
    ret
Add64 ENDP

END main
```