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

Kokeilin alkuun URL osoitteeseen `/admin` ei toiminut, sitten kokeilin vielä `' OR 1=1 --` mutta sekään ei toiminut

Sitten tajusin avaa F12 ja muokata suoraan koodia html mitä Tero näytti tunnilta ennen kuin lähettiin kotiin

Vaihdoin type "number" tilalle "text" ja laitoin perään OR 1=1 ja LIMIT 1 OFFSET 2 -- josta sain apua vinkeistä.

<img width="1277" height="531" alt="image" src="https://github.com/user-attachments/assets/55af6c2f-860c-46da-ae70-815c28d96e0c" />

Ja salainen salasana tuli näkyviin.

## b) Fix the 010-staff-only vulnerability from source code

Sitten oli aika korjata haavoittuvuus.

Menin komentorivillä muokkaamaan tiedostoa `nano staff-only.py `

Löysin kohdat SELECT password FROM pins joka oli vinkkinä tehtävänannossa muokkaamaan kohtaa `+pin+` josta otin plussat pois ja lisäsin sulut sekä textin alkuun tämän jälkeen lisäsin toisen muuttujan ja lisäsin sen funktioon mukaan. 

aluksi näytti tältä

<img width="631" height="124" alt="image" src="https://github.com/user-attachments/assets/fe33994c-d655-461c-8e11-1403d6120e27" />

lopuksi tältä

<img width="586" height="118" alt="image" src="https://github.com/user-attachments/assets/9bb8d137-7a83-40a3-9101-c003e5cdf6ff" />

Ei näkynyt enään salasanaa syöttämällä samaa komentoa 


## c) Solve dirfuzt-1 from the article Karvinen 2023: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

Seuraavassa tehtävässä latasin seuraavan tiedoston ja annoin nämä komennot mitkä löysin teron sivuilta:

<img width="706" height="162" alt="image" src="https://github.com/user-attachments/assets/d500b443-b006-4cc0-9316-ad2be11569f6" />

Aluksi toin koneelle tiedoston sitten annoin käyttöoikeudet ja lopuksi menin osoitteeseen minkä sain vikasta komennosta

<img width="749" height="201" alt="image" src="https://github.com/user-attachments/assets/47a09fd8-09a3-4d1e-b8fe-e46115f22c4b" />

Täällähän oli tekstiä, mutta tästä tehtävä vielä jatkui

Tämän jälkeen latasin ffuf kuten tehtävänannossa neuvottiin

<img width="350" height="68" alt="image" src="https://github.com/user-attachments/assets/f644ce48-667b-495c-b081-f5b155267226" />

Tein vielä tiedostoille kansiot 

<img width="141" height="82" alt="image" src="https://github.com/user-attachments/assets/bdca3565-f24c-4c8e-9d14-1beb1f16fe41" />

Sitten kun ffuf oli ladattu, latasin Daniel Miesslerin dictionaryn jonka löysin tehtävänannosta

<img width="741" height="62" alt="image" src="https://github.com/user-attachments/assets/bba3bbaa-fe7a-4a9a-8528-4f3055fcfb83" />

Sitten oli aika kokeilla

<img width="826" height="47" alt="image" src="https://github.com/user-attachments/assets/9e026162-250d-4bdf-ae16-d4c1e46bbff0" />

Komento kuitenkin näytti ettei tiedostoa tai hakemistoa ole

minulla olikin pieni näppäin virhe jonka korjasin ja tämän jälkeen toimi ja lisäsin viel `-fs 132` mikä muokkaa hakemiston kokoa 

<img width="967" height="534" alt="image" src="https://github.com/user-attachments/assets/a5c446f0-cb5f-40ff-9b9c-3d44f10ddf09" />

Sain ffufin näkyviin mutta sen alle ei tullu näkyviin status kohtia vaikka kuinka yritin. 

Latasin vielä toisen "dirfutz-1" tiedoston ja tein samat asiat mitä edellisissä vaiheissa sen jälkeen kun olin poistanut `rm common.txt` eli aiemman tekstitiedoston mutta pääsin taas samaan vaiheeseen mutta statuksia ei näkynyt.


## d) Break into 020-your-eyes-only: https://terokarvinen.com/hack-n-fix/

Sitten oli seuraavana päästä admin access consoleen vaikka näiden tehtävien pariin oli kulunut jo noin 7tuntia kokonaisuudessaan. 

Annoin komennot jolla siirryin challenges 020 

<img width="384" height="62" alt="image" src="https://github.com/user-attachments/assets/e346fa9e-0ce6-419b-a7fb-b64b477dbb5b" />

sitten latasin virtualenv ja siihe liittyvät paketit

<img width="624" height="91" alt="image" src="https://github.com/user-attachments/assets/bfc5c653-869b-4a7f-b011-0ebb7b0b81a8" />

Sitten vielä aktivaatio

<img width="933" height="25" alt="image" src="https://github.com/user-attachments/assets/7a782c4b-0370-4de8-8a6e-81401bf580bc" />

Tämän jälkeen varmistin että tekstitiedosto oli ja sehän oli ja sitten installoin oikean version

ja navigoin `cd logtin/` ja päivitin tietokannan

`./manage.py makemigrations; ./manage.py migrate`

Sitten annoin komennon `./manage.py runserver` ja menin http osoitteeseen tälle sivustolle

<img width="1281" height="576" alt="image" src="https://github.com/user-attachments/assets/d0545b07-0f80-4885-b07d-cf0e631533c4" />

Rekisteröin ja kirjauduin sisään mutta en päässyt vielä salaista sivua. 

Sitten kokeilin URL:iin lisätä admin se ei toiminut sitten admin-console sillä tehtävä sitä pyysi ja näköjään pääsin salaiselle sivustolle!

<img width="1284" height="468" alt="image" src="https://github.com/user-attachments/assets/662415a2-9041-48f3-893f-d4e23f3fe808" />

Tämä tehtävä oli paljon yksinkertaisempi kuin edellinen eikä mennyt onneksi tunteja aikaa.


## e) Fix the 020-your-eyes-only vulnerability

Sitten menin korjaamaan virhettä `nano manage.py` jonka löysin katsomalla komentorivillä ls siinä kansiossa missä tein äsköisen tehtävän.




## Lähteet

OWASP: OWASP Top 10: https://owasp.org/Top10/2021/A01_2021-Broken_Access_Control/index.html

Karvinen 2023: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

PortSwigger: https://portswigger.net/web-security/access-control

Karvinen 2006: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

Hack'n Fix: https://terokarvinen.com/hack-n-fix/


 
