# Vault-door-training
#picoCTF2019 #REVERSING
## Objetivo
Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: [VaultDoorTraining.java](https://jupiter.challenges.picoctf.org/static/1afdf83322ee9c0040f8e3a3c047e18b/VaultDoorTraining.java)
## Solución
Al descargar el archivo al final del archivo java viene dentro del código proporcionado.
picoCTF{w4rm1ng_Up_w1tH_jAv4_eec0716b713}

```bash
┌──(kali㉿kali)-[~/Downloads/REVERSING/vdt]
└─$ java VaultDoorTraining      
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{w4rm1ng_Up_w1tH_jAv4_eec0716b713}
Access granted.

```

## Referencias
