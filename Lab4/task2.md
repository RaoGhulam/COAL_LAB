```asm
include irvine32.inc
.data
.code
main proc
	mov al,'R'
	mov bl,'A'
	mov cl,'O'
	call dumpregs
main endp
end main
```