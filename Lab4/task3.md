```asm
include irvine32.inc
.data
varB BYTE +10
varW WORD -150
varD DWORD 600
.code
main proc
	movsx eax, varB
	movsx ebx, varW
	mov ecx, varD
	call dumpregs
main endp
end main
```