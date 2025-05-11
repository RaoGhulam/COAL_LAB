```asm
INCLUDE Irvine32.inc

.data
    result DWORD ?
    inputVal DWORD 5
    dataList SWORD 0,0,0,150,120,35,-12,66,4,0

.code
main PROC
    mov esi, LENGTHOF dataList
    mov eax, inputVal
    cmp eax, esi
    jge notValid
    lea edx, inputVal
    inc edx
    cmp esi, edx
    jl notValid

    mov result, 0
    jmp display

notValid:
    mov result, 1

display:
    mov eax, result
    call WriteInt
    exit
main ENDP
END main
```