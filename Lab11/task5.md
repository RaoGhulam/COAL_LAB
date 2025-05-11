```asm
Load PROC
    push ebp
    mov ebp, esp
    push esi
    push ecx
    push ebx
    
    mov esi, [ebp+8]     
    mov ecx, [ebp+12]  
    mov ebx, 0  
    
LoadLoop:
    cmp ebx, ecx
    jge Done       
    
    mov eax, [esi + ebx*4]
    shl eax, 1             
    mov [esi + ebx*4], eax 
    
    inc ebx               
    jmp LoadLoop
    
Done:
    pop ebx
    pop ecx
    pop esi
    pop ebp
    ret 8                
Load ENDP
```