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


## d) Nora CrackMe: Compile to binaries Tindall 2023: https://github.com/NoraCodes/crackmes
 
## e) Nora crackme01. Solve the binary.

## f) Nora crackme02


## Lähteet

Tero Karvinen Application Hacking: https://terokarvinen.com/application-hacking/#aikataulu

Hammond 2022: https://www.youtube.com/watch?v=oTD_ki86c9I

Eagly and Nancy 2020: https://learning.oreilly.com/library/view/the-ghidra-book/9781098125684/xhtml/ch02.xhtml#ch02lev29

Tindall 2023: https://github.com/NoraCodes/crackmes

