```asm
include Irvine32.inc

.data
   var byte ?
   m1 byte "Write Character: ",0
   m2 byte "Character is alphabet",0
   m3 byte "Character is not alphabet",0

.code
main PROC
    mov edx, offset m1
    call writestring
    call readchar
    call crlf

    cmp al,65
    jl not_alphabet
    cmp al,90
    jg check_capital
    mov edx, offset m2
    call writestring
    exit
    check_capital:
    cmp al,97
    jl not_alphabet
    cmp al,122
    jg not_alphabet
    mov edx, offset m2
    call writestring
    exit

    not_alphabet:
    mov edx, offset m3
    call writestring
    exit
main ENDP
END main
```