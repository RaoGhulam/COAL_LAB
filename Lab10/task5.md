```asm
include irvine32.inc

.data
    nums WORD 10, 4, 7, 14, 299, 156, 3, 19, 29, 300, 20

.code

sortArray proto, pArr:PTR WORD, count:BYTE

main proc
    invoke sortArray, addr nums, lengthof nums
    exit
main endp

sortArray proc, pArr:PTR WORD, count:BYTE
    LOCAL swapFlag:BYTE, tempVal:WORD
    LOCAL index:BYTE

    movzx ecx, count
    dec ecx
    mov index, cl

outer_loop:
    mov esi, pArr
    mov swapFlag, 1

    movzx ecx, count
    dec ecx

inner_loop:
    mov ax, [esi]
    mov dx, [esi+2]
    cmp ax, dx
    jle skip_swap

    mov [esi], dx
    mov [esi+2], ax
    mov swapFlag, 0

skip_swap:
    add esi, 2
    loop inner_loop

    cmp swapFlag, 1
    je output_sorted

    movzx ecx, index
    dec index
    jnz outer_loop

output_sorted:
    mov esi, pArr
    movzx ecx, count

print_next:
    movzx eax, word ptr [esi]
    call WriteInt
    call Crlf
    add esi, 2
    loop print_next

    ret
sortArray endp

end main
```