# h4 Maailma kuulee

## Tiivistelmä materiaalista

- Käytä aina hyvien käytäntöjen mukaisia turvallisia salasanoja tunnuksia luodessa ja järjestelmiä pystyttäessä
- Pilvipalvelimia voi vuokrata edullisin kustannuksin (alkaen muutama €/kk) useilta eri palveluntuottajilta
- SSH-yhteyksien Root-oikeudet tulee poistaa ja palomuuri aina enabloida
- Palvelimet tulee aina pitää päivitettyinä tietoturvasyistä, muista siis ajaa päivityskomentoja


## a) Oman virtuaalipalvelimen vuokraus

Vuokrasin oman virtuaalipalvelimen UpCloudilta https://upcloud.com/. Loin aluksi tilin UpCloudin palveluun. Valitsin tutustumistarjouksen, jolla sain 250€ "starttirahaa" käyttöön. Loin UpCloudin pilvipalvelimelle harjoituksiimme ja peruskäyttöön sopivan palvelimen seuraavilla asetuksilla:
- Sijainti > FI-HEL1 (palvelimen kannattaa olla lähellä palvelun asiakkaita)
- 1 CPU on riittävä 1 GB muistilla ja 10 GB tallennustilalla
- Hintaa tälle paketille tulee 3€/kk
- Operating system > debian GNU/Linux 13 (Trixie) eli sama mitä Karvisen Linux-kurssilla käytämme

Muilta osin menty oletusasetuksilla. Esim. back up -palveluita ei tässä otettu, eikä yleensäkään kannata luottaa pelkästään pilvipalveluntarjoajan varmuuskopiointipalveluun.
  
<img width="1638" height="921" alt="77" src="https://github.com/user-attachments/assets/2d6b5214-778d-41fc-b82f-5acd33b0a4dc" />

<img width="1043" height="704" alt="78" src="https://github.com/user-attachments/assets/4d8091af-8bbf-4a21-89c1-625cc1433863" />

Luotu omalta Debian-virtuaalikoneelta SSH-avain. Se tapahtui komentoriviltä komennolla _ssh-keygen_. Tulostettu komentoriviltä _ls -a_ ja tarkastettu tällä, että _.ssh_ kansio näkyi. Navigoitu .ssh -kansioon ja listattu näkymä _ls_. Julkinen avain oli nyt muodostettu ja .pub on sen merkki. Tulostettu julkinen avain komennolla _cat id_avaimenid.pub_. Tämä julkinen avain saa näkyä muillekin käyttäjille, koska se on nimenomaan julkinen, ja ilman yksityistä (salaista) avainparia sitä ei voi käyttää. 

<img width="1193" height="226" alt="79" src="https://github.com/user-attachments/assets/2e43c74e-0206-44b7-8cdd-e562471dd1de" />

Kopioitu julkinen avain UpCloudin serveriasetuksiin. Nimetty oma palvelin, tallennettu ja käynnistetty palvelin.

<img width="1263" height="825" alt="80" src="https://github.com/user-attachments/assets/cf8f2a84-73a3-4f65-aac4-2de2cabf7521" />

Aikaa virtuaalipalvelimen vuokraukseen ja käynnistämiseen kului n. puoli tuntia huomioiden, että tutkin asiaa rauhassa. Itse palvelimen käynnistys tapahtui parissa minuutissa, eli halutessaan saa nopeasti oman palvelimen pystyyn.

## b) Virtuaalipalvelimen alkutoimet; palomuuri, root-tunnus, ohjelmien päivitys

Otin etäyhteyden virtuaalikoneeltani äsken luodulle virtuaalipalvelimelle roottina komennolla _ssh root@palvelimenip_.

<img width="1041" height="205" alt="82" src="https://github.com/user-attachments/assets/1ab59b76-1c74-49b8-bc0f-d41b8fda8fdb" />

Aluksi tein reiän palomuuriin SSH-yhteyttä varten. Komentoa _sudo ufw allow 22/tcp_ ajaessa herjasi, ettei pakettia löytynyt. Tulin exitillä pois SSH-yhteydestä ja ajoin pakettipäivitykset/ tarvittavien ohjelmien asennukset komennolla _sudo apt-get -y install micro bash-completion openssh-client wget curl ufw_.
 
Tämän jälkeen ajoin uudestaan komennon _sudo ufw allow 22/tcp_, jolla saatiin reikä palomuuriin sekä komento _sudo ufw enable_, jolla palomuuri laitettiin päälle.

<img width="595" height="157" alt="85" src="https://github.com/user-attachments/assets/87ff512c-59bf-48c1-8b51-5c46a5c977da" />

Seuraavaksi tein uuden käyttäjän, jolla voidaan kirjautua virtuaalipalvelimelle. Loin käyttäjän komennolla _
sudo adduser nimi_. Tein käyttäjän nimeltä Seppo ja annettu käyttäjälle admin-oikeudet komennolla _sudo adduser seppo sudo_. 

<img width="715" height="283" alt="86" src="https://github.com/user-attachments/assets/b4681591-724b-44e6-9bdd-7890399b0a26" />


Testasin kirjautumista virtuaalipalvelimelleni "seppo" käyttäjällä ja sain virheen "permission denied". 

<img width="617" height="116" alt="88" src="https://github.com/user-attachments/assets/1843ffd7-30ee-42f5-8185-cf3e6060b4d4" />


Huomasin, että en ollut ajanut palomuurisääntöjä ja ohjelmien asennusta luodulle virtuaalipalvelimelle, vaan koneelle, josta otan etäyhteyttä. Otin roottina etäyhteyden virtuaalipalvelimelleni _ssh root@palvelimenip ja ajoin samat ylläolevat pakettipäivitykset ja asennukset sekä palomuurin reiän + enabloinnin. 

<img width="839" height="165" alt="89" src="https://github.com/user-attachments/assets/b8ab6a39-7550-4e2a-a439-1bc4a05d8fd3" />


Olin siis luonut käyttäjänkin väärälle koneelle, ja loin uuden käyttäjän ylläolevilla komennoilla virtuaalipalvelimelleni ja annettu sudo-oikeudet. Vaikka herjasi kuvanmukaista, niin sudo-oikeudet menivät perille.

<img width="774" height="449" alt="91" src="https://github.com/user-attachments/assets/16b251a8-e15d-4e84-9a2f-845e74c71f1d" />


Kokeilin kirjautua luodulla käyttäjällä SSH-yhteyteen - ei onnistunut "permission denied (public key)".

<img width="594" height="206" alt="92" src="https://github.com/user-attachments/assets/f2aa13bb-723c-4062-a579-ce2066aa4ef2" />


Huomasin, etten ollut kopioinut julkista SSH-avainta käyttäjälle. Kopioitu julkinen avain komennolla _sudo cp -rvn /root/.ssh/ /home/miika/_ ja annettu oikeudet _sudo chown -R miika:miika /home/miika/_.

<img width="701" height="61" alt="93" src="https://github.com/user-attachments/assets/1aa5018f-4e11-4b03-bf50-1d480750de9d" />


Tämän jälkeen SSH-yhteys virtuaalipalvelimelle käyttäjänä "miika" onnistui.

<img width="974" height="299" alt="94" src="https://github.com/user-attachments/assets/e0ff29a9-3faa-41f1-bb46-07a351d86144" />



Suljettu root-käyttäjä komennolla _sudo usermod --lock root_ ja disabloitu rootin kirjautuminen palvelimelle ko
nfaustiedostoa muokkaamalla (permitrootlogin no) > tallennettu.

<img width="799" height="756" alt="95" src="https://github.com/user-attachments/assets/d99416f0-6921-4063-96fe-5eb9b16064e7" />


Käynnistetty palvelu uudelleen komennolla _sudo service ssh restart_. Lopuksi päivitetty vielä palvelin komennoilla _sudo apt-get update_ ja _sudo apt-get upgrade_. Kello oli nyt 11.58, eli melkein tunti meni.


## c) Weppipalvelimen asennus

Aloitin tehtävän klo 13.15

Asensin Apache2 web-palvelimen virtuaalipalvelimelleni etäyhteyteen miika-käyttäjänä kirjautuneena komennolla _sudo apt-get -y install apache2_. Ajoin myös etusivulle uuden näkymän komennolla _echo ”Default”|sudo tee /var/www/html/index.html_.

Kokeilin yhdistää palvelimen etusivulle selaimesta osoitteella https://80.69.174.209/ (palvelimen osoite), mutta ei yhteyttä "unable to connect". 

<img width="1179" height="852" alt="96" src="https://github.com/user-attachments/assets/8900802d-c2f7-4a7e-8be8-a3a0b8696594" />


Tein Karvisen ohjeen mukaiset nimipohjaisen virtuaalihostin asetukset virtuaalipalvelimen konfaustiedostoon sekä enabloin sivun ja käynnistin Apachen uudestaan.

<img width="1177" height="744" alt="97" src="https://github.com/user-attachments/assets/00c5bc7f-99c4-4c1a-b380-9301d7d363ce" />

 
Virtuaalipalvelimelle ei edellenkään saa yhteyttä selaimesta - "unable to connect". Katsoin komennolla _curl_ mitä yhteystesti sanoo sivustolle. Vastaus "could not resolve host".

<img width="561" height="119" alt="98" src="https://github.com/user-attachments/assets/27660307-f56b-447f-8813-f8d273a761b2" />

Vaihdoin konfitiedostoon ServerNameksi virtuaalipalvelimeni osoitteen 80.69.174.209. 

<img width="813" height="446" alt="101" src="https://github.com/user-attachments/assets/b0707749-7539-4919-a4a9-6957b7f85cff" />


Pingasin palvelinta komentoriviltä ja kaikki paketit näyttivät menevän läpi ongelmitta. 

<img width="793" height="404" alt="99" src="https://github.com/user-attachments/assets/9fd24a32-6a0e-425b-ab4e-e4991653c856" />


Avasin virtuaalipalvelimelle vielä toisen portin Susanna Lehdon ohjeen mukaisesti sudolla _sudo ufw allow 80/tcp_. Ajoin myös uudelleenkäynnistykset _sudo systemctl restart apache2_ sekä sudo service apache2 restart_. Edelleenkään ei etusivulle saa yhteyttä, sama ongelma.

<img width="541" height="134" alt="100" src="https://github.com/user-attachments/assets/b8cbb136-fa02-4b89-800b-6c4d62b6f4fb" />

Sivun tietoja löytyy kyllä /etc/apache/ -kansiosta. 

<img width="898" height="243" alt="102" src="https://github.com/user-attachments/assets/1a2b662a-6402-41f6-82f5-f3e64009e4a9" />


Lopetin tehtävän tarkastelun klo 14.25, koska en nyt saanut selville, miksi yhteys etusivulle ei toimi. Selvitettävä vielä.

Edit 7.2.2026

En malttanut olla tutkimatta tätä sivun näkyvyyden ongelmaa vielä lisää. Huomasin, että olin koittanu ottaa etusivua näkyviin https-yhteydellä, vaikka tähän pitäisi olla http. Http//palvelimenip antaa käyttöoikeusvirhettä. Olin jo aiemmin kyllä antanut oikeudet "miika" käyttäjälle chmodilla. Tutkin asiaa ja konfaustiedosto oli väärässä polussa > siirsin tiedoston konfaustiedostoon määriteltyyn polkuun. Index.html -sivu pitäisi olla oikeassa polussa. Tässä vaiheessa silmäni olivat jo niin mutkalla, että tarvitsen lisäsilmäpareja katsomaan, mikä tässä menee vielä pieleen. Lopetin klo 15.16 ja selvitetään tätä vielä.

<img width="1243" height="415" alt="ongelmanselvitys1" src="https://github.com/user-attachments/assets/0e08e3f4-c9c5-43a3-ad74-ee0193ade77e" />

Edit 15.2.2026

Selvitelty luennolla porukalla sivuston toimimattomuutta. Ongelmanselvitystä tehty virhelokeja tutkimalla komennoilla: _tail -1 /var/log/apache2/error.log_ ja _Sudo apachectl configtest_. Lokeista selvisi, että olin luonut konfaustiedoston väärään sijantiin. Siirsin konfitiedoston oikeaan sijaintiin komennolla _sudo mv /home/miika/publicsites/miika.example.com.conf /etc/apache2/sites-available/_. Sivuston konfaustiedot on nyt järjestelmäasetuksissa käyttäjän kotikansion sijaan. 

Disabloitu oletussivu 000-default komennolla _sudo a2dissite 000-default.conf_. Enabloitu oman sivusto komennolla _sudo a2ensite miika.example.com.conf_. Käynnistetty Apache -palveu uudestaan _sudo systemctl restart apache2_.

<img width="1428" height="853" alt="ongelmanselvitys3" src="https://github.com/user-attachments/assets/a47c1c18-6b30-4b1b-a168-dc66350b26d8" />

Virhelokeista myös selvisi, että sivustolle en ollut tehnyt etusivua. Tein kansion etusivua varten sijantiin _/home/miika komennolla mkdir /home/miika/publicsites/miika.example.com_

<img width="1905" height="737" alt="ongelmanselvitys2" src="https://github.com/user-attachments/assets/371de7d9-bddd-494b-ab9d-e037588e6a32" />

Tein itse etusivun tänne kansioon komennolla _micro index.html_ eli index-sivun polku kaikkinensa on _/publicsites/miika.example.com$ micro index.html_. Lisätty index.html -tiedostoon HTML-koodia, josta tulee palvelimeni etusivu.

<img width="988" height="628" alt="ongelmanselvitys4" src="https://github.com/user-attachments/assets/f8b28945-3fb1-408f-a6b4-9679ce85c264" />

Oma etusivu toimi nyt testaessa ongelmitta ja näytti halutun mukaiselta. Tästä on hyvä jatkaa palvelun kehittämistä. Palvelimelle pääsee kiinni testatusti myös omalta puhelimelta.

Korjauksiin kului aikaa noin 15 minuuttia.

## d) Oman virtuaalipalvelimen Name Based Virtual Host ja asetukset

Edeltävässä tehtävässä olin jo alkanut tehdä tätä, mutta en saanut yhteyttä palvelimelle, joten näkyvyyden testaus ei onnistu. Selvitettävä.

Edit 15.2.2026.

Virtual hostin asetukset olivat jo kunnossa. Tarkistettu nämä asetukset ja tulostettu niitä komentoriviltä. Sivustoa pystyi nyt myös muokkaaman ilman sudoa.

<img width="1056" height="546" alt="ongelmanselvitys5" src="https://github.com/user-attachments/assets/71af961a-c68c-495a-86ed-75ccbf4d2d4b" />

<img width="931" height="429" alt="ongelmanselvitys6" src="https://github.com/user-attachments/assets/02bc6464-604e-46f1-a4d6-126ad3dbbfac" />

Testasin _curl_ komennolla yhteyksiä palvelimelle ja testi palautti halutun tulokset - onnistui.

<img width="928" height="267" alt="ongelmanselvitys7" src="https://github.com/user-attachments/assets/a322b799-60ed-437e-9f70-e20d1d34903b" />

Aikaa asetusten tarkistamiseen, ihmettelyyn ja testeihin kului noin 10 minuuttia.

## Muokkaukset

7.2.2026 ongelmanselvitystä tehtävä c)

15.2.2026 tehtävä c) - oman sivuston asetukset kuntoon. Tehtävä d) virtual host kuntoon.

## Lähteet

- Asennusohjeita. Luettavissa: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
- Name based Vhost -ohjeita. Luettavissa: https://httpd.apache.org/docs/2.4/vhosts/name-based.html
  
## Tekijätiedot
- Miika Vänttinen, Haaga-Helia Ammattikorkeakoulu, tietojenkäsittely
- Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
- Pohjana Tero Karvinen 2026: Linux kurssi, http://terokarvinen.com









