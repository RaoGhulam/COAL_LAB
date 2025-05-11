INCLUDE Irvine32.inc

.data
   s1 BYTE "Hello",0
   s2 BYTE "Hello w",0
   m1 BYTE "Both Strings are same",0
   m2 BYTE "Both strings are not same",0

.code

IsCompare PROTO,
 str1:PTR BYTE, str2:PTR BYTE, len:DWORD

main PROC
    INVOKE IsCompare, ADDR s1, ADDR s2, LENGTHOF s1
    exit
main ENDP

IsCompare PROC,
 str1:PTR BYTE, str2:PTR BYTE, len:DWORD

    mov esi, str1
    mov edi, str2
    mov ecx, len
    cld
    repe cmpsb              

    jz strings_equal        
    mov edx, OFFSET m2
    call WriteString
    jmp done

strings_equal:
    mov edx, OFFSET m1
    call WriteString

done:
    ret
IsCompare ENDP

END main