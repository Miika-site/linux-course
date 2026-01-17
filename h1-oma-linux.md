# h1 Oma Linux

## Raportin kirjoittaminen
- Raportti kirjoitetaan täsmällisesti. Mm. mitä tein, mitä tapahtui, työvaiheiden ajat ja onnistuminen/virhetilanteet.
- Raporttia kirjoitetaan samanaikaisesti, kuin tehtäviä suoritetaan
- Raportin kirjoittamisella muodostetaan samalla dokumentaatio tehdyistä toimenpiteistä, mahdollisista virhetilanteista ja niiden ratkaisuista. Raportti toimii myös ohjeistuksena, jota kenen tahansa tulisi pystyä seuraamaan ja toteuttamaan samat toimet ohjeistuksen mukaisesti.
- Raportin tulee olla helppolukuinen ja kirjoitettu käyttäen huolellista kieltä
- Raportissa tulee viitata lähteisiin, joka osoittaa, että aiheeseen on perehdytty huolellisesti
- Plagiointi, sepittäminen ja kuvien luvaton kopiointi webistä ei ole sallittua

 ## Linuxin asentaminen virtuaalikoneeseen

 Tein asennuksen omassa kotiverkossa Windows 11 OS:llä. Tarkemmat host specsit:
  - Lenovo Legion 5 15MH05H
  - OS Name:                       Microsoft Windows 11 Education
  - OS Version:                    10.0.26200 N/A Build 26200
  - System Type:                   x64-based PC
  - BIOS Version:                  LENOVO EFCN58WW, 15.11.2022
  - Total Physical Memory:         16 292 MB
  - Processor(s):                  1 Processor(s) Installed.
                               [01]: Intel64 Family 6 Model 165 Stepping 2 GenuineIntel ~2592 Mhz
  - GPU: NVIDIA GeForce RTX 2060

Tämä raportti kuvaa Oracle Virtualboxin ja Debian-käyttöjärjestelmän asennusta virtuaaliympäristöön Windows OS:lle. Lähteissä olevat ohjemateriaalit ovat osittain erinäköisiä, kuin kirjoitushetkellä 17.1.2026 suoritetut asennustoimet. Tämä raportin dokumentaatio on siis ajan tasalla kyseisillä versioilla kirjoitushetkellä. Asennukset onnistuivat ongelmitta. 

Lähdin asennustyöhön hakemalla webistä Oracle Virtualboxin asennustiedoston (https://www.virtualbox.org/wiki/Downloads). Valitsin käyttöjärjestelmäni mukaisen Windows-paketin ja uusimman verion 7.2.4, joka oli saatavilla raportin kirjoitushetkellä 17.1.2026.
Asensin VirtualBoxin onnistuneesti työasemalleni C:n juureen käyttäen oletuasetuksia. 

Kursilla tarvitsemme Linux-jakelun. Latasin sivustolta https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/ Debianin levykuvan. Versio: debian-live-13.0.0-amd64-xfce.iso.

Aloitin Debianin asentamisen avaamalla Virtualboxin ja valitsemalla "machine > new", jolla lähdetään luomaan uutta virtuaalikonetta. Nimesin koneen kuvaavasti: DebianMiika. Kiinnitetty aiemmin ladattu Debianin levykuva asetuksiin. Virtuaalikonetta määrittessä tuli ottaa pois täppä "proceed with Unattended installation", jotta OS Versioksi sai valittua 64-bittisen.

<img width="823" height="413" alt="1" src="https://github.com/user-attachments/assets/c75b5bb8-da4c-4e41-a06b-8511fd6527a3" />

Nostettu määrityksissä virtuaalikoneen suorituskykyä oletuksista seuraavasti; base memory 4096 MB, lisätty yksi CPU (yht. 2 kpl), nostettu tallennustilaa > 50 GB. Loin virtuaalikoneen näillä asetuksilla.

<img width="824" height="419" alt="2" src="https://github.com/user-attachments/assets/afbcc152-1130-476b-8d48-1be72c0628fe" />

Seuraavaksi itse Debianin asennus. Käynnistetty virtuaalikone Virtualboxista valitsemalla luotu ympäristö, klikattu hiiren kakkospainikkeella > start > start with GUI. Boot Menussa valittu "Live system (amd64)". Virtuaalikone käynnistyi nätisti ja lähes välittömästi työpöytänäkymään. Testasin koneen käyttöä, mm. nettiselainta, ja virheitä ei ilmennyt tässä kohtaa ja verkkoyhteys toimi.

Ajoin Debian Installerin virtuaalikoneen työpöydältä, jolla määrittelin OS:lle tarkemmat asetukset.

<img width="1279" height="892" alt="4" src="https://github.com/user-attachments/assets/96243f0b-5aa9-44d4-914b-d8bbcab3851b" />

Kieleksi valitsin American English, joka on suositeltava universaali kieli IT-ympäristöissä. Location eli sijainniksi valitsin Euroopan ja Zoneksi Helsingin. Näppäimistöasetukset (keyboard) määritin suomalaisittain. Malli - Generic 105-key PC, asettelu - Finnish.

<img width="1203" height="886" alt="5" src="https://github.com/user-attachments/assets/a148cdcd-b1bb-4666-bed4-c998d443011a" />

Levyn osioinnissa (partitions) valitsin "erase disk", jolloin kaikki virtuaalikoneen OS:n aiempi sälä ja ylimääräinen poistettiin ja pääsi aloittamaan ns. puhtaalta pöydältä. Tämän harjoituskoneen levy jätettiin kryptaamatta, tuotantokoneilla/oikeiden koneiden levyt tulee kryptata.

<img width="1189" height="817" alt="6" src="https://github.com/user-attachments/assets/47f025b9-9d9c-4a5b-9824-396872e4fed7" />

Määritin käyttäjän, jolle tuli koneen kaikkein vahvimmat oikeudet (sudo). Omassa nimessänikin on ääkkösiä, mutta ne eivät ole sallittuja, joten tulee käyttää ASCII-kirjaimia. Nimesin koneen tavalla, josta sitä ei voida suoraan tunnistaa (esim. verkosta), mikä kone kyseessä. Salasanaksi määritin Microsoftin yleispätevän ohjeistuksen mukaisesti vähintään 12-merkkisen tunnisteen yhdistellen erilaisia merkkejä.

<img width="1190" height="864" alt="7" src="https://github.com/user-attachments/assets/1e26a85f-12d7-4421-93c4-07e24e7d3678" />

Tarkastettu yhteenveto, joka näytti toivotun mukaiselta ja aloitin asennuksen. Määrityksissä ei mennyt muutamaa minuuttia kauempaa. Itse OS:n asennus alkoi klo 13.55 ja valmistui klo 14.01, eli kesti 6 minuuttia tällä kokoonpanolla.

<img width="1229" height="877" alt="8" src="https://github.com/user-attachments/assets/831a2728-be43-4d72-a055-29fd9a477ab9" />

Asennus onnistui. Asennuksen jälkeen käynnistin virtuaalikoneen kertaalleen uudestaan. Lopuksi testasin, että systeemi toimii, ja sehän toimi ongelmitta.

<img width="1283" height="882" alt="9" src="https://github.com/user-attachments/assets/6ae0fcb0-5457-434d-96dd-2d55e399ad5c" />

Kokonaisuudessaan näissä asennuksissa (ainakin tällä tietokonekokoonpanolla) selviää alle tuntiin levykuvan latauksineen. 


## Lähteet
  - Heinonen, Johanna. How to Install Linux to Virtualbox? Luettavissa: https://github.com/johannaheinonen/johanna-test-repo/blob/main/linux-20082025.md
  - Karvinen, Tero. Install Debian on Virtualbox. Luettavissa: https://terokarvinen.com/2021/install-debian-on-virtualbox/
  - Karvinen, Tero. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/
  - Microsoft. Vahvojen salasanojen luominen ja käyttäminen. Luettavissa: https://support.microsoft.com/fi-fi/windows/vahvojen-salasanojen-luominen-ja-k%C3%A4ytt%C3%A4minen-c5cebb49-8c53-4f5e-2bc4-fe357ca048eb
  - Virtual box asennus. Luettavissa: https://www.virtualbox.org/wiki/Downloads

## Tekijätiedot

  - Miika Vänttinen, Haaga-Helia Ammattikorkeakoulu, tietojenkäsittely
  - Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
  - Pohjana Tero Karvinen 2026: Linux kurssi, http://terokarvinen.com
