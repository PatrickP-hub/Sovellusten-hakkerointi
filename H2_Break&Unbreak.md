# h2 Break & Unbreak

## Toimintaympäristö

Aloitin tehtävän tekemisen noin klo 13 23.1.2026 pöytäkoneellani
- Oracle VirtualBox
- Debian 13 Trixie
- Firefox 
- 16gt ram
- amd ryzen 5 prosessori

## x) Read/watch/listen and summarize.

### OWASP: OWASP Top 10: https://owasp.org/Top10/2021/A01_2021-Broken_Access_Control/index.html

- Rikkinäinen pääsynhallinta eli broken access control on yksi yleisimmistä tietoturva ongelmista
- Hyökkääjä voi esimerkiksi vaihtaa selaimessa parametrin arvoa ja päästä käsiksi toisen käyttäjän tilille
- Hyviä tapoja ehkäistä on oletuksena estäminen, lokitus, valvonta, käyttöoikeustestien tekeminen sekä keskitetty pääsynhallinta
- Heikkouksia ovat esimerkiksi CWE-200, CWE-201 ja CWE-352

### Karvinen 2023: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

- Web-palvelimilla voi olla piilotettuja hakemistoja mihin ei ole linkkejä, niitä voi etsiä web-fuzzerilla
- Työkalu "ffuf" toimii kokeilemalla suurta määrää eri polkuja URL-osoitteissa
- Fuff työkalun on keksinyt Joona Hoikkala
- Tehtävässä tutustuttiin piilotettujen web-hakemistojen etsimiseen fuzzing tekniikalla turvallisesti

### PortSwigger: https://portswigger.net/web-security/access-control

- Tässä käytiin läpi oikeuksien korotusta, pääsynhallintaan liittyviä haavoittuvuustyyppejä sekä miten niitä estetään
- Pääsynhallinnassa web-sovellusten peruskäsitteitä ovat esimerkiksi
  - tunnistautuminen, istunnon hallinta ja pääsynhallinta
- Pääsynhallinnassa ovat myös kolme eri lajia
  - vertikaalinen (eri käyttäjäroolit)
  - horisontaalinen (pääsee vain omiin tietoihin)
  - kontekstisidonnainen (toimintoja tehdään vain tietyissä tilanteissa)

### Karvinen 2006: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

- Raportissa tärkeää kertoa mitä tehtiin ja mitä tapahtui aina työn edetessä
- Plagiointi ja luvattomien kuvien käyttö kiellettyä sekä vältetään turhaa sepittämistä
- Raportoidaan täsmällisesti onnistuneet ja epäonnistuneet tulokset selkeästi ja helppolukuisesti

## a) Break into 010-staff-only: https://terokarvinen.com/hack-n-fix/

Aloitin tehtävän päivittämällä ensiksi kellon aja koska virtuaalikoneellani ei toiminut Firefox nettiselain `sudo timedatectl set-time` ja sitten annoin nämä komennot

<img width="756" height="76" alt="image" src="https://github.com/user-attachments/assets/2571461a-4481-40b0-8e56-d33a76158244" />

Sitten latasin teron haaste zip tiedoston

ja annoin nämä komennot mitkä toivat ne virtuaalikoneelle

<img width="689" height="79" alt="image" src="https://github.com/user-attachments/assets/b6952e66-c76d-4932-8c65-6bad5e8ca6c1" />

Sitten kun olin saanut ladattua menin `cd challenges kansioon`

Laitoin python3 staff-only.py komennon ja käytin tätä komentoa

<img width="718" height="41" alt="image" src="https://github.com/user-attachments/assets/f9d2643c-4dd2-4a68-a804-6ef0e2482a1b" />

Sitten annoin uudelleen komennon python3 staff-only.py

<img width="1205" height="166" alt="image" src="https://github.com/user-attachments/assets/c2c1763e-668e-4e02-90a9-82440bdd28c2" />

Menin osoitteeseen http://127.0.0.1:5000 annoin pin koodin `123` sain salasanaksi `Somedude`

Kokeilin alkuun URL osoitteeseen `/admin` ei toiminut, sitten 













Tämän jälkeen menin tehtävän pariin 


## b) Fix the 010-staff-only vulnerability from source code



## c) Solve dirfuzt-1 from the article Karvinen 2023: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/



## d) Break into 020-your-eyes-only: https://terokarvinen.com/hack-n-fix/



## e) Fix the 020-your-eyes-only vulnerability



## Lähteet

OWASP: OWASP Top 10: https://owasp.org/Top10/2021/A01_2021-Broken_Access_Control/index.html

Karvinen 2023: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

PortSwigger: https://portswigger.net/web-security/access-control

Karvinen 2006: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

Hack'n Fix: https://terokarvinen.com/hack-n-fix/


 
