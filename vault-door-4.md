# vault-door-4
#picoCTF2019 #REVERSING 
## Objetivo
This vault uses ASCII encoding for the password. The source code for this vault is here: [VaultDoor4.java](https://jupiter.challenges.picoctf.org/static/09d3002ae349631324a17e2255ae8df2/VaultDoor4.java)
## Solución
Dentro del código se encuentra la contraseña cifrada en distintas bases. Base decimal, hexadecimal, octal y caracteres comunes.

```java
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 0143, 061 ,
            '9' , '4' , 'f' , '7' , '4' , '5' , '8' , 'e' ,

```

Una vez más se modifica el código fuente para desactivar funciones que no son utiles y se almacena la bandera en una cadena para poder ser mostrada en consola.

```bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/vd4]
└─$ javac VaultDoor4.java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
                                                                                 
┌──(kali㉿kali)-[~/Downloads/REVERSING/vd4]
└─$ java VaultDoor4      
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
jU5t_4_bUnCh_0f_bYt3s_c194f7458e
Access granted.

```
## Notas adicionales

## Referencias
