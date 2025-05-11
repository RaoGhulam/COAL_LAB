```asm
INCLUDE Irvine32.inc

.data
    msg1 BYTE "BX after manual shift: ", 0
    msg2 BYTE "BX after SHRD: ", 0

.code
main PROC

    mov ax, 0003h      

    shl ax, 15         
    mov bx,0
    or  bx, ax        
    mov edx, OFFSET msg1
    call WriteString
    movzx eax, bx
    call WriteHex

    mov ax, 0003h  

    mov dx, ax          
    shl dx, 15         
       
    mov cx, 1
    shrd bx, dx, cl    

    call Crlf
    mov edx, OFFSET msg2
    call WriteString
    movzx eax, bx
    call WriteHex

    call Crlf
    exit
main ENDP

END main
```