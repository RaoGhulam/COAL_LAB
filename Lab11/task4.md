```asm
Str_Reverse PROC
    push ebp
    mov ebp, esp
    push esi
    push edi
    push ebx
    
    mov esi, [ebp+8]       ; Get string offset
    
    ; Find string length
    mov edi, esi
    mov ecx, 0
FindLength:
    cmp BYTE PTR [edi], 0
    je FoundEnd
    inc edi
    inc ecx
    jmp FindLength
    
FoundEnd:
    dec edi                ; Point to last character before null
    
ReverseLoop:
    cmp esi, edi
    jae Done               ; If pointers meet/cross, we're done
    
    ; Swap characters
    mov al, [esi]
    mov bl, [edi]
    mov [esi], bl
    mov [edi], al
    
    ; Move pointers
    inc esi
    dec edi
    jmp ReverseLoop
    
Done:
    pop ebx
    pop edi
    pop esi
    pop ebp
    ret 4                  ; Clean up stack (1 param)
Str_Reverse ENDP
```