```asm
INCLUDE Irvine32.inc

.data
    msgSame BYTE "All are same", 0
    msgDiff BYTE "Not all same", 0
    msgPrompt BYTE "Provide 4 numbers:", 0
    nums DWORD 4 DUP(?)

.code
main PROC
    mov edx, OFFSET msgPrompt
    call WriteString
    call Crlf

    mov esi, 0
    mov ecx, LENGTHOF nums
inputLoop:
    call ReadInt
    mov nums[esi * TYPE nums], eax
    inc esi
    loop inputLoop

    mov esi, 1
    mov ecx, LENGTHOF nums - 1
    mov eax, nums[0]
checkLoop:
    cmp eax, nums[esi * TYPE nums]
    jne notEqual
    inc esi
    loop checkLoop

    mov edx, OFFSET msgSame
    call WriteString
    call Crlf
    exit

notEqual:
    mov edx, OFFSET msgDiff
    call WriteString
    call Crlf
    exit
main ENDP
END main
```