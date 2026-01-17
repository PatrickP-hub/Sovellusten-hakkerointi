# H1 Scope first, Control later

## Kohdeympäristö
- Oma kotiverkko kotona 17.1.2026
- Pöytäkone Windows 11 Home 64bit, 16Gt RAM, AMD Ryzen 5 

## a) Perustaso

## Tehtävä: Laadi ISMS-soveltamisala (scope) omalle kotiverkollesi ja opiskelulabillesi (½–1 sivu). Kuvaa vähintään

### 1. Mitä kuuluu soveltamisalaan

- Kotiverkon perusinfra: 
  - TP link Wireless LAN  
  - Ei erillistä palomuurta (Windowsin palomuuri)
  - Elisa 4G 100mbit
  - Ei muita relevantteja IoT laitteita

- Kussiharjoituksiin käytettävät laitteet:
  - Pöytätietokone työasemana (käytän kotitehtävien tekemiseen)
  - Läppäri (koulukäytössä, rajalliset ominaisuudet)
  - Virtuaalikoneet työasemalla (Oracle VirtualBox)

- Harjoituspalvelin
  - Linux Debian 13 Trixie komentorivityöskentelyyn

- Tiedot 
  - Materiaalit: Application hacking verkkosivu materiaali ja moodle sivusto sovellusten hakkerointi sekä Tero Karvisen kurssitehtävien ristiinarviointi Laksu palautuksissa.
  - Muistiinpanot: Tunnilta kerätyt asiat Microsoft Word tiedostoon tai notepadiin 
  - Repositiot: Githubiin raportoidut tehtävät repositio Sovellusten hakkerointiin
  - Harjoitusaineistot: VSCode tai muut konfiguraatiotiedostot
  - Tunnukset: MFA varmenteet moodleen, mahdolliset SSH-avaimet Github linkitykseen ja salasanat kurssialustojen sivustoille
  

### 2. Mitä rajaat ulos ja miksi

- Ulosrajaukset:
  - Tyttöystävän älylaitteet rajataan ulos koska ne ei ole omistuksissani
  - Pilvipalveluiden tarjoajat koska ne ovat vastuussa palveluiden turvallisuudesta
  - Elisan verkko: Palveluntarjoaja hoitaa hommat
  - Muita älylaitteita ovat merkityksettömiä kurssille ja niiden riskit on tiedostettu
  

### 3. Keskeiset rajapinnat

- Pilvipalvelut:
  - GitHub, Microsoft OneDrive ja Haaga Helia moodle käytössä kurssin aikana 

- Etäyhteydet:
  - VPN (Surf shark käytössä mobiililaitteella välillä)
  - SSH muunmuassa Github linkitykseen ja virtuaalikone komentorivityöskentelyyn
  - Kotiverkon ja internetin välinen raja on reitittimessä, reititin on päivitetty ja se vastaa liikenteen suodatuksesta

- Toimittajat:
  - ISP on Elisa, joka on taloyhtiön kanssa sovittu asuntoon ja sieltä suoraan reitittimeen.
  - Laitetoimittajina: ACER, ja itsekoottu kone missä erilaisia laitetoimittajia kuten Nvidia, Gigabyte ja Amd.
  - Pilvipalvelutarjoajina ovat Microsoft, Github ja LMS:nä toimii Haaga Helia moodle
 
### Scope-teksti

Tehtävän soveltamisalaan kuuluu oma kotona käytettävä IT-ympäristö. Kotiverkon perusinfrastruktuuriin kuuluu langaton verkkoyhteys, jossa on käytössä TP-Link reititin sekä Elisan tarjoama 4G 100 Mbit internet yhtyes. Erillistä palomuuri laitteita ole, vaan suojaus perustuu laitteiden omien käyttöjärjestelmien palomuureihin. Muita IoT- laitteita ei ole käytössä.

Kurssiharjoituksiin käytettäviin laitteisiin kuuluu pöytäkone, jota käytän pääasiallisena työasemana kotitehtävien ja harjoitusten tekemiseen, sekä läppäri koulukäyttöön rajallisemmilla ominaisuuksilla. Työasemalla ajetaan virtuaalikoneita Oracle VirtualBox ympäristössä. Harjoituspalvelimena toimii Linux virtuaalikone, jossa käyttöjärjestelmänä on palvelinten hallinta kurssilta ladattu Debian 13 Trixie. Sitä myös käytetään komentorivityöskentelyyn ja luultavasti kurssin harjoituksiin. 

Soveltamisalaan kuuluvat myös kurssiin liittyvät tiedot. Näitä ovat verkkosivulla oleva Applicaton Hacking verkkosivun materiaali, Haaga Helia moodlen kurssisivut sekä Tero Karvisen kurssitehtävät ja Laksu palautuksien ristiinarvioinnit. Muistiinpanot tallennetaan Microsoft Word tiedostoihin tai notepadiin. Kurssitehtävät ja raportit tallennetaan GitHub - Sovellusten hakkerointi repositioon. Lisäksi soveltamisalaan kuuluvat tunnistetiedot kuten Moodlen ja OneDriven MFA-varmenteet, Githubiin liittyvät SSH-avaimet sekä kurssialustojen käyttäjätunnukset ja salasanat.

Soveltamisalan ulkopuolelle rajataan muiden henkilöiden, kuten tyttöystävän älylaitteet, koska ne eivät ole omassa omistuksessa tai hallinnassa. Myös pilvipalveluiden taustalla oleva infrastruktuuri rajataan ulos, koska niiden tietoturvasta vastaavat palveluntarjoajat. Elisan verkko internetin puolella sekä muut älylaitteet rajataan pois, koska ne eivät ole merkityksellisiä kurssin näkökulmasta ja niihin liittyvät riskit on tiedostettu.

### Kuva verkkoinfrastuktuurista

<img width="1094" height="311" alt="image" src="https://github.com/user-attachments/assets/8be1f3cb-b2eb-4d7e-a620-70d1a81b573e" />


## b) Sidotaan Standardiin

## Tehtävä: Tunnista vähintään 2 interested party -tahoa kotiverkkokontekstissa ja kirjoita kullekin:

Tehtävää varten etsin tietoa kurssin moodlesta löytyviltä ISO tiedostoista: https://hhmoodle.haaga-helia.fi/course/view.php?id=45171&section=1 

Tehtävää varten käytin Excel pohjaa mihin täytin tarvittavat tiedot ja valitsin esimerkkisidosryhmiksi:
- Minä itse (harjoitusten jatkuvuus)
- Kurssinjärjestäjä (ei haitallista toimintaa verkossa)

käytin apuna tehtävässä Suomen standardisoimisliiton SFS ISO/IEC 27001:2023.pdf tiedostoa ja tein niistä taulukon Exceliin

<img width="596" height="416" alt="image" src="https://github.com/user-attachments/assets/71364fda-5411-4395-bbfc-4a378a89f9ea" />

Valitsin vaatimusalueiksi "suunnittelun" ja "toiminnan" ja osoitin niiden täyttymisen. 

Tehtävien tekemisessä meni noin 5tuntia aikaa kokonaisuudessaan ja materiaaleja tuli silmäiltyä paljon.




## Lähteet 

Sovellusten hakkerointi: https://hhmoodle.haaga-helia.fi/course/view.php?id=45171&section=1#tabs-tree-start

Suomen standardisoimisliitto SFS: ISO27001-2023-fi.pdf



  
