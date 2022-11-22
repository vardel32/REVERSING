# Need For Speed
#picoCTF2019 #REVERSING 
## Objetivo
The name of the game is [speed](https://www.youtube.com/watch?v=8piqd2BWeGI). Are you quick enough to solve this problem and keep it above 50 mph? [need-for-speed](https://jupiter.challenges.picoctf.org/static/cd51b2c95be9f3626db6fe6665afb5a3/need-for-speed).
## Solución
Mediante GDB Se ejecutan la siguiente serie de comandos.

```bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/nfs]
└─$ gdb need-for-speed -q
Reading symbols from need-for-speed...
(No debugging symbols found in need-for-speed)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x00000000000005d8  _init
0x0000000000000600  putchar@plt
0x0000000000000610  puts@plt
0x0000000000000620  alarm@plt
0x0000000000000630  __sysv_signal@plt
0x0000000000000640  exit@plt
0x0000000000000650  __cxa_finalize@plt
0x0000000000000660  _start
0x0000000000000690  deregister_tm_clones
0x00000000000006d0  register_tm_clones
0x0000000000000720  __do_global_dtors_aux
0x0000000000000760  frame_dummy
0x000000000000076a  decrypt_flag
0x00000000000007f1  calculate_key
0x000000000000080e  alarm_handler
0x000000000000082f  set_timer
0x000000000000087d  get_key
0x00000000000008ac  print_flag
0x00000000000008d8  header
0x000000000000091a  main
0x0000000000000960  __libc_csu_init
0x00000000000009d0  __libc_csu_fini
0x00000000000009d4  _fini
(gdb) disassemple main
Undefined command: "disassemple".  Try "help".
(gdb) disassemble main
Dump of assembler code for function main:
   0x000000000000091a <+0>:	push   %rbp
   0x000000000000091b <+1>:	mov    %rsp,%rbp
   0x000000000000091e <+4>:	sub    $0x10,%rsp
   0x0000000000000922 <+8>:	mov    %edi,-0x4(%rbp)
   0x0000000000000925 <+11>:	mov    %rsi,-0x10(%rbp)
   0x0000000000000929 <+15>:	mov    $0x0,%eax
   0x000000000000092e <+20>:	call   0x8d8 <header>
   0x0000000000000933 <+25>:	mov    $0x0,%eax
   0x0000000000000938 <+30>:	call   0x82f <set_timer>
   0x000000000000093d <+35>:	mov    $0x0,%eax
   0x0000000000000942 <+40>:	call   0x87d <get_key>
   0x0000000000000947 <+45>:	mov    $0x0,%eax
   0x000000000000094c <+50>:	call   0x8ac <print_flag>
   0x0000000000000951 <+55>:	mov    $0x0,%eax
   0x0000000000000956 <+60>:	leave  
   0x0000000000000957 <+61>:	ret    
End of assembler dump.
(gdb) set disassembly-flavor intel
(gdb) disassemble main
Dump of assembler code for function main:
   0x000000000000091a <+0>:	push   rbp
   0x000000000000091b <+1>:	mov    rbp,rsp
   0x000000000000091e <+4>:	sub    rsp,0x10
   0x0000000000000922 <+8>:	mov    DWORD PTR [rbp-0x4],edi
   0x0000000000000925 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x0000000000000929 <+15>:	mov    eax,0x0
   0x000000000000092e <+20>:	call   0x8d8 <header>
   0x0000000000000933 <+25>:	mov    eax,0x0
   0x0000000000000938 <+30>:	call   0x82f <set_timer>
   0x000000000000093d <+35>:	mov    eax,0x0
   0x0000000000000942 <+40>:	call   0x87d <get_key>
   0x0000000000000947 <+45>:	mov    eax,0x0
   0x000000000000094c <+50>:	call   0x8ac <print_flag>
   0x0000000000000951 <+55>:	mov    eax,0x0
   0x0000000000000956 <+60>:	leave  
   0x0000000000000957 <+61>:	ret    
End of assembler dump.
(gdb) 
(gdb) disassemble main
Dump of assembler code for function main:
   0x000000000000091a <+0>:	push   rbp
   0x000000000000091b <+1>:	mov    rbp,rsp
   0x000000000000091e <+4>:	sub    rsp,0x10
   0x0000000000000922 <+8>:	mov    DWORD PTR [rbp-0x4],edi
   0x0000000000000925 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x0000000000000929 <+15>:	mov    eax,0x0
   0x000000000000092e <+20>:	call   0x8d8 <header>
   0x0000000000000933 <+25>:	mov    eax,0x0
   0x0000000000000938 <+30>:	call   0x82f <set_timer>
   0x000000000000093d <+35>:	mov    eax,0x0
   0x0000000000000942 <+40>:	call   0x87d <get_key>
   0x0000000000000947 <+45>:	mov    eax,0x0
   0x000000000000094c <+50>:	call   0x8ac <print_flag>
   0x0000000000000951 <+55>:	mov    eax,0x0
   0x0000000000000956 <+60>:	leave  
   0x0000000000000957 <+61>:	ret    
End of assembler dump.
(gdb) run
Starting program: /home/kali/Downloads/REVERSING/nfs/need-for-speed 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
Keep this thing over 50 mph!
============================

Creating key...
Not fast enough. BOOM!
[Inferior 1 (process 24731) exited normally]
(gdb) break main
Breakpoint 1 at 0x55555540091e
(gdb) info breakpoints
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000055555540091e <main+4>
(gdb) run
Starting program: /home/kali/Downloads/REVERSING/nfs/need-for-speed 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x000055555540091e in main ()
(gdb) disassemble main
Dump of assembler code for function main:
   0x000055555540091a <+0>:	push   rbp
   0x000055555540091b <+1>:	mov    rbp,rsp
=> 0x000055555540091e <+4>:	sub    rsp,0x10
   0x0000555555400922 <+8>:	mov    DWORD PTR [rbp-0x4],edi
   0x0000555555400925 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x0000555555400929 <+15>:	mov    eax,0x0
   0x000055555540092e <+20>:	call   0x5555554008d8 <header>
   0x0000555555400933 <+25>:	mov    eax,0x0
   0x0000555555400938 <+30>:	call   0x55555540082f <set_timer>
   0x000055555540093d <+35>:	mov    eax,0x0
   0x0000555555400942 <+40>:	call   0x55555540087d <get_key>
   0x0000555555400947 <+45>:	mov    eax,0x0
   0x000055555540094c <+50>:	call   0x5555554008ac <print_flag>
   0x0000555555400951 <+55>:	mov    eax,0x0
   0x0000555555400956 <+60>:	leave  
   0x0000555555400957 <+61>:	ret    
End of assembler dump.
(gdb) call (int) header
$1 = 1430259928
(gdb) call (int) header()
Keep this thing over 50 mph!
============================

$2 = 2
(gdb) call (int) get_key()
Creating key...
Finished
$3 = 9
(gdb) call (int) print_flag()
Printing flag:
PICOCTF{Good job keeping bus #24c43740 speeding along!}
$4 = 56

```

En otras palabras se utiliza el debugger para analizar el binario, primero se muestran las funciones, después se dirige a la función main para ver el funcionamiento y se observa que existe la llamada a la función `set_timer` .
Se crea un breakpoint en el main para poder ejecutarlo paso por paso.
Una vez en el debug del main se manda a llamar el header, después el get_key y se manda a llamar la función print_key. Todo esto saltando el set_timer. De esta forma se obtiene la bandera.

Bandera:
==PICOCTF{Good job keeping bus \#24c43740 speeding along!}==
## Notas adicionales

## Referencias
- Debugger de código libre https://www.sourceware.org/gdb/