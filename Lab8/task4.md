```asm
INCLUDE Irvine32.inc

.data
    counter DWORD 0
    msg1 BYTE "Hello", 0
    msg2 BYTE "World", 0

.code
main PROC
    loop_start:
        cmp counter, 10
        ja end_loop
        
        cmp counter, 5
        jae case_else
        
        ; Print "Hello"
        mov edx, OFFSET msg1
        call WriteString
        call Crlf
        jmp continue_loop
        
    case_else:
        ; Print "World"
        mov edx, OFFSET msg2
        call WriteString
        call Crlf
        
    continue_loop:
        inc counter
        jmp loop_start
        
    end_loop:
    exit
main ENDP
END main
```