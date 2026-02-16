# harjoitus 5 - Nimekäs
Tässä raportissa vuokraan nimipalvelun ja laitan julkisen nimen osoittamaan omaan koneeseeni sekä teen alidomainit. Tutkin myös dig ja host-komentoja.

## a) Nimi osoittamaan omaan koneeseen

Aloitin raportin kirjoittamisen klo 21.40

Jotta palvelin oikeasti toimii järkevästi ja on helposti käyttäjien saatavilla, tulee sille asettaa DNS-palvelu (nimipalvelin). Tämän avulla palvelimelle saadaan nimenosoitus; esim www.vanttinen.com, jonka takana pyörisi palvelimeni IP xx.xx.xx.xx. DNS-palvelu muuntaa ihmisen ymmärtämiä nimiä (osoitteita) koneiden ymmärtämiksi IP-osoitteiksi. Näin ihmisten ei tarvitse tietää palveluiden hankalasti muistettavia IP-osoitteita palveluita käyttäessä, vaan helpommin ymmärrettäviä nimiä, kuten mainitsemani www.vanttinen.com. DNS-palvelua voi ajatella verkon puhelinluettelona; kuka vastaa tästä osoitteesta?

Vuokrasin virtuaalipalvelimelleni nimipalvelun Namecheap palvelusta, josta mainittiin Karvisen luennolla. Lähtökohtaisesti kannatta valita .com -päätteinen osoite, mikäli sellainen on saatavilla. Tässä tapauksessa haluamani vanttinen.com oli varattu, joten valitsin .org -päätteisen osoitteen. Org-päätteistä nimeä käytetään yleensä voittoa tavoittelemattomissa palveluissa, ja se sopii minulle tähän hetkeen mainiosti. Jos/kun teen kaupallisemman palvelun myöhemmin, valitsisin .com päätteen muulle nimelle. 
<img width="1110" height="729" alt="105" src="https://github.com/user-attachments/assets/787225a6-fe59-446f-b42f-1918cf7b2673" />

Vuokrasin nimipalvelun vuodeksi eteenpäin automaattisen uusiutumisen vaihtoehdolla, jolloin nimi pysyy hallinnassani, kunnes peruutan sen. Domain privacy jäi oletusasetuksille "auto renew" ja lisäpalveluita en tähän ottanut. Koska minulla ei ollut valmiina tiliä Namecheapilla, loin sellaisen nimipalvelun ostovaiheessa. Täytin pakolliset yhteystiedot. Tietoja täyttäessä tuli lomake, jossa tiedusteltiin registrant, admin, technical ja billing contactia, nämä jätin oletuksille eli itseni kaikkiin kohtiin. Jos kysymyksessä olisi yritys, näihin kannattaisi valita asianmukaiset henkilöt tietoineen. Domain privacyn jätin ehdottomasti päälle, jolloin yhteystietoni ei tule esille Whois palvelussa. Domain privacy on ilmainen lisäosa. Loppusummaksi Namecheapin nimipalvelulla vuodeksi tuli 7,68 $.

<img width="1256" height="773" alt="106" src="https://github.com/user-attachments/assets/d9ad3297-c0f5-4fe6-acc0-60e087be4e87" />

<img width="1223" height="921" alt="107" src="https://github.com/user-attachments/assets/179799ce-7baa-4a13-a41e-ce5c5bd41ed0" />

Testasin vielä, että pääsen varmasti kirjautumaan tunnuksillani palveluun, ja vahvistin tilin sähköpostistani - onnistui.

Seuraavaksi tein varsinaiset nimenosoitukset. Valitsin Namecheapin palvelussa domain list > domainini vanttinen.org > advanced DNS ja poistin aluksi kaikki jämätietueet. Tein uuden tietueen "add new record" -valinnalla ja lisäsin uuden A-tietueen. Ensimmäiseen laitoin Host: "@" ja value: palvelimeni IP-osoite. Toiseen valitsin Host: www ja valua: palvelimeni IP-osoite. TTL (time to live) laitoin 5 min. Nyt minulla on kaksi tietuetta osoittamassa palvelimelleni. 

<img width="1051" height="389" alt="109" src="https://github.com/user-attachments/assets/13fef03b-ba6a-46d3-bccf-40b010d64794" />



## b) Alidomain

Seurasin Namecheapin omaa dokumentaatiota alidomainin asettamisesta. Se tapahtui domain listin kautta > advanced DNS > Add new record. Valitsin tyypiksi A tietueen: host - example, value - palvelimen IP-osoite. Toisen tietueen tein CNAMElla: host - example, value - dns.vanttinen.org. Palvelimeni vastasi hienosti testatessa yhteyttä oman kotikoneeni selaimella. Myös alidomainit toimivat.

<img width="1020" height="346" alt="112" src="https://github.com/user-attachments/assets/afa0d1b8-a9ae-401e-9609-8865b0c7bbc1" />

<img width="492" height="265" alt="110" src="https://github.com/user-attachments/assets/81e4e4bc-0ca6-437a-a485-43eab4c1209d" />

<img width="492" height="223" alt="111" src="https://github.com/user-attachments/assets/a36f861d-dfdf-4cc9-b445-2c295e1b5373" />



## c) DNS-tietojen tutkiminen "host" ja "dig" komennoilla

Host-komento on työkalu DNS-hakujen tekemiseen. Sen avulla voidaan selvittää, mikä IP-osoite kuuluu millekin verkkotunnukselle ja toistepäin, tunnistaa nimipalvelimia tai esim. selvittää sähköpostipalvelimen tiedot. 

Minulla ei ollut host-työkalua asennettuna virtuaalikoneelleni. Asensin sen komennolla _sudo apt-get install host_. Tämän jälkeen ajoin komennon, jolla selvitin oman verkkosivuni tietoja seuraavilla komennoilla: 
  - _host -t mx vanttinen.org_ - sähköpostin käsittelijä. 
  - _host -t ns vanttinen.org_ - nimipalvelintiedot / NS-tietueet
  - _host -a vanttinen.org_ - verkkotunnuksen kaikkien tietueiden tiedot
NOERROR tarkoitti, että kysely onnistui. Oman palvelimeni kyselyssä näkyi AUTHORITY (viralliset nimipalvelimet) 0 ja namecheapilla 8. Johtuisiko tämä siitä, että vuokrasin nimipalvelun ihan vasta ja kaikkia asetuksia ei ole vielä palvelimellani? TTL oli omalla palvelimellani (TTL 1680 sek) määritetty pienemmäksi, kuin namecheapin (3200 sek) 

<img width="867" height="798" alt="114" src="https://github.com/user-attachments/assets/ab1db39d-ec59-47d2-9a40-d4d5bddcbb32" />

Yksinkertainen komento _host vanttinen.org_ palautti palvelun IP-osoitetiedot. 
<img width="738" height="240" alt="115" src="https://github.com/user-attachments/assets/aac09ff5-7d09-4fc3-9fbb-c11e7e6e1388" />

Painotalo Keski-Suomalaisen palvelimen tiedot: 

<img width="998" height="229" alt="116" src="https://github.com/user-attachments/assets/7261e008-ce33-40b9-a359-4f3115de2b00" />

Amazonin nimipalvelintiedot, joita löytyikin vinopino erilaisia rekisteröityjä nimiä:
<img width="443" height="194" alt="117" src="https://github.com/user-attachments/assets/bae90e9b-b0f0-4a1c-b971-52652629acd2" />

Dig-työkalun (Domain Information Groper) testauksissa asensin aluksin työkalun virtuaalikoneelleni komennolla _sudo apt-get install dnsutils_. Sitä käytetään mm. DNS-ongelmien selvityksessä ja vianmäärityksessä sekä DNS-hakujen tekemiseen.

Kokeilin dig-komentoa _dig vanttinen.org +noall +answer_. Lisävalinnat: _noall_ piilottaa kaikki osiot ja _answer_ näyttää tärkeimmät eli vain vastaukset.
Komennon tulkinta: 
  - vanttinen.org - verkkotunnus
  - 34 - TTL
  - IN - internet-luokka
  - A - tietuetyyppi
  - viimeisenä palvelimeni IP-osoite
<img width="653" height="90" alt="118" src="https://github.com/user-attachments/assets/379c6f68-cd30-4831-afe6-719e12b41e34" />

Muita dig-komentoja: _dig amazon.com MX_ - verkkotunnuksen MX-tietue (mail exchanger). Kertoo sähköpostin ohjaustietoja, minne palvelimelle tunnuksen sähköpostit ohjataan.

<img width="765" height="510" alt="119" src="https://github.com/user-attachments/assets/88baff71-2ea9-45da-b03b-bdf55d915951" />

Komennon perään laittamalla _+short_ saadaan siistittyä tulostetta. Alla kuvassa keskisuomalainen.fi:n sähköpostipalvelimen tiedot.

<img width="522" height="64" alt="120" src="https://github.com/user-attachments/assets/e4c2416e-4bc5-418a-9b93-28b7d310f1f1" />

Testien suorittamisen ja raportin kirjoittamisen lopetin klo 00.05. Aikaa tähän oppikokemukseen kului n. 2,5h. 

## Lähteet

-  Alidomainit. Luettavissa: https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/
-  Dig-työkalu ja asennus. Luettavissa: https://www.geeksforgeeks.org/linux-unix/dig-command-in-linux-with-examples/
-  Dig-työkalu. Luettavissa: https://linuxize.com/post/how-to-use-dig-command-to-query-dns-in-linux/
-  Host ja dig -komennoista. Luettavissa: https://blog.udemy.com/dns-lookup-command/




## Tekijätiedot
- Miika Vänttinen, Haaga-Helia Ammattikorkeakoulu, tietojenkäsittely
- Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
- Pohjana Tero Karvinen 2026: Linux kurssi, http://terokarvinen.com
