```asm
include irvine32.inc
.data
	SecondsInDay =  60*60*24
	
.code
main proc
	mov eax, SecondsInDay
	call writeint
	exit
main endp
end main 
```