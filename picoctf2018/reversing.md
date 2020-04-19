# Reversing

**assembly-0 - Points: 150**

> What does asm0\(0xaa,0xf2\) return? Submit the flag as a hexadecimal value \(starting with '0x'\). NOTE: Your submission for this question will NOT be in the normal flag format. [Source](https://2018shell.picoctf.com/static/5359d5442f2379ae9948dfeebe80d8f8/intro_asm_rev.S) located in the directory at /problems/assembly-0\_2\_485b2d48345b19addbeb06a36aabdc74.  
> Hint: 
>
> * basical assembly [tutorial](https://www.tutorialspoint.com/assembly_programming/assembly_basic_syntax.htm)
> * assembly [registers](https://www.tutorialspoint.com/assembly_programming/assembly_registers.htm)

The following is the context of the assembly file.

```text
.intel_syntax noprefix
.bits 32
	
.global asm0

asm0:
	push	ebp				
	mov	ebp,esp
	mov	eax,DWORD PTR [ebp+0x8]
	mov	ebx,DWORD PTR [ebp+0xc]
	mov	eax,ebx
	mov	esp,ebp
	pop	ebp	
	ret
```

Breakdown of code:

```text
push    ebp
mov     ebp, esp
```

Those two lines are what's is called the function prologue. We first save the calling function stack frame \(`ebp` is tracking that\) and in the second one, we set our function stack frame to be equal to the current stack location.

```text
mov eax, DWORD PTR [ebp+0x8]
mov ebx, DWORD PTR [ebp+0xc]
```

The above lines are loading our passed arguments to `eax` and `ebx`.  `eax`  will have `0xaa` and `ebx` will be equal to `0xf2`.

```text
mov eax, ebx
```

The value from `ebx` is stored in `eax`, thus we drop the need of the first line from the previous fragment. `eax` is usually the register containing the return value, in this case would be `0xf2`.

```text
mov esp,ebp
pop ebp
```

This is just bringing back the stack as it was when we enter the function - also called function epilogue.

```text
ret
```

picoCTF{0xf2}

### 

