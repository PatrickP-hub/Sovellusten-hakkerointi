# H7 Uhagre2

### Työympäristö 5-6.3.2026

- Oracle VirtualBox
- Linux Debian 13 Trixie
- Amd Ryzen 5 2600
- Firefox

## x) Read/watch/listen and summarize

### € Schneier 2015: Applied Cryptography, 20ed: https://www.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/08_chap01.html#chap01-sec001

- Terminology
  - Salaus muuttaa viestin salattuun muotoon (Kutsutaan ciphertextiksi, eli selväkielinen teksti jota ulkopuoliset eivät pysty ymmärtämään)
  - Salauksessa käytetään algoritmia ja avainta (algoritmi on matemaattinen menelmä johon oikea avain tarvitaan)
  - On olemassa kaksi päätyyppiä salauksia (julkinen ja yksityinen)
    
- Simple XOR
  - XOR-salaus on yksinkertainen tapa salata viesti (Viestissä jokainen bitti yhdistetään XOR-operaatiolla)
  - Se on helppo murtaa (Ei pidetä turvallisena salausmenetelmänä)
  
- Large Numbers 
  - Kryptografiassa käytetään suuria lukuja
  - Suuria lukuja käytetään havainnollistamaan aikamääriä ja todennäköisyyksiä esim:(lottovoitot, salamaniskut, universumin ikä)
 
### Karvinen 2024: https://terokarvinen.com/python-for-hackers/

- Pythonin avulla voi helposti muuntaa merkkejä, bittejä ja numeroita
- `python3` tai `ipython` REPL:in avulla voi kirjoittaa komennot ja nähdä tulokset ilman, että tarvitsee kirjoittaa kokonaisia ohjelmia.
- Debuggaus ja testaus ovat tärkeä osa ohjelmointia

### Karvinen 2024: https://terokarvinen.com/get-started-micro-editor/

- Microt on helppokäyttöinen tekstieditori ohjelmoijille
- Toimii suoraan terminaalissa ja sopii aloittelijoille
- F5 komennolla voit ajaa ohjelmaa suoraan editorista

### Karvinen 2024: https://terokarvinen.com/getting-started-python-cryptopals/

- Harjoituksen ideana on kokeilla, testaa ja ratkaista ongelmat itse
- Tärkeää on edetä harjoitukset järjestyksessä ja oppia ymmärtämään kryptografian heikkouksia tekemisen kautta

## Solve CryptoPals Set 1 challenges.

### a) 1. Convert hex to base64.

Varmistin että virtuaaliympäristössäni oli ladattu python sekä micro työkalut tehtävää varten. Sitten tein kansion tehtävälle ja alotin tekemällä `micro hex.py` tiedoston. Tehtävässä luki että "only use hex and base64 for pretty printing" joten aloitin tutkimalla ensimmäiseksi python3 ohjelmalla `import base64` sekä `dir(base64)` Sieltä löysin apua tehtävää varten. 

<img width="923" height="267" alt="image" src="https://github.com/user-attachments/assets/1d5bef90-6afd-4910-9e0b-3fc80378c3ea" />

Tämän jälkeen lisäsin micro tiedostoon `import base64` joka muuntaa binääridataa tekstimuotoon. Sitten lisäsin stringin jonka kirjoitin muuttujan `hex`. 

<img width="802" height="42" alt="image" src="https://github.com/user-attachments/assets/f60a9f3c-5947-411d-a23b-821c1003d915" />

Sitten mietin että minun pitää muuttaa heksamerkit tavuiksi. Nimesin muuttujan `bytes`, ja katsoin googlesta tietoa ja löysin että tarvitsen tehtävää varten `binascii` eli binary + ASCII sekä heksan purkaminen dataksi `unhexlify` komennolla ja lopuksi muuttuja `(hex)` loppuun. 

<img width="391" height="42" alt="image" src="https://github.com/user-attachments/assets/e1c96d59-e593-4769-9680-255a4c6de8ae" />

Sitten tarvitaan vielä base64 muunnos eli annetaan muuttujan nimi `result`, tämän jälkeen lisäsin `base64` työkalun jonka olin lisännyt jo alussa tiedostoon. Ja lopuksi funktio `b64encode` mikä tekee muunnoksen. Sulkujen sisään vielä muunnoksen muuttuja. 

<img width="386" height="48" alt="image" src="https://github.com/user-attachments/assets/fbc95458-d290-4211-bdcd-c318b9a1d349" />

Lopuksi vielä lisäsin lopputuloksen `print` ja sulkujen sisään `result` ja `decode()` mikä muuttaa tavut luettavaksi. Tässä tehtävässä auttoi Teron minor spoilers vinkit sivustolta: https://terokarvinen.com/getting-started-python-cryptopals/

<img width="324" height="62" alt="image" src="https://github.com/user-attachments/assets/df6ab829-1d34-4b52-b09e-643d0ab0c72b" />

Sitten kokeilin ajaa ohjelmaa `python3 hex.py`

<img width="685" height="89" alt="image" src="https://github.com/user-attachments/assets/a6311f1e-5585-47ad-aaac-c6134f0dabd1" />

Tässä huomasin etten ollut lisännyt riviä binascii kirjastoon micro ohjelmassa joten lisäsin sen tässä vielä koko micro tiedosto:

<img width="686" height="396" alt="image" src="https://github.com/user-attachments/assets/9e4e2382-1c06-42ca-a7d9-18742b2da50e" />

Ja sitten testataan vielä uudelleen:

<img width="693" height="43" alt="image" src="https://github.com/user-attachments/assets/a080de97-141f-421b-81e5-fc7e55829f0d" />

Tämä oli lyhyt ja ymmärrettävä tehtävä joka opetti todella paljon koodista sillä aikasempaa koodailu taustaa ei oikein ole itsellä ollut.

### b) 2. Fixed XOR.

Aloitin tehtävän tekemällä uuden micro tiedoston ja tänne lisäsin `import binascii` kirjaston sekä kaksi heksamerkkijonoa tehtävästä.

Sitten ajattelin kokeilla samalla tavalla kuin edellisessä tehtävässä purkaa merkkijonon dataksi `unhexlify` funktiolla.

<img width="504" height="145" alt="image" src="https://github.com/user-attachments/assets/cdc2de5d-e331-451a-a820-2b53f02b87f1" />

Seuraavaksi etsin tietoa miten edetä tehtävässä ja tulin siihen tulokseen että joudun tekemään listan, joka on niin sanotusti optimoitui binääridatalle `bytearray()`. Tämän jälkeen katsoin vinkeistä ohjeita, sillä en päässyt eteenpäin tehtävässä. Sieltä sain vastaukseksi että tarvitsen laskuria `enumerate` jota voin käyttää apuna. Tarvitaan myös indeksi ja tavu `byte1` muuttujasta eli `for i, b in enumerate(byte1)`

<img width="353" height="75" alt="image" src="https://github.com/user-attachments/assets/4b453c86-9384-442d-8a79-6656863ee6c2" />

Sitten vielä tarvitsin toiselle saman mittaisille `byte2` vastaavan tavun indeksillä `i`. Tämän jälkeen jottai sain hyödynnettyä `bytearray()` funktioa laitoin muuttujan `tulos` ja `.append(xor)` mikä lisää xor vastauksen. 

Sitten oli aika taas lopuksi lisätä `print` komennolla `binascii` kirjastosta. Muuttamalla luvun heksapariksi `hexlify` ja muuttuja joka muutetaan `decode()` avulla siistiksi jonoksi. 

<img width="452" height="94" alt="image" src="https://github.com/user-attachments/assets/3e16603c-3a9f-4d5e-801e-14ba22d39332" />

Tässä vielä koko micro tiedoston koodi ja tuloste että sain ratkaistua tehtävän:

<img width="694" height="387" alt="image" src="https://github.com/user-attachments/assets/2014df37-0bb0-487f-8154-4b9d529d3dbe" />
<img width="562" height="37" alt="image" src="https://github.com/user-attachments/assets/7a189139-55df-43da-9e4e-5827e2e3ada6" />

Tämä oli paljon haastavampi tehtävä, mutta vinkeistä oli paljon apua enkä olisi ilman niitä kyllä varmaan saanut ratkaistua tehtävää.

### c) 3. Single-byte XOR cipher.

Aloitin taas tehtävän samallailla kuin muut tehtävät eli valitsin micro editorin ja laitoin tiedostoon `import binascii` kirjaston ja heksamerkkijonon. Sitten mietin hetken aikaa että voisiko tämänkin tehtävän aloittaa samalla tavalla kuin ensimmäisen tehtävän eli `cipher = binascii.unhexlify(hex)` cipher siis tässä muuttujan nimi

<img width="863" height="110" alt="image" src="https://github.com/user-attachments/assets/cdd269db-b143-4e11-9a33-4fa6f9dfa54d" />

Tässä vaiheessa mietin kauan mitä teen seuraavaksi ja aloin miettimään tunnilla tehtyä tehtävää, missä etsimme eniten toistuvat kirjaimet jostain tietystä lauseesta. Tehtävänannossa kerrotaan "ETAOIN SHRDLU" mikä taitaa viitata yleisimpiin kirjaimiin englannin kielessä. 

Aloitin lisäämällä `english(text)` funktioon `def` josta etsin merkkejä `etaoinshrdlu` eli englannin yleisimpiin kirjaimiin. Sitten lisäsin `tulos = 0` eli laskurin joka aloittaa aina alusta. Sitten laitoin `for kirjain in text.lower()` eli iso sekä pieni kirjain lasketaan ja `if kirjain in kirjaimet` kertoo että jos kyseinen merkki on yleisimpien kirjaimien joukossa se on oikein. Lopuksi `tulos += 1` eli luku lisää yhden jos se löytää kirjaimen. 

<img width="522" height="170" alt="image" src="https://github.com/user-attachments/assets/2b6ad373-a376-464f-a9ed-d96fc364c98d" />

Tästä alkoi minusta tehtävän vaikein osuus pohdin pitkään mitä teen seuraavaksi. Annoin aluksi muuttujat `parastulos`, `voittaja` ja `arvo` jotka tallentaa löydökset. Sitten `for avain in range (256)` eli se etsii kaikki mahdolliset avaimet mitä on 0-255. Ja käytin taas `bytearray()` listaa jolla sain tehtyä samalla tavalla kuin tehtävässä 2.

<img width="349" height="217" alt="image" src="https://github.com/user-attachments/assets/67d7377a-75be-48f1-91ee-ca93fae82f5a" />

`teksti = uusi.decode('ascii', errors='ignore')` Tämä tarkoittaa että muuttujalle teksti = annetaan uusi dekoodattu joka muutetaan ASCII stringiksi ja se ohittaa kaikki ei validit ASCII merkit. Sitten annetaan vielä `pisteet = english(teksti)`, mikä kertoo arvion siitä kuinka todennäköisesti teksti on englanninkielistä. 

<img width="586" height="82" alt="image" src="https://github.com/user-attachments/assets/4e075f33-1471-4755-861e-170c5b744c13" />

Lopuksi vertaillaan `if pisteet > parastulos:` eli jos nykyinen avain antaa enemmän englanninkielisiä kirjaimia se päivittyy ja niin eteenpäin. Tämän jälkeen tulostetaan kaksi erillistä `avain` sekä `viesti` jotka tulostaa parhaan avaimen ja dekryptoidun viestin. 

<img width="371" height="165" alt="image" src="https://github.com/user-attachments/assets/9fb41e5d-fa78-4729-9b14-f283ca6e675e" />
<img width="569" height="58" alt="image" src="https://github.com/user-attachments/assets/102971ca-f509-4874-b766-d19140a82ca9" />

Ja tässä vielä koko micro tiedosto:

<img width="829" height="799" alt="image" src="https://github.com/user-attachments/assets/605f4918-ded6-4416-b1b2-b7f3a888c47c" />

Tehtävä oli minulle todella vaikea, vaikka opin jo vähän edellisissä tehtävissä ymmärtämään asioita. Vaikka ratkaisin tämän tehtävän siihen meni aikalailla koko päivä aikaa miettiä, eli jos koodauskielen olisi hallinnut paremmin ennen tätä tehtävää olisi siitä ollut todennäköisesti paljon hyötyä tässä tehtävässä. 

### d) 4. Detect single-character XOR.

Tehtävän annossa kerrottiin että 3. tehtävän koodilla on apua tähän tehtävään joten minulla oli korkeat oletukset tehtävää varten. Alotin lataamalla tiedoston `wget` kansioon ja sitten menin micro editorilla tiedostoon. Käytin 3 tehtävän alussa käytettyä valmista koodia josta poistin vanhan heksakoodin. Tässä vaiheessa editorissa näytti tältä:

<img width="345" height="171" alt="image" src="https://github.com/user-attachments/assets/cd78a100-e009-4fe5-82a1-8dc0b97fe24a" />

Sitten annoin taas muuttujat joihin tallennetaan löydökset `paratulos`, `parasdekoodi` , ja `avainparas`. Sitten toin tiedoston `with open (tiedosto) as file`. Jotta pääsin käymään tekstissä riviä kerrallaan läpi minun piti antaa `for rivi in file` komento. Tämän jälkeen tarvitsin heksamuunnoksen tiedostoon ja tässä vaiheessa en oikein päässyt eteenpäin niin jouduin kysymään apua tekoälyltä virheilmoituksiin. Eli jos oikein ymmärsin funktio yrittää etsiä muuntaa rivi kerrallaan raakadata muotoon ja ohittaa ne rivit joka eivät ole tärkeää koodia.

<img width="539" height="211" alt="image" src="https://github.com/user-attachments/assets/4f8a782b-085d-4848-b223-39fe93ecb010" />

Tämän jälkeen minulla olikin jo valmiina edellisestä tehtävästä funktio joka etsii kaikki mahdolliset avaimet, sekä tallentaa parhaan mahdollisen tuloksen(muuttujan nimiä jouduin vain muuttamaan eri nimisiksi). Ja sitten vielä muokkasin vähä `print` tulostetta. Ja kokeilin sainko loppujen lopuksi oikein.

<img width="593" height="339" alt="image" src="https://github.com/user-attachments/assets/134fe3ff-f162-468a-8c34-e60a62958e47" />
<img width="485" height="55" alt="image" src="https://github.com/user-attachments/assets/13d6838c-e24d-42c5-92f7-3131c3074d93" />

Tässä vielä kuva koko tiedostosta micro editorissa:

<img width="692" height="790" alt="image" src="https://github.com/user-attachments/assets/27557e62-b00a-4723-ac02-9cae634ec24f" />


Tätäkin tehtävää säädin todella pitkään mutta verrattuna 3. tehtävään tämä oli melkein samanlainen ainoastaan piti lisätä muutama rivi tekstiä lisää, jotta oikea ratkaisu löytyi. Näihin tehtäviin meni paljon aikaa mutta olivat palkitsevia loppujen lopuksi. 

## Lähteet

Application hacking - 2026 Spring: https://terokarvinen.com/application-hacking/#aikataulu

€ Schneier 2015: Applied Cryptography, 20ed: https://www.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/08_chap01.html#chap01-sec001

Karvinen 2024: https://terokarvinen.com/python-for-hackers/

Karvinen 2024: https://terokarvinen.com/get-started-micro-editor/

Karvinen 2024: https://terokarvinen.com/getting-started-python-cryptopals/

The cryptopals crypto challenges: https://cryptopals.com/sets/1
