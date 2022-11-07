# vault-door-3
#picoCTF2019 #REVERSING 
## Objetivo
This vault uses for-loops and byte arrays. The source code for this vault is here: [VaultDoor3.java](https://jupiter.challenges.picoctf.org/static/a648ca6dd275b9454c5d0de6d0f6efd3/VaultDoor3.java)
## Solución
Se modifica el código fuente dado para aplicarle los ciclos utilizados para descomponer la cadena dada, de tal manera que se descompone de forma inversa la cadena con la cual se compara la contraseña dada y se obtiene la contraseña real.

```bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/vd3]
└─$ javac VaultDoor3.java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
                                                                                 
┌──(kali㉿kali)-[~/Downloads/REVERSING/vd3]
└─$ java VaultDoor3       
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
jU5t_a_s1mpl3_an4gr4m_4_u_1fb380
Access granted.

```
## Notas adicionales

## Referencias
