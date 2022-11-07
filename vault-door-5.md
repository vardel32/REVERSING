# vault-door-5
#picoCTF2019 #REVERSING 
## Objetivo
In the last challenge, you mastered octal (base 8), decimal (base 10), and hexadecimal (base 16) numbers, but this vault door uses a different change of base as well as URL encoding! The source code for this vault is here: [VaultDoor5.java](https://jupiter.challenges.picoctf.org/static/0a53bf0deaba6919f98d8550c35aa253/VaultDoor5.java)
## Solución
Se utilizó URL encode y después se le aplicó un cifrado en base 64, la idea es eliminar el cifrado en b64 y posteriormente se aplica un URL decode.
picoCTF{c0nv3rt1ng_fr0m_ba5e_64_0b957c4f}

## Notas adicionales
URL encode existe pues existen caracteres especiales que un servidor no puede leer, son codificados de tal forma que la url enviada sean solo caracteres ascii
## Referencias
