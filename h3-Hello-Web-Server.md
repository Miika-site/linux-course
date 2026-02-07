# H3 Hello Web Server

- Nimipohjaisessa virtuaalihostingissa isäntäpalvelimet voivat jakaa saman IP-osoitteen mahdollistaen asiakkaiden palvelemisen samasta IP-osoitteesta määrittämällä Apache HTTP Serverin tunnistamaan eri isäntänimet. Tämä on yksinkertaisempi ja suositellumpi tapa hallita palvelimen yhteyksiä.
- IP-pohjaisessa virtuaali-isännöinnissä tarvitaan IP-osoitteiden määritys jokaiselle hostille erikseen
- Nimipohjainen virtuaalihallinta asennetaan ja määritetään Apache-palvelimelle Linuxin komentoriviltä


## a) Weppipalvelimen localhost-osoitteen testaus ja Apache-weppipalvelin

Tämän raportin tehtävien tekemiseen käytetty samaa host-konetta ja virtuaaliympäristöä, kuin aiemmissa raporteissa.

Aina aluksi kannattaa ajaa komento _sudo apt-get update_, joka päivittää Linuxin pakettikirjaston. Annettu komento tässäkin tapauksessa ennen muita asennuksia. Päivitykseen kului aikaa noin 10 sekuntia.

Virtuaalikoneelleni oli jo asennettuna Apache2-palvelin. Mikäli asennuksen tarvitsee, sen saa asennettua komennolla _Sudo apt-get install apache2_.

Testasin localhostin toiminnan virtuaalikoneelta. Se tapahtui kirjoittamalla selaimen osoitekenttään _http://localhost_, joka viittaa siis koneeseen itseensä. Komennolla voidaan testata, että koneen perusverkkotoiminnot ovat ok. Olin jo kerennyt määrittää muutamat asetukset (näistä myöhemmin), ja alla olevassa kuvassa näkyy määrittämäni palvelimen web-sivu selaimeen avattuna _localhost_ osoitteesta. Palvelimen verkkopino siis näiltä osin kunnossa.
<img width="977" height="494" alt="45" src="https://github.com/user-attachments/assets/19bccf47-3513-45c9-98c8-1c75d058927a" />

## b) Lokien tarkastelu ja analysointi 

Tutkin lokitietoja, jotka muodostuvat, kun palvelimeltani ladataan yksi web-sivu. Avattu oma defaut-kotisivu eli käytännös tämä localhost selaimeen. Lokien tarkastelu kävi komennolla _sudo tail /var/log/apache2/access.log_

<img width="1288" height="439" alt="46" src="https://github.com/user-attachments/assets/513786db-0b52-4717-b6ef-7f1e59282fba" />

127.0.0.1 on loopback-osoite eli viittaa koneeseen itseensä. Tämä on localhost. Seuraavaksi näkyy päivämäärä ja kellonaika sekä aikavyöhyke. _GET_ on HTTP pyyntö, eli haetaan sivuston sisältöä HTTP-protokollalla. Selaimena toimii Mozilla versio 5.0. Suluissa käyttäjärjestelmä Linux x86. Gecko/20100101 on Firefoxin käyttämä käyttäjäagentti, joka renderöi verkkosisältöä Linuxissa.




## c) Uusi etusivu palvelimelle
Etusivu uusiksi. Tee uusi name based virtual host. Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).

Tein aluksi nimipohjaisen virtuaalihostin määrityksen. Loin uuden konfaustiedosto komennolla _sudoedit /etc/apache2/sites-available/hattu.example.com.conf_.

Määritin hattu.example.com sivuston tarvittavat konfaukset. 

<img width="850" height="837" alt="48" src="https://github.com/user-attachments/assets/0ddb8cb5-e5ad-4c7d-82cc-ba5026e1ff79" />

Enabloitu sivusto komennolla _sudo a2ensite hattu.example.com_ ja käynnistetty palvelin uudestaan _sudo systemctl restart apache2_.

<img width="648" height="200" alt="50" src="https://github.com/user-attachments/assets/86ebae1a-7847-4523-a80f-4d38b9792733" />

Sivustoa testatessa selaimen osoiterivltä 127.0.0.1 sain tässä kohtaa virheen "403 forbidden", joka johtuu siitä, että tavallisella käyttäjällä ei ole vielä sivuston oikeuksia. 

<img width="732" height="427" alt="51" src="https://github.com/user-attachments/assets/bdab422e-ff4a-4215-b787-33b9348077bf" />

Tarkastettu virheilmoitus komentoriviltä _sudo tail -1 /var/log/apache/error.log_. 

<img width="1280" height="125" alt="52" src="https://github.com/user-attachments/assets/09129210-caa4-4a3d-8402-11436cf2c03c" />

Annettu oikeudet käyttäjälle "miika" komennolla _chmod ugo+x /home/miika_. Latasin sivun selaimesta uudestaan, mutta vieläkään ei toiminut. Katsoin mistä kiikastaa komentorivin komennolla _sudo apachectl configtest_, josta ilmeni, ettei hakemistoa _/home/xubuntu/publicsites/miika.example.com_ ole olemassa. Tässä kohtaa lienee konfaukset menivät sekaisin luennolla tehdyn testisivun konfauksien kanssa, koska tämän raportin tehtävässä on kyse hattu.example.com -sivustosta.

<img width="1274" height="194" alt="54" src="https://github.com/user-attachments/assets/f639416b-7ea0-413b-8bb3-3f712bc1971b" />

Latasin sivun selaimesta uudestaan, mutta vieläkään ei toiminut. Katsoin mistä kiikastaa komentorivin komennolla _sudo apachectl configtest_, josta ilmeni, ettei hakemistoa _/home/xubuntu/publicsites/miika.example.com_ ole olemassa. Tässä kohtaa lienee konfaukset menivät sekaisin luennolla tehdyn testisivun konfauksien kanssa, koska tämän raportin tehtävässä on kyse hattu.example.com -sivustosta.

<img width="1274" height="194" alt="image" src="https://github.com/user-attachments/assets/92a1576f-0634-4eb2-a3a9-456663f954f2" />


Avattu Micro-editoriin sivuston asetustiedosto komennolla micro _tiedostonnimi_. Korjattu hattu.example.com konfaustiedostoon DocumentRoot ja Directory polut oikein ja tallennettu.

<img width="790" height="350" alt="image" src="https://github.com/user-attachments/assets/2d250059-8b44-4085-8a15-dcddf5279dc2" />



Ajettu komento sudo apachectl configtest, joka antoi taas uuden virheen. Kuva alla.

<img width="1286" height="206" alt="image" src="https://github.com/user-attachments/assets/283faf00-6128-4f3a-801f-38fc7a5bb147" />


Katsoin mitä tiedostoja sites-enabled -kansio sisältää. 

<img width="836" height="189" alt="image" src="https://github.com/user-attachments/assets/5c169947-f6e0-402f-be04-64d2f468b66b" />

Avasin hattu.example.com.conf -tiedoston ja tarkistin syntaksit. Tiedostosta puuttui Directory-sulku. Lisätty _</Directory>_ tiedostoon ja tallennettu. 

<img width="685" height="388" alt="image" src="https://github.com/user-attachments/assets/3a5609e7-1fa9-455d-84ac-09d60cc75065" />


Tässä vaiheessa käynnistin palvelimen uudestaan komennolla _sudo systemctl restart apache2_.

Sivuston määritysasetuksissa on vielä jotain pielessä, ja ne eivät toimi. Virhettä kuvassa. Eli tiedostoa puuttuu tarvittavasta sijainnista.

<img width="1285" height="243" alt="image" src="https://github.com/user-attachments/assets/3f73ae67-aacb-4da3-94fa-9ef07856b06e" />



Tarkistettu virheessä mainittu tiedostopolku /home/miika/publicsite/miika, mitä kansio sisältää. Kansiossa on index.html -tiedosto, joka käsittääkseni pitäisi olla sivustoni etusivu. Tässä kohtaa menin nyt hieman solmuun ja sivuston näkyvyys jäi vielä vaiheeseen.

<img width="681" height="179" alt="image" src="https://github.com/user-attachments/assets/1648b246-49a0-4ded-ad94-dda6aafce3fa" />


Kokeilin disabloida aiemmin luodun sivuston komennolla _sudo a2dissite miika.example.com.conf_. Ajoin tämän jälkeen vielä _systemctl reload apache2_.

<img width="605" height="156" alt="image" src="https://github.com/user-attachments/assets/4200b07f-a7d2-44c2-a0ca-0e7fdc3bf8ee" />


Reloadia ajaessa piti varmistaa toiminto admin-salasanalla.
<img width="619" height="387" alt="image" src="https://github.com/user-attachments/assets/a8a8e0d2-01ee-4174-8514-33c7cb873cb3" />


Tarkistettu, että hattu.example.com sivusto on enabloituna. 

<img width="527" height="109" alt="image" src="https://github.com/user-attachments/assets/25c36ad8-8a28-490b-a1c9-347b51492d2c" />


Tarkistettu, mikä konfaustiedoston toiminnan tilanne on. Polkua sivustolle ei löydy.

<img width="1293" height="279" alt="image" src="https://github.com/user-attachments/assets/33aa941e-2414-4540-a695-367f8f576ea0" />


Koitin hakea _hattu.example.com.conf_ -tiedostoa komentoriviltä _find_ komennolla, löytämättä sitä. Konfaustiedoston kyllä aiemmin loin, mutta missä se on?

<img width="1293" height="279" alt="image" src="https://github.com/user-attachments/assets/c0de4b11-4299-4c5b-9d29-f506a7859f5d" />


Katsoin tekemääni raporttia taaksepäin ja huomasin, että loin konfaustiedoston polkuun _/etc/apache2/sites-available_. Siirsin hattu.examplen konfitiedoston oikeaan polkuun, eli siihen, jonka olin konfaustiedostoon määrittäny (/home/miika/publicsite) komennolla _sudo mv polku -t haluttu sijainti. 

<img width="1189" height="157" alt="image" src="https://github.com/user-attachments/assets/ec3485dd-214d-4eb9-82dc-e1b2bc935b98" />


Ajoin _sudo apachectl configtest_, ja nyt ei tullut herjoja.

<img width="1299" height="131" alt="image" src="https://github.com/user-attachments/assets/e6e6c648-84c7-44d5-bc99-fa748301f03d" />


Kokeilin localhost-sivustoa selaimella, mutta edellee antoi 403 forbidden -virhettä.

Ajoin error log -tarkastelukomennon jälleen ja alla tiedot. Herjasi oikeuksista.

<img width="1280" height="110" alt="image" src="https://github.com/user-attachments/assets/466e23f8-a184-42e3-92e5-b1abd70f2790" />


Annettu käyttöoikeudet "miika" käyttäjälle uudestaan. Ajettu configtest, joka herjasi edelleen virhettä. Käynnistetty vielä palvelin uudestaan ja testattu sivustoa selaimella, joka VIHDOINKIN toimi. 

<img width="1295" height="176" alt="image" src="https://github.com/user-attachments/assets/42d27d41-e3f4-4d0d-8851-4dd927a675e5" />

<img width="1084" height="680" alt="image" src="https://github.com/user-attachments/assets/8f81171f-471b-4a27-ab7b-56ac77b1b342" />



ATK:ssa aina tulee vastaan ongelmia ja tähän selvityksen aikaa kului noin kolme tuntia. Itse konfauksen tekeminen onnistuessaan ei ole monenkaan minuutin homma. Oppikokemus tämäkin.


## e) Validin HTML5 sivun tekeminen

Koitin Karvisen ohjeen mukaan tehdä normaalikäyttäjänä uuden HTML-sivun. Tunnin selvittelin oman HTML-sivun lisäämistä ja tämä kohta ei nyt itselleni ihan auennut ja en saanut sivustoa toimimaan. Tähän tarvitsen vinkkejä lisää. 

<img width="1044" height="256" alt="image" src="https://github.com/user-attachments/assets/d6b0dbc8-2903-4d89-aa6b-e481397ef1ca" />

Edit 7.2.2026. 

Korjattu oma HTML-sivusto. Sivuston konfaustiedosto oli väärässä sijainnissa /home/miika. Siirretty konfi-tiedosto järjestelmäasetusten kansion alle /etc/apache2/sites-enabled. Ajettu palvelimen uudelleen käynnistys _restart apache2_. Navigoitu index.hmtl -sivulle, joka on sijainnissa /publicsites/miika, ja luotu HTML-koodia etusivulle. Tiedostoa pystyi muokkaamaan ilman sudo-oikeuksia, kuten tehtävänannossa kuului. Tallennettu tiedosto ja testattu sivuston näkymä, joka näytti nyt validilta.

<img width="701" height="155" alt="76 1" src="https://github.com/user-attachments/assets/77b0df3c-002b-4ac9-a209-7129c3fd1465" />

<img width="1145" height="603" alt="76 2" src="https://github.com/user-attachments/assets/29f0733e-90cd-4ca8-901e-e6b79bfa4b86" />





## f) Esimerkit 'curl -I' ja 'curl' -komennoista

Curl-komentoa käytetään tiedon siirtämiseen järjestelmän ja palvelimen välillä eriliasia protokollia hyödyntäen. Sillä voidaan myös testata mm. API- ja REST-rajapintoja. 

Testasin _curl_-komentoa komentoriviltä kirjoittamalla _curl localhost_.  Syntaksi on siis _komento_ + _haluttu URL-osoite/isäntä_. Tässä tapauksessa sain vastaukseksi sivustoni otsikon "hellureiii". Sivustollani ei tällä hetkellä ole paljoa muuta näytettävää, joten curl -vastaus on sen mukainen.

Komennolla curl -i saadaan tulosteeseen myös HTTP-vastausotsikot. 

<img width="615" height="383" alt="image" src="https://github.com/user-attachments/assets/46277629-fbae-4007-9d66-e88ac0293bda" />

- HTTP/1.1 200 OK
		- Vastauslinja ja 200 OK tarkoittaa, että pyyntö onnistui
- Date: päiväys, jolloin palvelin vastasi pyyntöön
- Server: Ohjelmisto, joka vastasi pyyntöön
- Content-type, kertoo datan tiedostotyypin
- Last-modified, milloin tiedostoa on viimeksi muokattu



## m) GitHub Education -paketti.

Olin jo rekisteröitynyt aiemmin GitHub Education paketin. 

<img width="699" height="443" alt="76" src="https://github.com/user-attachments/assets/f53d5422-e005-4e0c-989d-deccaed13896" />


## Muokkaukset
Muokattu tehtävä e) 7.2.2026. Lisätty validi kotisivu toimintaan.

## Lähteet
- Curl-komento. Luettavissa: https://www.w3schools.com/bash/bash_curl.php
- Curl-komennon otsakkeiden selitys. Luettavissa: https://www.baeldung.com/linux/curl-request-headers
- Find-komento. Luettavissa: https://www.geeksforgeeks.org/linux-unix/find-command-in-linux-with-examples/
- HTML Basics. Luettavissa: https://www.w3schools.com/html/html_basic.asp
- User Agent. Luettavissa: https://useragents.io/uas/mozilla-5-0-x11-linux-x86-64-rv128-0-gecko-20100101-firefox-128-0_febf9b0952757bbbe1c625d785f7ba35
  
## Tekijätiedot

  - Miika Vänttinen, Haaga-Helia Ammattikorkeakoulu, tietojenkäsittely
  - Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
  - Pohjana Tero Karvinen 2026: Linux kurssi, http://terokarvinen.com
