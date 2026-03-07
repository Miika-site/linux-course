# h7 Maalisuora

Linux-kurssi alkaa olemaan loppusuoralla. Tässä raportissa tutkaillaan vielä hieman ohjelmointia sekä ratkaisen aiemmalla vastaavan kurssin toteutuksella tehdyn labraharjoituksen. 

## a) Ohjelmointia: "Hei maailma" kolmella kielellä

Aloitin raportin kirjoittamisen klo 11.45. Tehtävän työstämisen virtuaalikoneella aloitin tuttuun tapaan päivittämällä pakettikirjaston _sudo apt update_. Asensin kerralla useamman ohjelmointitulkin komennolla _sudo apt-get install python3 gcc g++ openjdk-17-jdk golang-go ruby lua5.4_. Näistä käytän tässä harjoituksessa Pythonia, C++ ja lisäksi Bashia.

<img width="893" height="84" alt="133" src="https://github.com/user-attachments/assets/45dd4a90-c18f-41bd-a302-5dd92effade7" />

Tein käyttäjän kotihakemistoon jokaista ohjelmointiprojektia varten omat kansiot, jotta kansiorakenne pysyy siistinä. Eli komennot _mkdir bash_, _mkdir python_, _mkdir cplus_. 

Aloitin Bashilla; siirryin projektin kansioon /home/miika/bash ja loin sinne tiedoston, johon itse koodi tulee _micro moikkulismaailma.sh_. Bash on varsin suoraviivainen ja tulostus tapahtuu echo-käskyllä. Ohjelman ajoin komennolla _bash moikkulismaailma.sh_ ja se toimi odotetulla tavalla.

<img width="524" height="318" alt="134" src="https://github.com/user-attachments/assets/56d77406-a9b1-4955-88ca-414b65f44269" />

<img width="507" height="161" alt="135" src="https://github.com/user-attachments/assets/0f157be7-2d3b-44f9-b5f0-57831a895365" />

Seuraavaksi Python. Navigoin aiemmin luotuun python-kansioon, jonne tein ohjelman koodin tekstieditorilla komennolla _micro moikkaus.py_. Koodi print("Hei maailma") editoriin ja tallennus. Ohjelman suoritus tapahtui komennolla _python3 moikkaus.py_. 

<img width="395" height="330" alt="136" src="https://github.com/user-attachments/assets/21d87441-79fd-48b7-8256-d0e6c6b3158d" />
<img width="470" height="116" alt="137" src="https://github.com/user-attachments/assets/7f361a17-9ff2-4570-a9bb-4f7da59c458a" />

C++. Siiryin aiemmin luotuun kansioon "cplus" ja tein sinne tiedoston komennolla _micro moikkaa.cc_. Tallensin koodin ja tein siitä ajettavan ohjelman komennolla _g++ moikkaa.cc -o moikkaa.cc_. Ohjelma löytyy nyt tiedostosta "a.out", jonka suoritin komennolla _./ a.out_.

<img width="434" height="148" alt="140" src="https://github.com/user-attachments/assets/33014fe0-0aa5-4e4c-9452-43d453c2a2ba" />
<img width="328" height="115" alt="139" src="https://github.com/user-attachments/assets/2a832e21-34ae-4303-993e-ffdb14317a25" />



## b) Lähdeviitteiden tarkistus

Aiempien tehtäväraporttien lähdeviitteet olivat melko hyvällä mallilla. Lisäsin vielä Karvisen Linux-kurssin tehtävänannot lähdeviitteisiin. 



## c) Linuxiin uusi komento niin, että kaikki käyttäjät voivat ajaa sitä

Annoin aiemmin tekemääni python-ohjelmaan suoritusoikeudet muille käyttäjille komennolla _chmod ugo+x /home/miika/python/moikkaus.py_. Kopioin sudona ohjelman "moikkaus.py" polkuun, josta kaikki käyttäjät voivat ajaa sen _sudo cp moikkaus.py /usr/local/bin/_. Ohjelman suoritus onnistui käyttöoikeuksien puitteissa, mutta herjasi jotain syntax-erroria. Tarkistin tiedoston, ja en nyt äkkiseltään huomannut, missä vika. Ohjelma kuitenkin toimii tehtävänannon mukaisesti, eli sitä voi nyt käyttää kaikki käyttäjät, joten tähän en kiinnittänyt enempää huomiota.

<img width="657" height="240" alt="144" src="https://github.com/user-attachments/assets/ffc75517-6d59-40ed-bd8c-4182b6261db6" />
<img width="901" height="402" alt="145" src="https://github.com/user-attachments/assets/d1eb5480-cff2-4af0-8d77-58fb3bbafb1d" />




## d) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.

Otin tehtäväksi vanhan laboratioriotehtävän Karvisen sivustolta https://terokarvinen.com/2016/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-1-uusi-ops-alkusyksylla-2016/?fromSearch=arvioitava. 
Lyhyt kuvaus: 
-  Etähallinta ja tulimuuri
-  yrityksen valvontapaketin asennus
-  Kotisivut
-  Ohjelmapaketin asennus
-  Python-ohjelma

Etähallintaan valmistautuminen. Aloitin varmistamalla, että palomuuri on päällä. Etähallintaa varten tarvitsee olla portti 22 auki. Tässä tapauksessa se oli virtuaalikoneellani jo auki. Sen saa avattua komennolla _sudo allow 22/tcp_. Itse tulimuurin saa enabloitua komennolla _sudo ufw enable_. 

<img width="584" height="240" alt="141" src="https://github.com/user-attachments/assets/944010ba-980c-4314-9c1d-e6e174cfefa2" />

Asensin vielä varmuuden vuoksi SSH-paketin komennolla _sudo apt install ssh_, joka tulee olla etähallintaa varten.

<img width="840" height="286" alt="142" src="https://github.com/user-attachments/assets/b4b9d600-8568-442e-9da7-cb62c3f4a3e3" />

Yrityksen valvontapaketin asennus. Tässä kohtaa ajaessani komentoa _wget http://terokarvinen.com/qrs/terorep/pool/main/t/terorep/terorep_0.0.3_all.deb_, sain 404 vastaukseksi, joten sivustoa ei enää ole. Tämän tehtävän "valvontapakettia" ei siis löytynyt, mutta se olisi saanut ohjeistuksen mukaisesti asennettua komennoilla:

- wget http://terokarvinen.com/qrs/terorep/pool/main/t/terorep/terorep_0.0.3_all.deb
- sudo dpkg -i terorep_0.0.3_all.deb
- sudo apt-get update
- sudo apt-get -y install terowatch ssh

<img width="1068" height="503" alt="143" src="https://github.com/user-attachments/assets/8ee1df84-cf69-4d22-9053-7e067c3f8b1c" />

Tehty käyttäjät Maija Mehiläinen, Peter Ö ja Maija Maitoparta. Määritetty turvalliset salasanat käyttäjille. 

<img width="749" height="502" alt="147" src="https://github.com/user-attachments/assets/d90f8068-db2d-4994-9738-73d145fb13f0" />

Määritin käyttäjälle Peter kotisivun: konfitiedosto
 
  <img width="695" height="58" alt="149" src="https://github.com/user-attachments/assets/56d973d2-5dc0-4b4f-9b4d-7b86e578cb59" />
  
Huomasin, että olin nimennyt konfitiedoston väärin, ja siirsin tiedoston uudelle nimelle, joka tulee conf-päätteiseksi komennolla _sudo mv petero.example.org petero.example.org.conf_. Enabloitu Peterin sivun konfit ja käynnistetty apache2 uudestaan.

<img width="1062" height="230" alt="151" src="https://github.com/user-attachments/assets/e6ac997c-4725-40b2-a100-a25d8df6e80e" />

Tein sudona Peterille kotisivun Peterin kotihakemistoon.
<img width="636" height="86" alt="152" src="https://github.com/user-attachments/assets/c99b4c17-4acb-4065-97bb-16b5c2a3f5d9" />

Sivustolle peterdev.example.org en saanut yhteyttä paikallisesti.  

<img width="1089" height="850" alt="155" src="https://github.com/user-attachments/assets/ba142097-5c2e-4250-9736-d1815a94b767" />


Asennettu PHP-laajennus virtuaalikoneelle. 

<img width="1097" height="497" alt="153" src="https://github.com/user-attachments/assets/31c89a65-d964-4664-b78c-2ecdfb53c077" />

Kirjauduin testiksi Peter-käyttäjällä virtuaalikoneelleni. Tarkistin conf-tiedoston. 

<img width="718" height="276" alt="154" src="https://github.com/user-attachments/assets/e841c927-2402-4321-a47e-377f3516818d" />

Disabloin virtuaalikoneeni aiemman etusivu komennolla _sudo a2dissite sivunnimi_. Enabloin uuden Peterin kotisivun _sudo a2ensite petero.example.org.conf_  > Latasin asetukset uudestaan _sudo systemctl reload apache2_. Sivusto ei toimi, eikä näy.
<img width="1089" height="850" alt="155" src="https://github.com/user-attachments/assets/52976fd2-adfe-42b5-b4ae-f1d4c1e5d11f" />

Tarkisin komennolla _sudo apachectl configtest_ mistä ongelma voisi johtua.

<img width="1417" height="162" alt="156" src="https://github.com/user-attachments/assets/321b8ece-9109-4688-b3fe-32434e2225f6" />
Kuvassa näkyykin virhe, ettei documentrootia ole olemassa. Muokkasin konfitiedostoa, alla kuvassa tarkemmin.

<img width="1411" height="959" alt="157" src="https://github.com/user-attachments/assets/9c35033e-cdf6-46d5-bffb-d99fb7e2316f" />

Hain ongelmanselvitystä komennolla _sudo tail -f /var/log/apache2/error.log_, ja document rootista ainakin herjaa. Document root pitäisi joko luoda Peterille (tein jo aiemmin Peterille kotisivun?) tai sitten konfitiedostossa on vielä jotain pielessä document rootin osalta. Tässä kohtaa oma kuuppa oli jo sen verran pyörällä, että tämä jää nyt vielä selvitykseen.

<img width="1418" height="348" alt="158" src="https://github.com/user-attachments/assets/508ba562-5c2d-4e98-912b-f49c01522f17" />

Kokeilin asentaa iot12tools-pakettia komennolla _sudo apt install iot12tools_, mutta pakettia ei löydy. Asensin tehtävänannon ohjelman erikseen yhdellä komennolla _sudo apt install arduino gedit curl python3_.

<img width="765" height="213" alt="159" src="https://github.com/user-attachments/assets/7ab87917-196f-4f4f-832c-251ff6eca813" />

Tein Peterin kotihakemistoon Python-tiedoston heimaailma.py. Peterillä on nyt kyseinen tiedosto käytettävissä, ja muilla ei ole sinne oikeuksia. 

<img width="522" height="95" alt="161" src="https://github.com/user-attachments/assets/8b4a9cb6-4177-4852-8e5b-608a68a76e78" />

Raportin kirjoittamisen lopetin klo 15.15.

*muokattu 7.3.26.

Jatkoin ongelmanselvitystä 7.3.26 klo 15.10. 

Aloitin ongelmanratkaisun siitä, että tein kokonaan uuden sivuston toiselle käyttäjälle ja seurasin, missä kohtaa ongelma ilmenee. Tein aiemmin tässä tehtävässä luodulle käyttäjälle Maija Mehiläinen (maijame) kotisivun. Aloitin tekemällä kansion public_html käyttäjän kotihakemistoon. 

<img width="633" height="161" alt="image" src="https://github.com/user-attachments/assets/4bc1c487-3f15-4b0d-9078-c4e970954584" />

Tämän jälkeen ajoin komennon sudo chmod ugo+x /home/maijame/, jolla Apache saa suoritusoikeuden ajaa Maijan kotisivua. Loin käyttäjälle (maijame) konfiguraatiotiedoston sivustoa varten.

<img width="958" height="445" alt="image" src="https://github.com/user-attachments/assets/019bfe29-3f00-433d-b7a6-b89948a5accf" />

Enabloitu uusi sivusto ja potkaistu Apachea. 

<img width="701" height="189" alt="image" src="https://github.com/user-attachments/assets/82f6b8d6-2f41-43e2-bbc8-ebc260918c9c" />

Tein Maijalle yksinkertaisen kotisivun.

<img width="1761" height="96" alt="image" src="https://github.com/user-attachments/assets/54741cdd-5ec5-43cb-aabc-b7780ea3aea4" />

Testatessa Maijan sivustoa local hostilla virtuaalikoneen selaimesta, tuli virhe, ettei sivustoo saa yhteyttä (sama kuin yllä). Selvitin webistä usean käyttäjän luomisen asiaa samalle local hostille Ask Ubuntun sivustolta. Ongelma oli DNS:ssä, jonka tulee näin ilman oikeaa DNS:ää osoittaa tietenkin palvelimeen itseensä eli local hostiin (127.0.0.1). Muokkasin webistä saatujen vinkkien mukaan /etc/hosts -tiedostoa, johon lisäsin halutut "oikeat" käyttäjien web-sivujen osoitteet localhostiin. 





Maijan sivusto toimi nyt ongelmitta. UTF:t puuttuu indexistä, kuten kuvasta näkyy. Ääkköset saa toimimaan sivustolla lisäämällä index.html koodiin rivin _<meta charset="utf-8" />_.

<img width="913" height="629" alt="image" src="https://github.com/user-attachments/assets/13bd346b-c9fd-4908-a687-2a6f58b14884" />

Tein samat temput käyttäjälle Peter Ö. Kopioin Maijan konfitiedoston ja tein siitä pohjan Peterin konfeille. Tämä tapahtui komennolla _sudo cp /etc/apache2/sites-available/maijame.example.conf /etc/apache2/sites-available/peterdev.example.conf_. Muokkasin tiedoston osoittamaan Peterin document rootiin.

<img width="1558" height="95" alt="image" src="https://github.com/user-attachments/assets/46e53b6e-fbfa-4510-bf9e-c73d5e1b7a12" />

<img width="979" height="348" alt="image" src="https://github.com/user-attachments/assets/767ff46b-f965-4a05-87f8-95a8b3d943c0" />

Tein Peterille etusivun.

<img width="1198" height="140" alt="image" src="https://github.com/user-attachments/assets/a783db59-0d00-42f5-b3c7-7ed0608e1d21" />

Enabloitu Peterin sivusto.

<img width="706" height="180" alt="image" src="https://github.com/user-attachments/assets/5d4b452f-d5a6-4b8e-b9ba-95c2b9cf0368" />

Nyt myös Peter Ö:n omat sivut toimivat ongelmitta.

<img width="473" height="348" alt="174" src="https://github.com/user-attachments/assets/81d47f41-ce29-40eb-8952-210fa095bd53" />

 



## Muokkaukset
7.3.26 Ratkaistu tehtävän d) ongelma.

## Lähteet

- Karvinen Tero. Perusrakenteita ohjelmointikielistä. Luettavissa: https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/
- Karvinen. Tehtävänanto. Luettavissa: https://terokarvinen.com/linux-palvelimet/#h7-maalisuora
- Karvinen. Vanha arvioitava labratehtävä. Luettavissa: https://terokarvinen.com/2016/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-1-uusi-ops-alkusyksylla-2016/?fromSearch=arvioitava
- PHP asennus. Luettavissa: https://www.php.net/manual/en/install.unix.debian.php
  
## Tekijätiedot
- Miika Vänttinen, Haaga-Helia Ammattikorkeakoulu, tietojenkäsittely
- Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
- Pohjana Tero Karvinen 2026: Linux kurssi, http://terokarvinen.com
