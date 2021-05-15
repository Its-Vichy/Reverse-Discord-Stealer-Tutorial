<h1 align="center">REVERSE TOKEN GRABBER</h1>

<p align="center">
  <b>🖤 Follow me here:</b><br>
  <a href="https://discord.gg/aMs5BHuyaU">Discord</a> |
  <a href="https://www.youtube.com/channel/UC09GPm24_rdeOXa5KOmhDnw">YouTube</a> |
  <a href="https://twitter.com/its_vichy">Twitter</a> |
  <a href="https://github.com/Its-Vichy">Github</a>
  <br><br>
  <img src="https://steamuserimages-a.akamaihd.net/ugc/939465072079337699/A44A2D24BB987267F26C56440F51A0B468481222/">
  <br><br>
</p>

#

# 📜 Liens utiles.

- [PyInstxtractor - Python Decompiler](https://github.com/extremecoders-re/pyinstxtractor)
- [DE4JS - JavaScript Deobfuscator](https://lelinhtinh.github.io/de4js/)
- [VirusTotal](https://www.virustotal.com/gui/)
- [DnSpy](https://github.com/dnSpy/dnSpy)
- [Script](https://cdn.discordapp.com/attachments/842802089763012669/842900999475036221/Script.rar)
- [Curl](https://fr.wikipedia.org/wiki/CURL)

#

# 🔎 Premières investigations:

  - Tout d'abbord, avant de commencer à chercher réellement nous avons besoin d'**informations** sur l'exécutable en question (*language, détections*). Parfois obtenir ces informations peut se révéler être une aide capitale pour gagner un maximum de temps.

## 1. Rechercher des potentielles menaces:

  - Grâce à [Virus Total](https://www.virustotal.com/gui/) nous pourrons savoir beaucoup d'informations, dont:
    * Le Webhook (se que l'on cherche principalement)
    * Le Type de menace

  - Certains grabbers sont très bien [FUD](https://www.undernews.fr/fiches-pirates/techniques-de-pirates-comment-les-cybercriminels-contournent-les-antivirus) et sont donc très peux voir non détéctée

![](https://media.discordapp.net/attachments/842802089763012669/842899093788819464/unknown.png)
![](https://media.discordapp.net/attachments/842802089763012669/842896683125178418/unknown.png)

## 2. Rechercher des chaînes de caractères:

  - Grâce à l'outil [Strings](https://docs.microsoft.com/en-us/sysinternals/downloads/strings), nous allons pouvoir analyser les [chaînes de caractères](https://fr.wikipedia.org/wiki/Cha%C3%AEne_de_caract%C3%A8res) présents dans l'exécutable ou dans des fichiers particuliers comme nous le verront plus tard. Il est installé nativement sous certaines [distribution linux](https://fr.wikipedia.org/wiki/Distribution_Linux) comme [Kali Linux](https://fr.wikipedia.org/wiki/Kali_Linux).
  
  - Son utilisation est très simple:
  ```
  Strings v2.53 - Search for ANSI and Unicode strings in binary images.
Copyright (C) 1999-2016 Mark Russinovich
Sysinternals - www.sysinternals.com

usage: strings64.exe [-a] [-f offset] [-b bytes] [-n length] [-o] [-s] [-u] <file or directory>
-a     Ascii-only search (Unicode and Ascii is default)
-b     Bytes of file to scan
-f     File offset at which to start scanning.
-o     Print offset in file string was located
-n     Minimum string length (default is 3)
-s     Recurse subdirectories
-u     Unicode-only search (Unicode and Ascii is default)
-nobanner
       Do not display the startup banner and copyright message.
```
  - L'option `-n` nous seras très utile, elle nous permet de récupérer uniquement les chaînes de caractères d'une longueur minimal, pratique pour un webhook 🦖

#

# 🔎 La Deobfuscation:

  - Généralement une des techniques les plus utiliser afin de protéger son code est l'[Offuscation](https://fr.wikipedia.org/wiki/Offuscation), elle est très efficace mais toute personne assez motivée peut arriver à débusquer plus ou moins partiellement, pour nous aider des projets tel que [DE4JS](https://lelinhtinh.github.io/de4js/) pour le JavaScript ou encore [PyInstxtractor](https://github.com/extremecoders-re/pyinstxtractor) pour le python ( du moins pour décompiler )

## 1. Programmes open source

  - Il est très probable que le [néophyte](https://fr.wikipedia.org/wiki/Script_kiddie) ayant poster le grabber l'est repris depuis Github, il y a donc de grande chance que vous trouvez le code sur github. Sur cet exemple j'ai pu retrouve le WebHook très facilement, et le récupérer comme nous le verront ci-dessous
  
  ![](https://media.discordapp.net/attachments/842811981807222804/842852017348673536/unknown.png)
  ![](https://media.discordapp.net/attachments/842811981807222804/842851719888109638/unknown.png)
  
## 2. Des signes qui ne pardonnent pas

  - Lors de la deobfuscation, vous pourrez trouver tous un tas d'indices ! *Le code ne ment jamais 💪*
  
  ![](https://media.discordapp.net/attachments/842811981807222804/842833849369362482/unknown.png)
  ![](https://media.discordapp.net/attachments/842811981807222804/842833123212263434/unknown.png)

## 3. L'utiliser des Log

- Une fois que vous saviez qu'elle est la variable qui contient le web Hook, il vous faut la connaître c'est le moment de `console log()`, `print()`... sur votre variable,
  Veuillez garder à l'esprit que vous connaissez peut de ce code veuillez donc être sûr de désactiver la fonction qui envoie le token... sinon vous allez avoir l'air pas très malin !


![](https://media.discordapp.net/attachments/842811981807222804/842852517984337930/unknown.png)

## 4. Apprécier le résultat 😎:

![](https://media.discordapp.net/attachments/842811981807222804/842916423650246656/unknown.png)

#

# 🧠 Utilisation de l'outil *Curl*:

  - [Curl](https://fr.wikipedia.org/wiki/CURL) est un outil puissant, installé nativement sous Linux, et sous Windows également !

## 1. Suprimmer un webhook avec curl:
  
  - L'option `-X DELETE` sera notre amie !, en effet elle permet de faire une requête de [méthode `DELETE`](https://developer.mozilla.org/fr/docs/Web/HTTP/Methods) et ainsi supprimer le webhook 🖕

![](https://images-ext-1.discordapp.net/external/ut3cVPPlQhctgNbUkHQ8RTfAPleQiYmqW2IYIl2zqTY/https/media.discordapp.net/attachments/842802089763012669/842898314282139689/unknown.png)

  - Un simple `curl` suivit de l'URL nous permettra d'obtenir des informations sur le web Hook, ce qui correspond à une [méthode `GET`](https://developer.mozilla.org/fr/docs/Web/HTTP/Methods)

![](https://images-ext-1.discordapp.net/external/Hk9W4VNU57pUf4C1Pyih-4I6H41ClxEuk7-JBY7v6mU/https/media.discordapp.net/attachments/842802089763012669/842896986218430484/unknown.png)
