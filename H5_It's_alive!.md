# H5 It's Alive!

### Työympäristö: 16.2.2026

- Oracle VirtualBox
- Debian 13 Trixie
- Amd Ryzen 5
- Firefox

Ennen kun lähdin liikkeelle latasin tarvittavat paketit ja asensin GNU Debuggerin omalle työympäristölleni. Ohjeet löysin moodlesta 01-GDB.pdf tiedostosta:

`gdb --version` katsoin onko GNU Debuggeria ladattu: ei löytynyt, eli aloitin lataamalla sen `sudo apt-get install gdb`. 

## a) Lab1. Investigate what's wrong with the program and how to fix it

Aloitin lataamalla moodlesta kansion "dynaaminen analyysi.zip" kansion jossa tehtävät oli. Unzippasin kansion `unzip` komennolla ja sitten siirryin tarkastelemaan lab1.zip tiedostoa. `unzip lab1.zip` ja siirryin `cd lab1` ja katsoin oikean tiedoston kansiossa `ls`

<img width="496" height="44" alt="image" src="https://github.com/user-attachments/assets/fbf8bbd5-6a7b-4330-aa16-d7e88b6d456c" />

Uskoisin että `gdb_example` tiedosto oli oikea, sillä se oli ajettava tiedosto. Käänsin tiedoston luettavaksi `g++ gdb_example1 -o lab1`

Sitten ajoin tiedoston `gdb ./gdb_example1` ja katsoin `l` eli listaamalla seuraavat lähdekoodit ja uudestaan `l` sain kokonaan näkyviin lähdekoodin.  

<img width="468" height="272" alt="image" src="https://github.com/user-attachments/assets/8f5d8931-446f-45b9-9679-5607f8148d2c" />

Pysäytin riville 12 `break 12` ja `run` komennolla ajoin ohjelmaa 

<img width="614" height="181" alt="image" src="https://github.com/user-attachments/assets/d443904d-82dc-44ac-961b-e9f8d9e6fe88" />

Huomasin kohdassa breakpoint 1 rivillä 14 char * bad_message = NULL; siirryin eteenpäin komennolla `next` ja pysähdyin kohtaan riville 17 josta menin katsomaan `step` funktioon sisään 

<img width="530" height="124" alt="image" src="https://github.com/user-attachments/assets/a7c4d70b-29d8-44fb-b6dc-3a660a34704a" />

Aloitin uudelleen ajamaan ohjelman ja sain rivillä 7 segmentation fault

<img width="496" height="75" alt="image" src="https://github.com/user-attachments/assets/9ccb6eaf-c236-4a14-ae09-266ee9bb478a" />

Tähän jouduin käyttämään tekoälyä, sillä minulla ei ollut mitään ideaa, miten voisin koodia alkaa muuttamaan että ongelma ratkeisi. Promptina: "Ohjelma antoi signal SIGSEGV, Segmentation fault ja koodissa bad_message = NULL; antaa ensimmäisen breakpointin, miten voin korjata ongelman?"

## b) Lab2. Find out the password and flag + write a report on how it opened

## c) Lab3. Try Nora Crackmes exercises tasks 3 and 4


## Lähteet

Application Hacking 2026: https://terokarvinen.com/application-hacking/#aikataulu

Tindall 2023: https://github.com/NoraCodes/crackmes
