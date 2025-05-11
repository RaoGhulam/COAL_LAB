```asm
include irvine32.inc
.data
	val1 BYTE 10h
	val2 WORD 8000h
	val3 DWORD 0FFFFh
	val4 WORD 7FFFh
.code
main proc
	;i)
	inc val2
	movzx eax, val2
	call writeint
	call crlf
	;ii)
	mov eax, 9000h
	sub eax,val3
	call writeint
	call crlf
	;iii)
	movzx  eax, val2 
	sub ax, val4
	mov val2,ax
	call writeint
	call crlf

	
	exit
main endp
end main 
```