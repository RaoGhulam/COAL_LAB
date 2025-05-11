```asm
INCLUDE Irvine32.inc

.data
    Str1 BYTE "127&j~3#^&*#*#45^",0
    m2 BYTE "Letter Not found",0

.code

Scan_String PROTO arr:PTR BYTE, w:BYTE

main PROC
    INVOKE Scan_String, ADDR Str1, '#'
    exit
main ENDP

Scan_String PROC arr:PTR BYTE, w:BYTE
    push edi                
    mov edi, arr           
    mov al, w              
    mov ecx, lengthof Str1   
    cld                    
    repnz scasb            
    jnz NotFound           

    mov eax, lengthof Str1  
    sub eax, ecx           
    dec eax                
    call WriteInt
    call Crlf
    pop edi
    ret

NotFound:
    mov edx, OFFSET m2
    call WriteString
    call Crlf
    pop edi
    ret
Scan_String ENDP

END main
```