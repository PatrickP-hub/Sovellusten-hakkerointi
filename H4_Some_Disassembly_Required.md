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






## b) rever-C. Reverse engineer the packd binary to C language with Ghidr

## c) If backwards. Modify the passtr program's binary

## d) Nora CrackMe: Compile to binaries Tindall 2023: https://github.com/NoraCodes/crackmes
 
## e) Nora crackme01. Solve the binary.

## f) Nora crackme02


## Lähteet

Tero Karvinen Application Hacking: https://terokarvinen.com/application-hacking/#aikataulu

Hammond 2022: https://www.youtube.com/watch?v=oTD_ki86c9I

Eagly and Nancy 2020: https://learning.oreilly.com/library/view/the-ghidra-book/9781098125684/xhtml/ch02.xhtml#ch02lev29

Tindall 2023: https://github.com/NoraCodes/crackmes

