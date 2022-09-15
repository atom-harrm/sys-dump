;this is a simple nasm code
	version 1.1
;	author johnson
 

; nasm -f elf -g -F stabs task.asm
; ld -m elf_i386 task.o -o task	

SECTION .bss	;section of unitilased data

len equ  10

SECTION .data	;section of initilased data

 msg db "HI world",10

SECTION .text    ;section for the actual code

	global _start:
		
		nop:		;this  make the gdb happy
		_start:
;let's create our write function

	write:	
		mov eax,4	;sys_write
		mov ebx,1 	;sys_fd_out
		mov ecx,msg	;this our string	
		mov edx,len	;this the size of the string
		int 80H		;this is sys_kernel


		mov ebp,eax
		mov edx,edi
		pop eax
		call Done

		
;let end the party

	Done:
		mov eax,1 	;return the 1 to the sys_exit
		mov ebx,0	;this returns a zero to the kernel
		int 18H		;sys_kernel call to reboot the system 



