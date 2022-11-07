# vault-door-1
#picoCTF2019 #REVERSING 
## Objetivo
This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: [VaultDoor1.java](https://jupiter.challenges.picoctf.org/static/29b91e638ccbd76aaa8c0462d1c64d8d/VaultDoor1.java)
## Solución
La contraseña una vez más se encuentra dentro del código fuente, pero dividido por caracteres y colocados en posiciones distintas a las que corresponde.
Se coloca el código de comprobación de caracteres dentro de un archivo de texto para poder hacer operaciones con la linea de comandos.
Se completan los digitos dentro de la comprobación a dos números para que los comandos de la terminal puedan ordenarlos de forma correcta.
Mediante la siguiente serie de comandos podemos obtener la bandera.
```bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/vd1]
└─$ cat laflag.txt| sort | awk '{print($3)}' | tr -d "'" | tr -d "\n" | tr -d ";"
d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0 
```

picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0}

## Notas adicionales

## Referencias
