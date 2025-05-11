```asm
INCLUDE Irvine32.inc

.data
    user_input WORD ?
    numbers WORD 10, 4, 7, 14, 299, 156, 3, 19, 29, 300, 20
    found_msg BYTE "Index of Value: ", 0
    not_found_msg BYTE "Value not present", 0
    prompt_msg BYTE "Enter a value: ", 0

.code
main PROC
    mov edx, OFFSET prompt_msg
    call WriteString
    call ReadInt
    mov user_input, ax

    mov ecx, LENGTHOF numbers
    mov esi, 0

search_loop:
    cmp numbers[esi * TYPE numbers], ax
    je value_found
    inc esi
    loop search_loop

    mov edx, OFFSET not_found_msg
    call WriteString
    jmp end_search

value_found:
    mov edx, OFFSET found_msg
    call WriteString
    mov eax, esi
    imul eax, 2
    call WriteInt

end_search:
    exit
main ENDP
END main
```