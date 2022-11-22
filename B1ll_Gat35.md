# B1ll_Gat35
#picoCTF2019 #REVERSING 
## Objetivo
Can you reverse this [Windows Binary](https://jupiter.challenges.picoctf.org/static/0ef5d0d6d552cd5e0bd60c2adbddaa94/win-exec-1.exe)?
## Solución
- instalar wine
``` bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/bill_gates]
└─$ sudo dpkg --add-architecture i386
┌──(kali㉿kali)-[~/Downloads/REVERSING/bill_gates]
└─$ sudo apt update    
┌──(kali㉿kali)-[~/Downloads/REVERSING/bill_gates]
└─$ sudo apt install wine

```

Vemos que la ejecución del programa es la siguiente.

``` bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/bill_gates]
└─$ wine win-exec-1.exe
Input a number between 1 and 5 digits: 32
Initializing...
Enter the correct key to get the access codes: 52
Incorrect key. Try again.
```

Se abre el proyecto en ghidra y se busca una cadena

![[Pasted image 20221115093917.png]]

Dentro de ghidra se modifica una instrucción JNZ por JNC para eliminar un if dentro del programa.

## Notas adicionales
Wine es una capa de compatibilidad que permite correr aplicaciones de windows, es una especie de emulador.

## Referencias
https://es.wikipedia.org/wiki/Portable_Executable