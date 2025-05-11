```asm
include irvine32.inc
.data
	A DWORD  0FF10h
	B DWORD  0E10Bh
.code
main proc
	mov eax, A
	XCHG eax, B 
	mov A,eax
	call dumpregs
	exit
main endp
end main 
```