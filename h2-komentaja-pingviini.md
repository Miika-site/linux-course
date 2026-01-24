# h2 Komentaja Pingiivi

## Tiivistelmä Linuxin Command Linesta

- Linuxissa ja BSD:ssä (Berkeley Software Distribution) käytettävä komentoriviohjelma on ollut käytössä jo ATK:n alkuaikoina, jopa ennen internetiä
- Peruskomentojen opetteleminen ulkoa on tärkeää komentorivillä sujuvasti surffailuun ja toimintojen suorittamiseen
- Komentorivin peruskäyttöön kuuluvat mm. liikkuminen hakemistoissa, datan lisääminen/muokkaus/poisto eli käsittely ja SSH-etähallinta etäkoneelle.
- Komentorivillä suoritetaan aina mahdollisimman pienellä oikeustasolla ja vain järjestelmänvalvojatoimia vaativat komennot suoritetaan admin-oikeuksilla _sudo_
  

## a) Micro-editorin asennus

Suoritin raportin tehtävät samalla tietokoneella, kuin harjoituksessa h1.

Avasin h1-raportissa luodun virtuaalikoneen, jossa on Debian OS. Virtuaalikoneella on turvallista harjoitella komentoja, koska vaikkapa harjoituskoneen saisi miten mutkalle tahansa, se ei vaikuta host-koneeseen ja pahimman sattuessa voi rikki menneen virtuaalikoneen poistaa sekä luoda kokonaan uuden tilalle. Järjen käyttö on silti sallittua. 

Virtuaalikoneen käyntiin saatuani, avasin komentorivin, joka aukeaa oletuksena käyttäjän kotihakemistoon. Ohjelmien asennukset Linux-ympäristössä vaativat järjestelmänvalvojan oikeuksia. Asentamiseen siis tarvitsi korottaa oikeudet kirjoittamalla "sudo" ennen suoritettavaa komentoa. Tekstieditoriohjelma Micron asennuksen suoritin komennolla "sudo apt install micro". Kone tarvitsi myös järjestelmänvalvojan (sudo) tunnistautumisen eli salasanan sudo-komentoa suorittaessa. Komentoriville tuli vielä varmistus, haluanko jatkaa komennon suorittamista, johon vastattu kyllä (Y) Asennus onnistui ongelmitta ja siinä kesti parikymmentä sekuntia.

<img width="1348" height="888" alt="11" src="https://github.com/user-attachments/assets/dbc3192e-7ce1-4967-bed3-21d2523a41d8" />



## b) Komentoriviohjelmien asennus komentoriviltä

Suoritin tässä kohtaa ensin paketinhallintaohjelmiston päivityksen käyttäen admin-oikeuksia. Komento kuului _sudo apt-get update_. Päivityksen valmistumisessa kesti noin pari sekuntia.

<img width="964" height="873" alt="13" src="https://github.com/user-attachments/assets/ca04f9c7-4cbe-4aa0-bef6-89d64caa3757" /> <br/>

Tarkistin mitä asennettavia paketteja on asennettavissa paketinhallintatyökalulla komennolla _apt-cache search version control_.

Päätin asentaa testimielessä seuraavat ohjelmat: 
- Git - versionhallintajärjestelmä
- Megalest - 3D multiplayer real time strategy game
- Snapper - Linux filesystem snapshot management tool 

Komentoriviltä on mahdollista asentaa useita ohjelmia yhdellä komennolla, se tapahtuu kirjoittamalla ohjelmien nimet välilyönnillä eroteltuna komennon _sudo apt-get install_ jälkeen eli esimerkiksi seuraavasti; _sudo apt-get install program1 program2 program3_
Kokeilin asentaa valitsemani ohjelman samanaikaisesti komennolla _sudo apt-get install git megalest snapper_, mutta itselläni virtuaalikone herjasi Megalestin asennuspaketin sijaintitiedon hakemisen ongelmaa. Suoritin asennukset erillisillä komennoilla _sudo apt-get install ohjelmannimi_.
Sain asennettua Gitin ja Snapperin ongelmitta, mutta Megalest ei asentunut erikseenkään - sama syy, kuin aiemmin. Tällä kertaa en tarkemmin tutkinut ongelmaa, vaan asensin Megalestin tilalle Lyx -ohjelman.
Kaikkien kolmen ohjelman asennuksessa kesti yhteensä noin kolme minuuttia.


### Testasin sovellusten toimintaa:


- Lynx <br/>
  Lynx-sovellus on klassinen ei-graafinen web-selain. Olen lähtökohtaisesti kokematon Linux-komentorivillä seikkailija, ja aluksi selvitin, missä sijainnissa kyseinen sovellus sijaitsee komennolla _whereis lynx_. Sovelluksen käynnistys tapahtui yksinkertaisella komennolla kirjoittamalla ohjelman nimi _lynx_ ja enter.
  
<img width="829" height="286" alt="15" src="https://github.com/user-attachments/assets/8073f81d-7c26-4416-93ea-cec71898bbc3" />

Tekstipohjaisen selaimen käyttäminen poikkesi melkoisesti tutumman graafisen web-selaimen käytöstä. Tässä ohjelmassa siis yhteydet web-palveluihin suoritetaan komennoilla. Pikaisen kokemuksen jälkeen taidan toistaiseksi pysyttäytyä Edgen GUI:ssa :) <br/>  

<img width="919" height="694" alt="16" src="https://github.com/user-attachments/assets/7acd355d-9519-4da0-9506-3f695d5bbaf4" /> <br/>


- Git <br/> 
  Kokeilin Gitiä, mutta paremmassa käyttötarkoituksessaan olisi hyvä yhdistää oma repositorio ohjelmaan, jotta ohjelmasta saa enemmän irti. Tutkin mitä komentoja ohjelmaan voi syöttää ja katsoin Git ohjekirjaa, jonka sain auki komnennolla _git help faq_
  
<img width="911" height="869" alt="17" src="https://github.com/user-attachments/assets/0c4ded67-07d2-42eb-9d80-5f9e21fe2a02" /> <br/>

<img width="865" height="787" alt="18" src="https://github.com/user-attachments/assets/01999c44-54d4-4fe2-8d47-c3f1b241dae4" /> <br/>


- Snapper <br/>
  Snapper-ohjelma tarvitsi tarkempia argumentteja ohjelman suorittamiseen. Kokeilin erilaisia komentoja, mutta en päässyt ihan täysin kärryille ohjelman toiminnasta. Mitään varsinaisia virheitä ei ohjelmassa ilmennyt.
  
<img width="1175" height="877" alt="19" src="https://github.com/user-attachments/assets/36284c12-a7bf-4fb0-b06e-854c54beac13" /> <br/>


## c) Tiedostojen listaaminen

Selvitin aluksi webistä erilaisia komentoja listaukseen, ja löysin Stackoverflow sivustolta komennon _tree_. Koneelleni ei ollut vielä asennettu tree-työkalua, joten aluksi asensin sen komennolla _sudo apt-get install tree_. Työkalu asentui virtuaalikoneelle alle minuutissa.

<img width="1160" height="527" alt="20" src="https://github.com/user-attachments/assets/2d25862f-3bd9-4be1-95cc-9235c5bc5ab1" />

Testasin komentoa _tree_ eri hakemistoissa. Tree on mielestäni visuaalisempi ja helpommin hahmotettava listauskomento, kuin esimerkiksi _ls_. 
  - _/_ on root directory eli juurihakemisto, jonka alla kaikki muut tiedostot ovat. Kokeilin _tree_ komentoa tässä hakemistossa ja kone jyskytti n. 30 sekuntia tiedostojen listauksia, joita tuli lopulta kymmeniä tuhansia.
    
<img width="1165" height="795" alt="23" src="https://github.com/user-attachments/assets/65ac13c0-fa0b-45f0-809c-f5e7b4609642" />

  - komennolla _/home_, ja sain täydellisen listauksen kaikista kansion sisällä olevista tiedostoista. Home-kansio pitää sisällään kaikkien käyttäjien kotikansiot, mutta tässä tapauksessa koneellani on vain yksi käyttäjä eli minä. Komento toimii kaikilla käyttäjillä samalla tavalla.

<img width="1160" height="811" alt="21" src="https://github.com/user-attachments/assets/cd7d1aa0-324e-43fb-81a3-dbee79319497" />

  - _/Etc_ kansio sisältää tietoja järjestelmästä. Tarkastelin, mitä tiedostoja tämä kansio on syönyt, ensin navigoimalla sijaintiin _cd /etc_ ja listasin tiedot komennolla _ls -F_. 
    
<img width="1059" height="821" alt="24" src="https://github.com/user-attachments/assets/16e630fb-94e4-4266-b89f-8cb99b090c67" />

  - Media-kansio sisältää tietoja irrotettavista medioista, kuten /media/cdrom/ tai /media/usbdisk/. Toisiin hakemistoihin pystyy siirtymään antamalla suoraan halutun hakemiston nimi. Navigoin media-hakemistoon etc-hakemistosta komennolla _cd /media_. Listasin näkymän _tree_ ja _ls_ komennoilla, ja omalla koneellani tämä hakemisto ei sisältänyt vielä mitään tiedostoja.

<img width="1064" height="167" alt="25" src="https://github.com/user-attachments/assets/4e6a7368-232c-4070-a467-f4b93d54a105" />

  - _/var/log/_ on hakemisto, joka sisältää järjestelmän lokitiedot. Siirryin hakemistoon komennolla _cd /var/log_ ja listasin _ls_ komennolla. Kokeilin avata boot-lokin admineilla _sudo nano boot.log_, mutta tiedosto oli tyhjää täynnä (0 riviä). Miksi, se selvinnee seuraavassa jaksossa? 
    
<img width="1078" height="149" alt="26" src="https://github.com/user-attachments/assets/eb5cc30e-2b4c-419c-9465-6ca64982438c" />


## d) Grep-komento

_Grep_ on komento, jolla voi etsiä tiedostoista tiettyä sanaa tai merkkijonoa ja tulostaa haetut rivit.

Komennolla _grep --help_ sain lisätiedot, mitä grep-komennolla voi tehdä. 

<img width="1113" height="812" alt="27" src="https://github.com/user-attachments/assets/c01311fd-026d-4e0f-992c-f63cb8c6ae53" />

Katsoin Linux-wikistä Grepin käyttämisen ohjeita ja kokeilin hakea luennolla harjoituksena luodun _kissa.md_ tiedoston hakemista komennolla ls- R | grep -e kissa_. Listauksessa näkyi haettu tiedosto niin monta kertaa, kuin se löytyy koneeni hakemistoistani. 

<img width="846" height="622" alt="28" src="https://github.com/user-attachments/assets/4e149526-b2b2-4f82-9c41-6d0b824433e1" />


## e) Pipe - putkittaminen (pipes, "|")

Putkittaminen on tehokas ja erittäin hyödyllinen operaatio Linuxin komentorivillä toimiessa. Operaatiolla ketjutetaan yhden ohjelman tuloste, joka voidaan ohjata toiselle ohjelmalle syötteeksi. Operaattorina käytetään "|" -merkkiä. 

Testasin putkittamista Linux-wikin ohjeistuksia seuraten. Wikissä mainittiin hauska pikkuohjelma _cowsay_, joten asensin sen virtuaalikoneelle komennolla _sudo apt-get install cowsay_. Seuraavaksi testasin putkittamista kyseistä ohjelmaa hyödyntäen antamalla komennon _uname -r | cowsay (näyttää ytimen version lehmän suusta ammuttuna). Eli tässä tapauksessa tuloste "ytimen versio" ohjattiin ohjelmalle "cowsay" ja tulostettiin.

<img width="1060" height="814" alt="31" src="https://github.com/user-attachments/assets/9adbf788-9fe4-46f0-bad1-553923cd5e8c" />


## f) Testaamani koneen rauta

Virtuaalikoneellani ei ollut valmiina _lshw_ työkalua koneen tietojen tulostamiseen. "Lshw" = list hardware, ja se tarkoittaa järjestelmäraudan tietoja. Asensin työkalun komennolla _sudo apt-get install lshw_. Asennuksessa ei mennyt montaakaan sekuntia. Tämän jälkeen listasin testikoneeni tiedot komentorivin komennolla _sudo lshw -short -sanitize_.

<img width="1072" height="783" alt="32" src="https://github.com/user-attachments/assets/b5a9355d-3d91-4d8d-a3b1-a5ff98e66930" />

Tietojen analysoinnista:
- järjestelmä pyörii VirtualBoxissa ja sillä on käytössään 4 GB muistia. Täysin tarkkaan en kaikkia kuvassa olevia tietoja osaa tulkita.

  
- H/W path = väyläosoitteet
- Device = laitteet (esim. kiintolevyt, liitetyt USB-laitteet)
- Class = laitteiden kategoria (esim. verkkoyhteydet, prosessori). Näitä voidaan sortata lisäämällä list hardware-komentoon esim. _-input_
      - vielä tarkemmat tiedot esim. luokasta "disk" saa sortattua komennolla _sudo lshw -class disk_
  <img width="1076" height="572" alt="33" src="https://github.com/user-attachments/assets/0585d4a4-5048-4501-bbc7-e8fa61675b0a" />

- Description = kuvaus
  
## g) Cheat-pluginin asennus micro-editorille

Hain verkosta ohjetta cheat-pluginin asennukseen micro-ohjelmalle, ja kappas vain päädyin kurssin opettajamme Tero Karvisen Git-sivuston syövereihin. Pluginin asennus oli helppo ja se tapahtui komennolla _micro --plugin install cheat_. 

<img width="1009" height="107" alt="34" src="https://github.com/user-attachments/assets/74878adc-455d-46fa-a0e6-05da79554205" />

Asennus kesti muutaman sekunnin.

Avasin micro-editorin komennolla _micro_ ja kirjoitin tekstitiedostoon pienen tarinan > tallensin > poistuin editorista. Avasin kyseisen tiedoston uudestaan Microon, jolloin sain allaolevan kuvanmukaisen ilmoituksen ja painettuani _continue_ sain tiedoston auki. 

<img width="689" height="131" alt="35" src="https://github.com/user-attachments/assets/69290cc0-a119-452c-9976-28763bd48449" />

Seurasin Karvisen ohjetta cheatin käytöstä, mutta tässä vaiheessa "F1" painamalla avautui vain selaimeen jokin Xfce Terminal -dokumentaatio, ja plugin ei toiminut odotetulla tavalla. 

<img width="1063" height="621" alt="37" src="https://github.com/user-attachments/assets/e7ed33ce-4171-45c7-b411-f8fc17307adf" />

Asensin vielä lisäksi Karvisen micro-cheat-ohjeessa mainitun lisäpaketin komennolla _sudo apt-get -y install micro fzf pythonpy git exuberant-ctags_. Avasin luomani tiedoston micro-editoriin, mutta sama ongelma jäi - en saanut plugaria toimimaan toivotulla tavalla. Voi hyvinki olla, että vika on myös ruudun ja näppäimistön välissä ;)

- asennuksista yleisesti sanoisin, että kaikki tässä raportissa mainitut kilkkeiden asennukset sujuivat ajallisesti alle minuuttiin, pääasiassa jopa muutamaan sekuntiin.
  
## Lähteet

- Asennettujen ohjelmien sijainnin löytäminen komentoriviltä. Luettavissa: https://askubuntu.com/questions/54395/where-can-i-find-the-location-of-folders-for-installed-programs
- Cheat-plugarin asennus. Luettavissa: https://github.com/terokarvinen/micro-cheat
- Grep-työkalun käyttäminen. Luettavissa: https://www.linux.fi/wiki/Grep
- Komentorivin perusteet. 2025. Putkittaminen komentorivillä ja Cowsay-ohjelman asennus. Luettavissa: https://www.linux.fi/wiki/Komentorivin_perusteet#Putkitus
- Raudan tietojen tulkkaus- lshw. Luettavissa: https://www.linux.com/training-tutorials/deep-hardware-discovery-lshw-and-lsusb-linux/
- Tiedostojen listaaminen komentoriviltä. Luettavissa: https://stackoverflow.com/questions/14827686/list-of-all-folders-and-sub-folders
- Tree-komennon käyttäminen. Luettavissa: https://www.geeksforgeeks.org/linux-unix/tree-command-unixlinux/
- Usean ohjelman asentaminen yhdellä komennolla. Luettavissa: https://askubuntu.com/questions/516850/is-there-any-way-to-install-multiple-software-at-a-single-command-via-terminal


## Tekijätiedot

  - Miika Vänttinen, Haaga-Helia Ammattikorkeakoulu, tietojenkäsittely
  - Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
  - Pohjana Tero Karvinen 2026: Linux kurssi, http://terokarvinen.com
