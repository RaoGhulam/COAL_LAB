```asm
section .data
    array dd 12, 45, 3, 78, 23, 56, 89, 34, 67, 90, 1, 45, 78, 23, 56, 89, 34, 67, 90, 100
    array_size equ 20

section .text
global _start

_start:
    push array
    call MinMaxArray
   
    mov eax, 1
    mov ebx, 0
    int 0x80

MinMaxArray:
    push ebp
    mov ebp, esp
    push ebx     
    push esi
 
    mov esi, [ebp+8] 
    
    mov eax, [esi]     
    mov ebx, [esi]    
    
    mov ecx, 1      
    .loop:
        cmp ecx, array_size
        jge .done
        
        mov edx, [esi + ecx*4]
        
        cmp edx, eax
        jge .not_min
        mov eax, edx
        .not_min:
        
        cmp edx, ebx
        jle .not_max
        mov ebx, edx
        .not_max:
        
        inc ecx
        jmp .loop
    
    .done:
    pop esi
    pop ebx
    mov esp, ebp
    pop ebp
    ret 4        
```