# H6 Salataampa
	
## Tiivistelmä
	
- Lets encryptin palvelun ja AMCE-protokollan (automatic certificate management environment) tavoite on mahdollistaa HTTPS -protokollan käyttöönotto ja  automaattinen hankkiminen. 
- Käyttöönotto toteutetaan ACME-asiakasohjelmalla. ACME -asiakas vastaa Let's Encryptin CA:n tiliavainparin haasteella , jolla se todistaa hallitsevansa omistamiaan verkkotunnuksia
- Asiakas allekirjoittaa CSR (Certificate Signing Request) pyynnön omalla julkisella avaimellaan, joka tarkastetaan Lets Encryptin palvelussa. Jos kaikki näyttää olevan kunnossa, Let's Encrypt lähettää  vastaukseksi sertifikaatin
- Portti 443 tarvitaan auki palomuurista, jotta yhteys HTTPS-protokollalla (salattu yhteys) toimii

## a) TLS-serfifikaatin hankkiminen Let's Encryptiltä

Aloitin tehtävän klo 16.45. Kirjauduin SSH-yhteydellä palvelimelleni. Aluksi testasin, että palvelimeni vastaa käyttäen komentoa _curl vanttinen.org_. 

<img width="916" height="243" alt="123" src="https://github.com/user-attachments/assets/b8e2ab88-7a24-4a59-8914-c123e99742c7" />

Seuraavaksi varmistin, että palvelimeltani on tarvittavat portit auki komennolla _sudo ufw status verbose_. Auki oli portit 22 - SSH, ja 80 - HTTP (salaamaton yhteys). Avasin palomuuriin vielä tarvittavan HTTPS-protokollan portin 443 komennolla _sudo ufw allow 443/tcp_.

<img width="548" height="113" alt="125" src="https://github.com/user-attachments/assets/2692be0a-c77b-4ac9-98b8-b8fad0c5406d" />

Sertifikaatin asennuksen aloitin päivittämällä pakettiohjelmiston _sudo apt-get update_. Sen jälkeen certbotin asennus komennolla _sudo apt install certbot_ sekä samalla Python plugarin _python3-certbot-apache_. Kuvassa olin jo kerennyt nämä asentaa.

<img width="659" height="187" alt="126" src="https://github.com/user-attachments/assets/90044840-c863-47fa-9a65-eb9aa875db47" />

Sitten itse sertifikaatin pyytäminen. Tämän tein komennolla _sudo certbot_. Pyysin sertifikaattia molemmille rekisteröidyille domaineilla vanttinen.org sekä www.vanttinen.org. Pyyntö suoritettu onnistuneesti.

<img width="1147" height="567" alt="127" src="https://github.com/user-attachments/assets/e1a81a67-3a33-40cb-900d-b61e8dfdd968" />

Varmistin vielä, että HTTPS:n portti on palvelimeltani auki: komento _nc -vz vanttinen.org 443_. Portti oli auki, kuten pitikin. 

<img width="785" height="97" alt="129" src="https://github.com/user-attachments/assets/56b48e27-87a4-4fef-be51-b5399fd670ce" />

Testasin, että sertifikaatti toimii oikein ja otin yhteyden palvelimelleni selaimelta kirjoittamalla osoiteriville vanttinen.org. Sertifikaatin asennus onnistui ongelmitta.

Edgen selaimen näkymä:
<img width="519" height="302" alt="128" src="https://github.com/user-attachments/assets/868de8db-b1ac-40b2-8b42-c966f8918a98" />

Chromen selain:
<img width="808" height="737" alt="130" src="https://github.com/user-attachments/assets/54bbebf0-7505-44b8-9498-4e687dbf34a8" />

## b) A-rating testaus

Testasin sivustoni toiminnan yleisellä TLS-laadunvarmistustyökalulla. Käytin tähän Qualys SSL labsin työkalua, jonne hain oman domainini hakukenttään ja sain tulokseksi A-luokituksen. Eli hyvin toimi! 

<img width="1057" height="1374" alt="131" src="https://github.com/user-attachments/assets/5ed31551-fc01-4e89-a531-d2ab5bab4082" />

Tarkistin vielä palvelimeni konfitiedoston, johon SSL-muutokset olivat puraisseet sertifikaatin hankkimisen jälkeen oikein, kuten pitääkin.

<img width="871" height="546" alt="132" src="https://github.com/user-attachments/assets/17c56aa5-3bfd-41a0-a2e3-0de5e20858b4" />


Weppisivujen turvallisuuden kannalta on oleellista, että palvelussa käytetään aina salattua yhteyttä (HTTPS). Skenaario; vain HTTP-protokollaa (salaamaton) käyttävä sivusto sisältää weppilomakkeen, johon käyttäjä syöttää tunnuksen ja salasanan. Tunnukset välitetään verkon yli salaamattomana. Kuuntelemalla verkkoliikennettä esimerkiksi Wireshark-ohjelmistolla, tunnukset voidaan saada vääriin käsiin varsin selkokielisenä. HTTPS-protokolla salaa myös esimerkin tapauksessa liikenteen, ja on näin huomattavasti turvallisempi sekä palvelun käytettävyyden ja luotettavuuden kannalta parempi vaihtoehto. Nyrkkisääntönä: webissä asioidessa ei kannata käyttää mitään palveluita, joilla ei ole sertifikaattia ja salattua HTTPS-yhteyttä.

Tehtävän tekemisen lopetin klo 18.50. Aikaa kului reilu tunti.

## Lähteet

- Sertifikaateista. Luettavissa: https://letsencrypt.org/how-it-works/
- Tero Karvinen 2026. Linux-kurssi. Luettavissa: http://terokarvinen.com
- Konfiguraatiot. Luettavissa: https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample
  
## Tekijätiedot
- Miika Vänttinen, Haaga-Helia Ammattikorkeakoulu, tietojenkäsittely
- Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
- Pohjana Tero Karvinen 2026: Linux kurssi, http://terokarvinen.com


