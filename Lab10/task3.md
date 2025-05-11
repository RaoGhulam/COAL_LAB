```asm
include Irvine32.inc

.data
  m1 byte "Enter Integer for Square ",0

.code

main proc 
   
    call LocalSquare
    exit
main endp

LocalSquare proc 
    enter 4,0
    mov edx,offset m1
    call writestring
    call readint
    mov dword ptr[ebp-4],eax

    mov ebx,eax
    mul ebx
    call writeint
    leave
    ret              
LocalSquare endp

end main
```