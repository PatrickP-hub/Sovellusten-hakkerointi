# H3 No Strings Attached

### Työympäristö

- Oracle VirtualBox
- Linux Debian 13 trixie
- Firefox
- Macbook Air M2

Aloitin tehtävänän 31.1 klo 8.30 ja tein tehtävän läppärilläni, sillä olin reissussa eikä normaali työasemaa (pöytäkone) ollut käytettävissä.

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

Tässä siis alkuperäinen nano tiedosto.

Tehtävänannossa suositeltiin XOR-obfuskointia, joka oli minulle aivan uusi termi. Etsin tietoa netistä obfuskoinnista, ja myös tapoja millä saisi salasanan piilotettua ettei se näkyisi selväkielisenä binäärissä. Täältä löysin jotain vinkkejä: https://www.threatdown.com/blog/nowhere-to-hide-three-methods-of-xor-obfuscation/

Kysyin myös ChatGPT tekoälyltä apua c kielellä obfuskointiin. Tässä siis salasana on muutettu ja se puretaan ajonaikana.

<img width="1796" height="1390" alt="image" src="https://github.com/user-attachments/assets/677d7cfa-97b3-424c-8289-9183f6bd927a" />

Koodissa siis salasana on piilotettu muuttamalla normaalikirjaimet obfuskaamalla eli piilottamalla "0x muotoon"

Sitten oli aika testata tuleeko salasana enään näkyviin komennolla `./passtr`

<img width="898" height="64" alt="image" src="https://github.com/user-attachments/assets/dbbac5e7-b39d-4512-9c23-2c84358a0327" />

Ei tullut enään, joten obfuskointi näytti toimivan. Tässä tehtävässä kesti kuitenkin aikaa keksiä miten muutan selkokielisen salasanan piilotettuihin kirjaimiin. 

## c) Packd

Aluksi latasin toisen zip paketin Teron sivuilta: https://terokarvinen.com/application-hacking/ 

Sitten toin samanlailla zip paketin virtuaalikoneelle kuin a) tehtävässä. Siirryin kansioon challenges ja sieltä kansioon packd `cd` komennolla.

Kokeilin aluksi samaa kuin edellisessä tehtävässä käyttäen `strings packd` komentoa. 

<img width="1796" height="186" alt="image" src="https://github.com/user-attachments/assets/36a579e5-6a9b-4386-9d48-d12811d0a91c" />

Tässä kohdassa tuli kuitenkin epäonnistunut tuloste sillä tehtävässä tarvitaan UPX:ää.

Latasin tarvittavan paketin `sudo apt install upx-ucl` tämän jälkeen purin vielä pakatun binäärin
`upx -d packd`

<img width="898" height="181" alt="image" src="https://github.com/user-attachments/assets/5ec07057-e484-4211-b9fa-9c2614b76c2a" />

Ja kokeilin uudestaan komentoa `strings packd`

<img width="898" height="375" alt="image" src="https://github.com/user-attachments/assets/1bafb7ca-8270-4da3-a759-5de42d49c552" />

Komento toimi, lippu ja salasana tulivat näkyviin. Tehtävää ajatellen onneksi katsoin mitä tulosteessa luki ja tajusin heti ladata UPX paketin, koska ilman sitä tehtävään olisi voinut mennä ikuisuus. 

Tässä vielä kuvat lipusta ja salasanasta:

<img width="653" height="35" alt="image" src="https://github.com/user-attachments/assets/abfb9669-3b63-4f48-9bf8-f2f7ad08ce21" />

Minusta tämä jälkimmäinen tehtävä oli paljon selkeämpi ja helpompi kuin b) kohdan tehtävä. Tehtävää tehdessä myös huomasi että Linux:in komentorivin käyttö alkoi tuntua jo paljon sulavammalta ja peruskomennot tulivat ulkoimuistista. Tehtävätkin oli myös kivoja ja mielestäni opin paljon uutta. 


## Lähteet

Sovellusten hakkerointi: https://terokarvinen.com/application-hacking/ 

Nowhere to Hide: Three methods of XOR obfuscation: https://www.threatdown.com/blog/nowhere-to-hide-three-methods-of-xor-obfuscation/



