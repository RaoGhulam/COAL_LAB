```asm
section .data
    ask_input db "Provide number: ", 0
    format_int db "%d", 0
    txt_is_prime db "%d is a prime", 10, 0
    txt_not_prime db "%d is not a prime", 10, 0
    txt_max_prime db "Highest prime entered: %d", 10, 0
    data_array times 4 dd 0

section .text
global main
extern scanf, printf

main:
    mov ecx, 0
    mov edi, data_array
collect_inputs:
    push ecx
    push edi
    push ask_input
    call printf
    add esp, 4
    push edi
    push format_int
    call scanf
    add esp, 8
    pop edi
    pop ecx
    add edi, 4
    inc ecx
    cmp ecx, 4
    jl collect_inputs

    mov esi, data_array
    xor ecx, ecx
    mov bl, 1
verify_loop:
    cmp ecx, 4
    jge check_done
    push ecx
    push ebx
    push esi
    mov eax, [esi + ecx*4]
    push eax
    call isPrime
    add esp, 4
    pop esi
    pop ebx
    pop ecx
    test eax, eax
    jnz continue_check
    xor bl, bl
continue_check:
    inc ecx
    jmp verify_loop
check_done:
    cmp bl, 1
    jne end_program
    push data_array
    call findMax
    add esp, 4
end_program:
    ret

isPrime:
    push ebp
    mov ebp, esp
    push ebx
    mov eax, [ebp+8]
    cmp eax, 2
    jl not_a_prime
    mov ebx, 2
check_division:
    mov edx, 0
    div ebx
    test edx, edx
    jz not_a_prime
    inc ebx
    mov eax, [ebp+8]
    cmp ebx, eax
    jl check_division
    mov eax, 1
    jmp prime_done
not_a_prime:
    xor eax, eax
prime_done:
    push eax
    push dword [ebp+8]
    cmp eax, 1
    jne show_not_prime
    push txt_is_prime
    jmp show_output
show_not_prime:
    push txt_not_prime
show_output:
    call printf
    add esp, 12
    pop ebx
    mov esp, ebp
    pop ebp
    ret

findMax:
    push ebp
    mov ebp, esp
    mov esi, [ebp+8]
    mov eax, [esi]
    mov ecx, 1
next_elem:
    cmp ecx, 4
    jge display_result
    mov edx, [esi + ecx*4]
    cmp edx, eax
    jle skip_update
    mov eax, edx
skip_update:
    inc ecx
    jmp next_elem
display_result:
    push eax
    push txt_max_prime
    call printf
    add esp, 8
    mov esp, ebp
    pop ebp
    ret
```