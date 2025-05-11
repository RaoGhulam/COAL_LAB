```asm
INCLUDE Irvine32.inc

.data

.code
main PROC

    mov ax, -128       
    movzx eax, ax        


    shl eax, 16          
    sar eax, 16          

    call WriteInt        
    call Crlf
    exit
main ENDP

END main
```