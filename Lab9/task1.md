```asm
include irvine32.inc
.data
.code
main proc
	mov eax,10
	mov ebx,eax
	mov ecx,eax
	shl eax,4
	shl ebx,2
	add eax,ebx
	add eax,ecx
	call writeint
exit
main endp
end main
```