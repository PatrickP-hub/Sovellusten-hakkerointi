# H4 Some Disassembly Required

## Työympäristö 6.2.2026

- Pöytäköne AMD Ryzen 5
- Linux 13 Debian Trixie
- Firefox

## x) Read/watch/listen and summarize

### Hammond 2022: https://www.youtube.com/watch?v=oTD_ki86c9I

- Videossa näytetään, miten käytetään Ghidra ohjelmaa, joka auttaa tutkimaan ohjelmia sisältä päin.
  
- Ghidran avulla muutetaan binääritiedosto helpommin luettavaan muotoon.

- Tärkeää on tietää koodissa mistä etsiä ja mitkä ovat oleellista koodissa.
  

### Eagly and Nancy 2020: https://learning.oreilly.com/library/view/the-ghidra-book/9781098125684/xhtml/ch02.xhtml#ch02lev29

- Tekstissä perehdytään myös muihin työkaluihin, joita käytetään binääritiedostojen "reverse engineeringissä"

- Ghidra yhdistää tekstissä käytyjen monien työkalujen ominaisuuksia yhteen ohjelmaan.


## a) Install Ghidra.

Latasin uudestaan Ghidran pöytäkoneelle, koska latasin sen viime viikolla läppärilleni mikä käyttää arm arkkitehtuuria.

Menin osoitteeseen: https://github.com/NationalSecurityAgency/ghidra?tab=readme-ov-file josta löysin zip filen versioon 12.0.2

Sitten avasin VirtualBoxista virtuualikoneen ja päivitin `sudo apt update` ja `sudo apt upgrade -y`

Tämän jälkeen latasin javan virtuaalikoneelle `sudo apt install openjdk-21-jdk -y`

Sen jälkeen oli aika tuoda zip paketti virtuaalikoneeseen `wget https://github.com/NationalSecurityAgency/ghidra/releases/download/Ghidra_12.0.2_build/ghidra_12.0.2_PUBLIC_20260129.zip`

Sitten purin paketin `unzip ghidra*.zip`

<img width="891" height="113" alt="image" src="https://github.com/user-attachments/assets/4a68120c-4176-42de-af76-8821c6cf2eba" />

Tämän jälkeen avasin Ghidran `./ghidraRun` komennolla

<img width="510" height="466" alt="image" src="https://github.com/user-attachments/assets/15167a8c-9546-457b-bd02-3b88caae8261" />

Ghidra oli installoitu ja valmiina käyttöön virtuaalikoneella

## b) rever-C. Reverse engineer the packd binary to C language with Ghidr

Latasin zip tiedoston ja unzippasin sen terminaalissa jonka löysin Lataukset kansiosta.

<img width="686" height="241" alt="image" src="https://github.com/user-attachments/assets/2b68abf1-4dc3-4dc3-8afc-4f2bf3c73095" />

Sitten Ghidrassa tein uuden projektin packd ja importtasin tiedoston `packd`

<img width="633" height="303" alt="image" src="https://github.com/user-attachments/assets/f474b59b-b776-44a4-9733-9f1a21315417" />

<img width="806" height="617" alt="image" src="https://github.com/user-attachments/assets/52ea6d8c-5ad9-4506-88b8-2d192770b537" />

Sitten avasin launching toolin `packd` tiedostolle ja analysoin sen valmiilla asetuksilla.

<img width="528" height="144" alt="image" src="https://github.com/user-attachments/assets/29c15e89-52f1-4cdd-8015-cc28e6931d89" />

Etsin ratkaisua seuraavaan kohtaan joku 2tuntia kun en löytänyt `main` osiota. Etsin binääriä tiedostosta, mikä voisi olla main mutta löysin vain `entryn` yritin sieltä etsiä, mutta se ei näyttänyt oikealta paikalta. Etsin vielä tietoa eri paikoista ja kokeilin unzippaa tiedostoa uudelleen ja analysoida sitä moneen kertaan mutta en päässyt eteenpäin. Sitten kysyin kaverilta neuvoa ja sanoi että jos lataa UPX se voisi toimia.

Latasin `sudo apt install upx` ja kansiossa missä minulla oli packd tiedosto annoin komennon `upx -d packd` joka unpackkasi 1 tiedoston

<img width="786" height="223" alt="image" src="https://github.com/user-attachments/assets/06126153-c6e7-43ae-af13-3a97d8729c5f" />

Tämän jälkeen kokeilin uudestaa ja main tuli näkyviin heti... 

<img width="1256" height="336" alt="image" src="https://github.com/user-attachments/assets/c0cc7ab5-b63c-464c-861e-35853a2f2c22" />

Sitten pääsin muuttamaan decompilee c-koodia. Vaihdoin muuttujan selkeämmäksi "input" ja local_28 kohdan vaihdoin salasana, koska se oli minusta selkeämpi.

<img width="604" height="302" alt="image" src="https://github.com/user-attachments/assets/cc0e6cd6-6b18-4b7e-835c-593c87890d80" />

Ohjelma siis kysyy mikä on salasana, kun käyttäjä kirjoittaa salasanan -> ohjelma vertaa sitä oikeaan salasanaan `strcmp` funktiolla

Jos salasana on oikein ohjelma hyväksyy käyttäjän ja jos salasana on väärin funktio palauttaa muun arvon eli hylkää sen.


## c) If backwards. Modify the passtr program's binary

Seuraavana aloitin taas lataamalla zip tiedoston ja purin sen `unzip` sekä varmuudella `upx -d passtr` komennoilla. Sitten pääsin muokkaamaan alkuperäistä c-koodia että käännän ehtolauseen toisinpäin. 

<img width="619" height="287" alt="image" src="https://github.com/user-attachments/assets/97655322-e76e-4bc2-92da-49577c7384c2" />

Etsin tietoa netistä miten voisin vaihtaa suoraan koodista ehtolausetta jotta salasana hyväksyy kaikki vaihtoehdot. Täältä löysin tietoa: https://medium.com/@anandrishav2228/reverse-engineering-for-beginner-0bf9b20542f7 vaihtaa 

`JNZ` -> `JZ`  eli jump if not zero to jump if zero, Patch instruction assemblen avulla. 

<img width="618" height="80" alt="image" src="https://github.com/user-attachments/assets/aced3bcb-56d1-49b8-8c24-63e5fe1676bf" />

<img width="196" height="20" alt="image" src="https://github.com/user-attachments/assets/d9caeace-f263-4ccc-aff8-cab1be778c1e" />

Tämän jälkeen tallensin tiedoston orginal filenä ja menin terminaaliin kokeilemaan toimiiko.

<img width="348" height="216" alt="image" src="https://github.com/user-attachments/assets/2811671d-2cb2-4245-b0cf-6834167df773" />

Annoin käyttöoikeudet tiedostolle `chmod +x` uutta exportettua tiedostoa. Tarkistin löytyykö tiedosto `ls -la`

<img width="848" height="215" alt="image" src="https://github.com/user-attachments/assets/1323f6b0-6c1a-457c-aac1-134c01cbfb2a" />

Sitten komento `./passtr_muokattu` joka kysyi salasanaa annoin väärän salasanan 

<img width="775" height="85" alt="image" src="https://github.com/user-attachments/assets/7ef6e4fe-a81c-4f2e-b668-3eede1e904be" />

Toimi! ja sitten kokeillaan vielä oikeaa salasanaa:

<img width="770" height="85" alt="image" src="https://github.com/user-attachments/assets/7f917b7b-f507-47d3-80b8-608d48891d2f" />

Tuloste todistaa että nyt väärä salasana toimi ja oikea ei toiminut.

## d) Nora CrackMe: Compile to binaries Tindall 2023: https://github.com/NoraCodes/crackmes

En ollut varma ymmärsinkö oikein pitikö tässä tehtävässä silmäillä vain README.md tiedostoa ja analysoida binäärejä. 

Silmäilin hetken README.md tiedostoa huomasin, että sielä oli tutoriaali: https://nora.codes/tutorial/an-intro-to-x86_64-reverse-engineering/ 

Aloitin tehtävän kloonaamalla githubista tiedostot

<img width="795" height="172" alt="image" src="https://github.com/user-attachments/assets/56cb130e-561b-4fce-be87-d300870c436d" />

Siirryin `cd crackmes` jossa tehtävät sijaitsivat

Varmistin että tiedostot oli vielä ladattu:

<img width="944" height="82" alt="image" src="https://github.com/user-attachments/assets/7b7b482a-9862-4a93-b7f0-de2258352caa" />

ja suoritin komennon  `make crackme01` jotta se kääntyi binääriksi. Oli aika aloittaa tehtävä

## e) Nora crackme01. Solve the binary.

Kokeilin ajaa ohjelmaa ./crackme01

<img width="543" height="45" alt="image" src="https://github.com/user-attachments/assets/402da43d-4600-478a-a50a-a953f95f2654" />

Tulosteessa "Need exactly one argument"

Tein uuden projektin Ghidraan ja importtasin crackme01 tiedoston sinne. 

Löysin sieltä main kohdasta salasanan, mutta tämä tuntui jotenki liian helpolta että tehtävä olisi tässä.

Ajoin ohjelman `./crackme01.64 password1`

<img width="650" height="45" alt="image" src="https://github.com/user-attachments/assets/6c3142f2-548c-4d5a-a5dc-b7bfe902864a" />

Tämä tulosti salasanan oikeaksi

Nora crackme01e kohdassa kokeilin lähestyä tehtävää stringsien avulla:

<img width="816" height="400" alt="image" src="https://github.com/user-attachments/assets/8381c0d4-dec0-45ce-b888-3c1c296b3384" />

Tästä voisi päätellä että salasana löytyyi mutta salasanassa oli huutomerkki joka näytti vähän oudolta. 

Melkein jo unohdin muuttaa `make crackme01e` komennon avulla siitä toimivan

Sitten kokeilin "./crackme01e.64 "slm!paas.k""

<img width="689" height="46" alt="image" src="https://github.com/user-attachments/assets/b79e87a7-b615-401d-b1d2-d1b619690cda" />

"event not found" tämän jälkeen kokeilin pelkillä normi hipsuilla mitä on myös python kurssilla opetettu

<img width="685" height="43" alt="image" src="https://github.com/user-attachments/assets/b6657d5c-a00e-43ba-9471-45bdde367278" />

Tämähän tehtävä meni yllättävän helposti.


## f) Nora crackme02

Ensimmäiseksi `make crackme02` Sitten importtasin sen Ghidraan ja katsoin decompile kohtaa `main` funktiosta

<img width="477" height="483" alt="image" src="https://github.com/user-attachments/assets/69d31b9e-6527-4ce6-a691-42d5de4b90c0" />

En oikein ollut varma mitä tästä jäi käteen sillä koodia oli enemmän. Rivillä 20 kuitenkin näkyi salasana "password1".

Kokeilin `strings` komennolla terminaalissa näkyisikö siellä vastausta

<img width="336" height="89" alt="image" src="https://github.com/user-attachments/assets/4978372d-037f-42cd-a3a8-b92eb44193f9" />

Sitten kokeilin salasanaa `./crackme02.64 password1` ja hipsuilla myös

<img width="685" height="132" alt="image" src="https://github.com/user-attachments/assets/a49ab995-36b2-4897-ac93-c61728dc965d" />

Ei ollut mikään oikein, sitten menin Ghidraan tarkastelemaan kohtaa `cVar2` kohtaa kaksoisklikkaamalla

Se laittoi suoraan minut oikealle riville tarkastelemaan sisältöä

<img width="980" height="132" alt="image" src="https://github.com/user-attachments/assets/261357a4-bc50-4d66-91b6-6d7ed5b9da00" />

Sitten kokeilin uudelleen terminaalissa

<img width="659" height="182" alt="image" src="https://github.com/user-attachments/assets/69842216-0337-48b6-9306-78f747e45c42" />

Ei silti mikään oikein... Tässä kohdassa ei ollut oikein mitään ajatuksia mitä seuraavaksi voisin tehdä muutakuin lukea noran tiedostoa: https://github.com/NoraCodes/crackmes crackme02 kohdasta

En halunnut vielä luovuttaa, mutta tässäkin oli kulunut niin kauan jo aikaa että kysyin tekoälyltäkin jo neuvoa mitä voisin tehdä. 

Täältä löysin paikan jossa pystyin Decryptoida salasanan esimerkiksi eri arvoilla: https://www.dcode.fr/ascii-shift-cipher

Laitoin salasanan `assword1` löysin +1 arvolla 

<img width="280" height="62" alt="image" src="https://github.com/user-attachments/assets/dde30cc4-cf41-4a74-8846-e6a9b5701367" />

<img width="669" height="54" alt="image" src="https://github.com/user-attachments/assets/ae55e133-6b38-4f62-a873-050df4eedb73" />

Tämä ei kuitenkaan toiminut...

Yritin ymmärtää mitä `cVar2 = 'p'` tarkoittaa tunnin verran ja tajusin että jos laitan vaan `password1` suoraan ASCII siirtoon numerolla 1 saan oikean vastauksen, eli minulta puuttui vain alusta `p` kirjain

<img width="799" height="170" alt="image" src="https://github.com/user-attachments/assets/71e21276-d48b-4c88-951b-b25d7366aac8" />

<img width="693" height="48" alt="image" src="https://github.com/user-attachments/assets/9b94743f-c820-43d9-aa42-1001548d89a2" />

En tiedä oliko tämä oikein tehty, mutta lopulta sain oikein niin olen tyytyväinen. Tehtäviin meni aikaa suunnilleen koko päivä aamusta iltaan ja luulen että opin näissä tehtävissä todella paljon Ghidrasta ja muutenkin reverse engineeringistä.


## Lähteet

Tero Karvinen Application Hacking: https://terokarvinen.com/application-hacking/#aikataulu

Hammond 2022: https://www.youtube.com/watch?v=oTD_ki86c9I

Eagly and Nancy 2020: https://learning.oreilly.com/library/view/the-ghidra-book/9781098125684/xhtml/ch02.xhtml#ch02lev29

Reverse Engineering for Beginner: https://medium.com/@anandrishav2228/reverse-engineering-for-beginner-0bf9b20542f7

Tindall 2023: https://github.com/NoraCodes/crackmes

