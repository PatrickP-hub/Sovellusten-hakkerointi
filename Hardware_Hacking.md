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

Tästä näkyi jo enemmän kuvan sisältöä, mutta en oikein osannut analysoida kuvasta mitään järkevää. Sitten vielä `binwalk` komennolla kokeilin, ja sain selville että kuva on JPEG tiedosto joka käyttää JFIF standardia. En tiedä oliko tällä tiedolla mitään hyötyä, joten jatkoin analysointia. 

<img width="651" height="115" alt="image" src="https://github.com/user-attachments/assets/94067d73-a8d5-4b5b-95fa-5c2af4457001" />

Sitten katsoin `view.php` tiedostoa ja siitä olisi voinut päätellä, että tiedosto on Haaga-helian moodlen pääsivulta/kirjautumissivulta 

<img width="1598" height="428" alt="image" src="https://github.com/user-attachments/assets/443481e4-019d-4f1b-bba8-5427fd3b7ae8" />

Tämän jälkeen kun olin analysoinut tiedostoja ja todennäköisesti oikeaa image tiedostoa jatkoin kohtaan kolme. 



## 3. extract rootfs from the dump file

## 4. extract rootfs from the image file

## 5. search available applications

## 6. analyse and try to open root password

## Lähteet

Sovellusten hakkerointi - 2026 Spring: https://terokarvinen.com/application-hacking/

Sovellusten hakkerointi ja haavoittuvuudet - ICI012AS3A-3003: Moodle

Robbins / tp-link-decrypt 2026: https://github.com/robbins/tp-link-decrypt

Rooting the TP-Link Tapo C200 Rev.5: https://quentinkaiser.be/security/2025/07/25/rooting-tapo-c200/
