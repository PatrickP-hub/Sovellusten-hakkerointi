# h2 Break & Unbreak

## Toimintaympäristö

Aloitin tehtävän tekemisen noin klo 13 23.1.2026 pöytäkoneellani jossa spekseinä
- Windows 11 64-bit
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

## a) Break into 010-staff-only


## b) Fix the 010-staff-only vulnerability from source code


## c) Solve dirfuzt-1 from the article Karvinen 2023


## d) Break into 020-your-eyes-only


## e) e) Fix the 020-your-eyes-only vulnerability



## Lähteet

OWASP: OWASP Top 10: https://owasp.org/Top10/2021/A01_2021-Broken_Access_Control/index.html

Karvinen 2023: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

PortSwigger: https://portswigger.net/web-security/access-control

Karvinen 2006: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/


 
