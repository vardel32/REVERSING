# reverse_cipher
#picoCTF2019 #REVERSING 
## Objetivo
We have recovered a [binary](https://jupiter.challenges.picoctf.org/static/31c9b832d036a10daeef52d8b4290ef0/rev) and a [text file](https://jupiter.challenges.picoctf.org/static/31c9b832d036a10daeef52d8b4290ef0/rev_this). Can you reverse the flag.
## Solución
Primeramente nos encontramos con dos archivos, un archivo binario que cifra un texto dado, y la bandera cifrada con el cifrado que crea el binario.
No es un cifrado ROT13, ni Base64, ni ningún otro cifrado, es un cifrado especial.
rev es un archivo ELF de linux, Exdcutable an Linkeable Format. Un archivo ELF están conformadas por una serie de secciones especificas que contienen información particular.
rev es un archivo de 64bits.
En este caso en particular nos interesa la sexio ".text" y ".data"
Mediante objdump se puede observar que el programa rev al ser ejecutado busca un archivo llamada "flag.txt" para cifrarlo.

```bash 
┌──(kali㉿kali)-[~/Downloads/REVERSING/reverse_cipher]
└─$ objdump -dj .rodata rev

rev:     file format elf64-x86-64


Disassembly of section .rodata:

0000000000002000 <_IO_stdin_used>:
    2000:	01 00 02 00 00 00 00 00 72 00 66 6c 61 67 2e 74     ........r.flag.t
    2010:	78 74 00 61 00 72 65 76 5f 74 68 69 73 00 00 00     xt.a.rev_this...
    2020:	4e 6f 20 66 6c 61 67 20 66 6f 75 6e 64 2c 20 70     No flag found, p
    2030:	6c 65 61 73 65 20 6d 61 6b 65 20 73 75 72 65 20     lease make sure 
    2040:	74 68 69 73 20 69 73 20 72 75 6e 20 6f 6e 20 74     this is run on t
    2050:	68 65 20 73 65 72 76 65 72 00 70 6c 65 61 73 65     he server.please
    2060:	20 72 75 6e 20 74 68 69 73 20 6f 6e 20 74 68 65      run this on the
    2070:	20 73 65 72 76 65 72 00                              server.

```

Se instala ghidra para analizar bianrios.

```bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/reverse_cipher]
└─$ sudo apt install ghidra   
```

Mediante Ghidra para analizar el binario se crea un nuevo proyecto y después se analiza. Se pude obtener el código decompilado en lenguaje C. Mediante el decompilado se puede observar el funcionamiento del archivo.
El decompilado contiene variables con nombre asignados por Ghidra, se pueden renombrar las variables para darle un poco más de coherencia al decompilado.
El proceso de cifrado utilizado por el programa es el siguiente:
```C
  for (j = 8; (int)j < 0x17; j = j + 1) {
    if ((j & 1) == 0) {
      rev = flag[(int)j] + '\x05';
    }
    else {
      rev = flag[(int)j] + -2;
    }
```

Básicamente si la posición del carácter dada es par se le suma un '/x05' y si el carácter es non se le resta '2'.
Se realiza un script en python para descifrar la bandera.

```python
cifrado = open('rev_this', 'r').read()
print(cifrado)
flag = ''
#Se obtienen los caracteres de la bandera
for posicion in range(8,len(cifrado)-1):
        #Proceso de descifrado, se aplica el proceso inverso al cifrado
        if posicion & 1 == 0:
                #se obtiene el valor ASCII del caracter
                #Se hace la resta y se almacena en la bandera
                flag += chr(ord(cifrado[posicion])-5)
        else:
                #Si es una posicion non entonces se le suman 2
                flag += chr(ord(cifrado[posicion])+2)
print('picoCTF{'+flag+'}')

```

```bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/reverse_cipher]
└─$ python3 xploit.py 
picoCTF{w1{1wq85jc=2i0<}
picoCTF{r3v3rs37ee84d27}
```

Bandera:
==picoCTF{r3v3rs37ee84d27}==

## Notas adicionales
- La herramienta objtdump permite obtener información de programas dados.
- La herramienta readelf también despliega información sobre archivos ELF.
## Referencias
https://es.wikipedia.org/wiki/Executable_and_Linkable_Format