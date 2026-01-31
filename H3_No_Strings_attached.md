# H3 No Strings Attached

### Työympäristö

- Oracle VirtualBox
- Linux Debian 13 trixie
- Macbook Air M2

Aloitin tehtävänän 31.1 klo 8.30 ja tein tehtävän läppärilläni, sillä en olin reissussa eikä normaali työasemaa ollut käytössä.

## a) Strings.

Alussa latasin tarvittavat paketit ja päivitin `sudo apt update` & `sudo apt upgrade`

Sitten annoin vielä komennon `sudo apt install build-essential binutils coreutils` joka asentaa kehitys- ja analyysityökaluja, joita tarvitset C-ohjelmien kääntämiseen ja binäärien tutkimiseen.
Tähän otin apua chatgpt:ltä.

Seuraavaksi oli aika ladata zip paketti Tero Karvisen sivulta: https://terokarvinen.com/application-hacking/ 

Tämän jälkeen hain paketin

<img width="829" height="19" alt="image" src="https://github.com/user-attachments/assets/73293a38-e990-4ac3-8934-404fda807b31" />

Kun paketti oli ladattu niin unzippasin paketin virtuaalikoneella `unzip ezbin-challenges.zip` ja sitten siirryin `cd challenges` ja `cd passtr`

Tämän jälkeen oli aika etsiä salasana ja lippu stringsin avulla

Tähän käytin `strings passtr`

<img width="829" height="383" alt="image" src="https://github.com/user-attachments/assets/c45337aa-7b1d-4487-bd61-cd1ad0772d62" />

Salasana ja lippu löydetty, mutta tarkistusta ajamalla ohjelmaa `./file passtr`ei pysty suorittaan kun tehtävän teen ARM64 arkkitehtuurilla.


## b) Make a new version of the passtr.c program

Tässä tehtävässä piti tehdä uusi versio C-kielellä sillä tavalla ettei salasana tule näkyviin. 

Etsin tiedoston `ls` komennolla ja löysin passtr.c tiedoston jota pääsin muokkaamaan. `nano passtr.c`

<img width="901" height="383" alt="image" src="https://github.com/user-attachments/assets/15646ea7-409f-4d0f-a134-8daf01047359" />



## c) Packd

## Lähteet

Sovellusten hakkerointi: https://terokarvinen.com/application-hacking/ 



