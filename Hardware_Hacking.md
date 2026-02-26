# Hardware Hacking moodle

### Työympäristö 26.02.2026

- Oracle VirtualBox
- Linux Debian 13 Trixie
- Firefox
- AMD Ryzen 5 2600

## 1. decrypt firmware image

Aloitin tehtävän lataamalla https://github.com/robbins/tp-link-decrypt sivulta tiedoston ja kloonasin sen `git clone` komennolla virtuaaliympäristöön. Tämän jälkeen siirryin tiedostoon `cd tp-link-decrypt` ja pääsin tarkastelemaan tiedostoja. 

Teimme jonkun verran tätä tehtävää jo tunnilla aiemmin ja kerron tähän raporttiin jo asioita mitä aloitin ja kerkesin tekemään. 

1. Katsoin README.md tiedostoa ja sen ohjeita
2. Latasin TapoV3 firmwire binaryn `aws s3 cp s3://download.tplinkcloud.com/firmware/Tapo_C200v3_en_1.4.2_Build_250313_Rel.40499n_up_boot-signed_1747894968535.bin Tapo_C200v4_en_1.4.2.bin --no-sign-request`
3. Sekä kamera tiedoston `wget https://hhmoodle.haaga-helia.fi/mod/resource/view.php?id=3617382`
4. Ajoin tarvittavat skriptit `./preinstall.sh` ja `./extract_keys.sh` näihin meni hetki aikaa. 
5. Latasin binwalkin ja muut tarvittavat työkalut.
6. Ajoin komennon make bin/tp-link-decrypt

<img width="1606" height="246" alt="image" src="https://github.com/user-attachments/assets/e4ded54f-9168-404e-85be-d6887ca68cfe" />

Tämän jälkeen kun olin saanut käännettyä tiedoston luettavaksi oli aika siirtyä seuraavaan kohtaan.
   

## 2. Analyse the image file

Tarkastelin tiedostoja mitä löysin ja uskoisin `view.php` tiedoston olevan kuva tiedosto

<img width="1606" height="202" alt="image" src="https://github.com/user-attachments/assets/971f997e-52d5-44c9-b672-18402d1ed857" />

katsoin eka tiedostoa `cat example.jpg` komennolla mutta tiedostosta ei saanut oikein irti mitään. Sitten `strigs` komennolla

<img width="1598" height="428" alt="image" src="https://github.com/user-attachments/assets/69ab8dd7-5834-4706-819b-76a9eba119e5" />

Tästä näkyi jo enemmän kuvan sisältöä, mutta en oikein osannut analysoida kuvasta mitään järkevää. Sitten vielä `binwalk` komennolla kokeilin, ja sain selville että kuva on JPEG tiedosto joka käyttää JFIF standardia. Kuvasta näkee myös sen että tiedostossa ei ole sisäänrakennettuja koska hexadecimal arvo on `0x0` . Jatkoin analysointia jos vielä löytäisin jotain muuta hyödyllistä. Rupesin miettimään että `strings`komennolla kuitenkin tuli paljon sisältöä, mutta `binwalk` komennolla tiedosto oli kuitenkin "tyhjä" tämä herätti epäilyksiä. 

<img width="651" height="115" alt="image" src="https://github.com/user-attachments/assets/94067d73-a8d5-4b5b-95fa-5c2af4457001" />

En kuitenkaan löytänyt `main` kohtaa stringsistä tai muuta mistä olisi voinut päätellä että ohjelmassa olisi mitään ajettavaa joten jatkoin eteenpäin. 

Kokeilin alussa lähteä liikkeelle etsimällä dump tiedostoa. Olin ladannut jo sen aluksi mutta sitten kokeilin `binwalk` komennolla Tapo_C200v5 tiedostoa ja tässä sain mielenkiintoista tietoa että olisiko tämä sittenkin se kuva tiedosto mitä äskön yritin etsiä.

<img width="1606" height="322" alt="image" src="https://github.com/user-attachments/assets/9cf0c16d-e0ed-442e-a5fa-d617ad2b1b8e" />

Kuten kuvasta näkyy "image id:9" ja image size, tämä taitaa olla se tehtävässä haettava kuva tiedosto. Tässä kuva tiedostossa myös oli mielenkiintoista se, että siinä on `JBOOT` osio joten se voisi viitata laiteohjelmiston käynnistysosaan. Mikä on tärkeä osa firmwarea. Jätin tämän hetkeksi rauhaan ja siirryin tekemään 3 tehtävää. 

## 3. extract rootfs from the dump file

Latasin `dump` tiedoston ja yritin extractata rootfs. Menin `cd Downloads` kansioon johon dump tiedosto oli ladattu ja sitten kokeilin aloittaa taas komennolla `binwalk` etsimään tietoa dump tiedostosta. 

Löysin videon missä opetettiin samaa asiaa ja tässä tehtävässä käytin sitä työkaluna: https://www.youtube.com/watch?v=-AYmTMILsM8 

<img width="1608" height="1352" alt="image" src="https://github.com/user-attachments/assets/68f2189d-525f-41b2-85ee-58eb7a4f4aa7" />

Tarkistelin tiedoston koodia ja yritin etsiä mikä on tarpeellista tässä tehtävässä ja lopuksi scrollasin ihan alas ja löysin sieltä `squashfs` tiedostojärjestelmän mikä herätti heti kiinnostusta eli se liittyy todennäköisesti jotenkin `rootfs` tiedostossa. 

<img width="1608" height="184" alt="image" src="https://github.com/user-attachments/assets/94fb13f2-4038-4612-9110-ad030578239f" />

Hetken yritin miettiä miten pääsisin tässä kohdassa eteenpäin, mutta en keksinyt ratkaisua muutakuin tyytyä tekoälyltä apua. "Miten pääsen tarkastelemaan squashfs tiedostojärjestelmää" Tämä antoi tulosteeksi komennon ja selitykset: Jälkeenpäin huomasin, että ohjeet tälle samalle komennolle löytyi myös osoitteesta: https://quentinkaiser.be/security/2025/07/25/rooting-tapo-c200/ mitä opettaja oli neuvonut käyttämään tehtävässä.

<img width="1424" height="634" alt="image" src="https://github.com/user-attachments/assets/55bf007e-4cf1-4097-9b2d-3f8de81edc3c" />

Sitten annoin komennon:

<img width="1608" height="210" alt="image" src="https://github.com/user-attachments/assets/32943a5e-366e-463c-86d8-9f2b297f5cd7" />

Ja siirryin `unsquashfs` komennolla purkamaan `rootfs.sqsh` tiedostoa.

<img width="799" height="254" alt="image" src="https://github.com/user-attachments/assets/66b0b594-8ca0-400e-954f-f556071708da" />

Tämän jälkeen katsoin mitä se sisälsi `ls` komennolla

<img width="1598" height="84" alt="image" src="https://github.com/user-attachments/assets/c37eff92-ca79-4209-87fc-b4a47adc70a5" />

Tehtävässä oli tarkoituksena purkaa root file system ja uskoisin että tämä oli onnistuneesti tehty dump filessä.


## 4. extract rootfs from the image file

Tässä tehtävässä kokeilin edetä samalla tavalla kuin äsköisessä tehtävässä olettaen että oikea tiedosto on `Tapo_C200v5` tiedosto. Katselin taas `binwalk` komennolla ja kokeilin purkaa `jboot_part.bin` tiedoston manuaalisesti komennolla `dd` 

<img width="1598" height="206" alt="image" src="https://github.com/user-attachments/assets/7d20000a-b36f-483f-ad20-8b064291c7b8" />

Tämän jälkeen kokeilin taas `unsquashfs` komennolla purkaa jos se löytäisi sen squashfs-paketista mutta se ei toiminut.

<img width="1598" height="82" alt="image" src="https://github.com/user-attachments/assets/560f10ec-b157-4e02-a33c-16f5a040a3f4" />

Tarkastelin tiedoston `jboot_part.bin` hexakoodia ja yritin etsiä jotain hyödyllistä `strings` komennoilla, mutta tuntui että jumitin vaan paikallaan enkä päässyt eteenpäin. 

Komennolla `ls -lh` katselin tiedostoa josta, tuli selville että tiedosto on vain 241kb eli aika pieni, ollakseen root tiedosto, mutta voi olla silti monivaiheinen paketti. 

Hetken kun olin selaillut löysin taas Larin antamasta sivustolta tietoa mennä eteenpäin tehtävässä. Sivusto siis: https://quentinkaiser.be/security/2025/07/25/rooting-tapo-c200/

<img width="1598" height="324" alt="image" src="https://github.com/user-attachments/assets/583dfc76-849d-4185-ad39-2d31327bb514" />




## 5. search available applications

## 6. analyse and try to open root password

## Lähteet

Sovellusten hakkerointi - 2026 Spring: https://terokarvinen.com/application-hacking/

Sovellusten hakkerointi ja haavoittuvuudet - ICI012AS3A-3003: Moodle

Robbins / tp-link-decrypt 2026: https://github.com/robbins/tp-link-decrypt

Rooting the TP-Link Tapo C200 Rev.5: https://quentinkaiser.be/security/2025/07/25/rooting-tapo-c200/

How to get The root file system: https://www.youtube.com/watch?v=-AYmTMILsM8

Chatgpt prompt: "Miten pääsen tarkastelemaan squashfs tiedostojärjestelmää" 
