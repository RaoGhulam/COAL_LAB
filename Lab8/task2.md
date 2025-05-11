```asm
INCLUDE Irvine32.inc

.data
    msgNone BYTE "No non-zero number found", 0
    msgFound BYTE "First non-zero number: ", 0
    numbers SDWORD 0, 0, 0, 150, 120, 35, -12, 66, 4, 0

.code
main PROC
    mov esi, 0
    mov ecx, LENGTHOF numbers

searchLoop:
    cmp numbers[esi * TYPE numbers], 0
    jne foundValue
    inc esi
    loop searchLoop

    mov edx, OFFSET msgNone
    call WriteString
    exit

foundValue:
    mov edx, OFFSET msgFound
    call WriteString
    mov eax, numbers[esi * TYPE numbers]
    call WriteInt

    exit
main ENDP
END main
```