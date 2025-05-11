```asm
include Irvine32.inc

.data
  x dword 3
  y dword 6
  z dword 9

.code

main proc 
   
    push z
    push y
    push x
    call SumThree
    exit
main endp

SumThree proc 
    push ebp
    mov ebp, esp

    mov eax, [ebp+8]    ; x
    add eax, [ebp+12]   ; y
    add eax, [ebp+16]   ; z

    call WriteInt
    call Crlf           

    pop ebp
    ret 12              
SumThree endp

end main
```