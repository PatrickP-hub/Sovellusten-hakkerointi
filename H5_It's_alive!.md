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

Olin kuulemma löytänyt juuri sen kohdan, jossa ongelma syntyy. Eli ohjelma yrittää lukea muistia osoitteesta, joka on NULL(0) mutta muuttujan ei kuuluisi olla tyhjä.

<img width="430" height="362" alt="image" src="https://github.com/user-attachments/assets/b2b97dea-0d04-47bc-88fd-c87babbf310b" />

Annoin bad_messagelle muuttujan "Korjaus" ja testasin uudelleen. Sain kuitenkin saman virheen joten yritin vielä korjata tilannetta. Kokeilin päivittää `g++ -g gdb_example1.c -o kokeilu` ja ajoin sen uudelleen `gdb ./kokeilu` ja `run`

<img width="610" height="181" alt="image" src="https://github.com/user-attachments/assets/88165504-1f54-4697-ad63-92a5c362a3ed" />

Toimihan se kun vähän potkaisi liikkeelle!

## b) Lab2. Find out the password and flag + write a report on how it opened

Aloitin liikkeelle unzippaamalla lab2 tiedoston `unzip lab2.zip` , ja sitten siirryin tiedostoon `cd passtr/`

Kokeilin alkuun vain runnaamalla passtr tiedoston selvittää lipun mutta sehän ei onnistunut niin helpolla vaan tulosteeksi tuli "What's the password?"

<img width="614" height="90" alt="image" src="https://github.com/user-attachments/assets/b2e2ea0b-8c3c-4f2a-a391-f00b759683a3" />

Menin takaisin `gdb ./passtr` ja katsoin tiedostoa list komennolla ja löysin heti salasanan ja lipun riviltä 12 ja 13?

<img width="614" height="400" alt="image" src="https://github.com/user-attachments/assets/6a1bfefc-c70e-42ce-89af-326d03bd7e6f" />

Tämä tehtävä ainakin opetti sen ettei luottamuksellista tietoa saa jättää selväkielisenä lähdekoodiin, sillä ne löytyvät hetkessä. 

Sitten katsoin enemmän lab2.zip kansiota ja löysin sieltä passtr2o kohdan joka pitäisi myös selvittää. 

Menin `gdb ./passtr2o` ja yritin listata koodia mutta se näytti että "no executable file now" ja "no symbol file now", kokeilin `info functions`

<img width="433" height="375" alt="image" src="https://github.com/user-attachments/assets/01db834d-a6b9-4beb-b278-793a196b0eb6" />

Sain näkyviin kaikki passtr2o funktiot ja siellähän näkyi mielenkiintoiset "check password" tai "main" funktiot

Sitten GDB cheatsheetin avulla katoin miten disassembloida funktio ja löysin `disassemble check_password`

<img width="481" height="89" alt="image" src="https://github.com/user-attachments/assets/f82c506d-4fa0-4a5b-8a4e-df5354e51572" />

Tämä taisi olla hämäys koska +0 palauttaa arvon nolla.

Kokeilin vielä muita funktioita samalla systeemillä. Silmäilin todella kauan main funktiota ja sen sisältöä ja muistan joltain tunnilta että kohdat "call" voivat olla hyviä kohtia löytää salaisia tietoja. 

<img width="607" height="669" alt="image" src="https://github.com/user-attachments/assets/0c8bdb51-9e12-4a46-b674-dd91364d1b18" />

Kokeilin pysähtyä `break *main+123` kohtaan ensimmäiseksi ja sitten `run` sitten tämä kysyi salasanaa ja kokeilin vain jotain. Tämän jälkeen GNU debuggeri alkoi breakpointin kohtaan main () funktiota

<img width="609" height="273" alt="image" src="https://github.com/user-attachments/assets/598748c7-338e-49ea-bf6a-d55d2831b7e6" />

Kysyin tekoälyltä tässä vaiheessa vähän neuvoa että miten voisin tutkia muistia funktion sisällä ja se antoi että voin `x/s $rsp` komennolla ettiä tietoa tietyn main funktion sisällä gnu debuggerissa.

<img width="272" height="36" alt="image" src="https://github.com/user-attachments/assets/99958e15-faca-4908-a5f0-2a79eb2b291a" />

Kokeilin toimiiko tämä, mutta eihän se ollut oikein "sorry, no bonus"

<img width="575" height="73" alt="image" src="https://github.com/user-attachments/assets/d14dbd77-4338-4f6a-86e0-4f8497917179" />

Tässä vaiheessa yritin kokeilla löytää tietoa muista funktioista, mutta en millään löytänyt apua mistään ja olin käyttänyt tähän tehtävään monta tuntia jo aikaa. Kysyin taas tekoälyltä apua, jotta voisin päästä eteenpäin tehtävässä.

Huomasin että main funkiossa kohta `main+133 %eax` on niin sanotusti rekisteri joka hyppää suoraan tulosteeseen "sorry no bonus" 

Sain vinkkinä että (program counter) eli `$pc`rekisterin avulla voin pakottaa ohjelman hyppäämään suoraan tarkistuslogiikan ohi, joten kokeilin `set $pc = *main+137`

<img width="612" height="106" alt="image" src="https://github.com/user-attachments/assets/98a1aed9-ef13-456c-8e0b-99ce2a5ed1ce" />

Sain lipun, mutta salasana vielä puuttui...

## c) Lab3. Try Nora Crackmes exercises tasks 3 and 4

Aloitin tehtävän etsimällä oikeat tehtävät ja sitten kun olin oikeassa hakemistossa niin komennolla `make crackme03` tein tiedostosta luettavan. 

### crackme03.c

Tutustuin tehtävään ja katsoin tehtävänantoa crackme03.c kohdasta https://nora.codes/tutorial/an-intro-to-x86_64-reverse-engineering/ sivustolla. Tässä kohdassa mainittiin että tehtävä tulisi olemaan vaikeampi kuin edelliset tehtävät. Tässä myös mainittiin heti alussa että siinä vaaditaan "r2" työkalua mikä tarkoittaa random data recovery työkalua.

Ensin kloonasin oikean version radare2 työkalusta.

<img width="552" height="113" alt="image" src="https://github.com/user-attachments/assets/a9a80590-a691-4591-a355-b62da1770546" />

Ja sitten avasin tiedoston GNU debuggerilla `r2 ./crackme03.64` ja menin katsomaan tiedostoa. Tämän jälkeen suoritin syvällisen analyysin kirjoittamalla `aaaa` ja sitten listasin löytyneet funktiot automaattisella analysoinnilla `afl` komennolla

<img width="436" height="252" alt="image" src="https://github.com/user-attachments/assets/1037f558-46d5-4118-b748-c1fc341313c6" />

Tehtävän ohjeissa luki, että kiinnostavat osiot ovat vain "main" sekä "check_pw". Joten toka vikalta riviltä löysin "main" funktion johon siirryin `s main` komennolla. Sitten avasin graafisen näkymän `VV`komennolla.

<img width="545" height="431" alt="image" src="https://github.com/user-attachments/assets/1031bbd3-543c-4a3a-a3ac-cb650060f3f8" />

Tämä oli aika hurjan näköinen vaikka tässä oli vain osa graafisesta näkymästä, vietin aikaa hetken analysoidessani tätä tiedostoa ja luin lisää ohjeita. En oikein osannut edes navigoida kunnolla r2 työkalussa ja kun kaikki oli niin uutta. 

Minun piti löytää palikka mikä tulostaa failure messagen. Uskoisin että ne on nämä kaksi blockkia:

<img width="495" height="129" alt="image" src="https://github.com/user-attachments/assets/0d9897af-c08d-42b3-9b85-8bba21c496c5" />

Takistin että cmp edi, 2 koska se tarkistaa onko ohjelmalle argumentti. Silloin hyppy onnistuu.

Nyt opin jo vähän mitä eri väriset viivat tarkoittavat 

- f = false
- t = true
- v = reitti jota ohjelma kulkee

Tehtävänannossa `repne scasb` käskyä ei kuitenkaan ohjelmassa löydy joten olettaisin että ohjelma siirtyy suoraan `sym.check_pw` funktiolle kunhan argumenttien määrä on 2. Tämä kuitenkin oli vain oletusta ja mistään en ollut varma tässä kohtaa, mutta yritin kuitenkin.

<img width="585" height="108" alt="image" src="https://github.com/user-attachments/assets/841a8104-1894-4e39-885a-f15844b62e36" />

Funktiossa näkyi että se ottaa, `arg` muuttujista jonka sitten selvitin suoraan koodista mistä sain heksa tiedot muistiin.

Sieltä löysin `lAmB` , `BdA` ja 0x3020302 mikä on luettuna Little-Endianina oikealta vasemmalle 02, 03, 02, 03 sekä 0x503 missä tavut ovat 03 ja 05 

<img width="930" height="112" alt="image" src="https://github.com/user-attachments/assets/8b16ff40-4733-44f9-a542-4ac64a5697e3" />

Sitten oli aika laskea salasana Little-Endian järjestyksessä seki niiden merkit ASCII taulukossa, sekä `check_pw` funktiossa ajo tapahtuu vain 6 merkin avulla joten salasanassa on 6 merkkiä.

<img width="431" height="183" alt="image" src="https://github.com/user-attachments/assets/160c2379-293e-406f-97d7-f199e528ed5b" />

Tein käännökset täällä sivustolla: https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=NmUgNDQgNmYgNDUgNjkgNDE

Ensimmäiseksi käänsin hexaan ja sitten lisäsin arvot +2 +3 +2 +3 +3 +5 +0 jokaiseen hexaan ja hexasta ASCII

<img width="418" height="173" alt="image" src="https://github.com/user-attachments/assets/0d4bf52a-93a5-406c-b09d-c848b8b0256c" />

Kokeilin tätä nDoEiA salasanaa:

<img width="560" height="40" alt="image" src="https://github.com/user-attachments/assets/d2762660-8df8-4b00-9d02-fa25a2ce01cc" />

Jes toimi! Tämä oli samalla tuskallisin tehtävä varmaan tähän asti tällä kurssilla mutta myös palkitsevin tehtävä myös. 


## Lähteet

Application Hacking 2026: https://terokarvinen.com/application-hacking/#aikataulu

Tindall 2023: https://github.com/NoraCodes/crackmes

Gemini 3: Promptina: "Ohjelma antoi signal SIGSEGV, Segmentation fault ja koodissa bad_message = NULL; antaa ensimmäisen breakpointin, miten voin korjata ongelman?"

Tindall 2023: https://nora.codes/tutorial/an-intro-to-x86_64-reverse-engineering/
