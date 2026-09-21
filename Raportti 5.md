# Linux Exercises - Module 5 (TLS Certificates)

## DNS

Dig-ohjelmiston asennus tapahtuu asentamalla dnsutils, se tehdään komennolla "sudo apt-get intsall -y dnsutils". -y on valinnainen parametri, joka automaattisesti vastaa y, eli yes kaikkiin kysymyksiin.


DNS-haku löysi virtuaalikoneen ja sen julkisen IP-osoitteen: 

<img width="1101" height="416" alt="image" src="https://github.com/user-attachments/assets/e37a6a1a-8153-4572-a600-0d524f450faf" />

TCP-dump päälle komennolla "sudo tcpdump -i eth0 port 53 -n -v" jolloin saadaan seuraava näkymä:

<img width="795" height="70" alt="image" src="https://github.com/user-attachments/assets/6cab0e80-71f4-4c2d-a86b-2da12ab9c59a" />

Vaikka ajoin DNS-haun kahdesti, ei TCP-dump löytänyt mitään:

<img width="1157" height="789" alt="image" src="https://github.com/user-attachments/assets/fa647e4b-e23a-4fce-9da2-61f644f87431" />

Syyksi oletan sen, että DNS-haku ajetaan localhostin kautta joka näkyy kuvassa kohdassa SERVER: 127.0.0.53#53(127.0.0.53) (UDP), eli haku suoritettiin loopbackin kautta, eikä eth0 portin kautta. Eroja kahdessa DNS-haussa en huomaa kuin ID:n kohdalla.

Komento dig {vm-ip} @8.8.8.8 pakottaa DNS-haun kulkemaan internettiin, eikä ohjaa sitä loopback portin kautta, joten DNS-haku suoritetaan käyttäen eth0-porttia ja se ohjataan googlen DNS-serverille joka näkyy komentokehotteessa TCP-dumpin kautta: 

<img width="904" height="83" alt="image" src="https://github.com/user-attachments/assets/aba06964-8e84-4043-8869-7c4cad170391" />


## Name-Based VirtualHost

Luodaan tarvittava käyttäjätili edituser käyttäjälle:

<img width="547" height="252" alt="image" src="https://github.com/user-attachments/assets/3a03da05-2859-4e1f-899c-1f0c9b615c29" />

Seuraavaksi luodaan sivu linuxuser käyttäjän avulla, sekä uusi tiedosto käyttäjällä linuxuser: 

<img width="1260" height="78" alt="image" src="https://github.com/user-attachments/assets/c52e03a7-7f1d-4719-9504-e68732cc4390" />

Siirrytään tekemään tiedosto käyttäjälle edituser, joka osoittautui työläämmäksi kuin oletin, sillä luvanhallinta ei ole paras taitoni: 

<img width="853" height="260" alt="image" src="https://github.com/user-attachments/assets/8350985d-149d-4361-b82b-bd6e2bf63f4b" />

Kun luvat on saatu kuntoon voi siirtyä käyttäjälle edituser ja luoda uuden tiedoston:

<img width="917" height="142" alt="image" src="https://github.com/user-attachments/assets/fd722af2-2eb1-4363-8486-2faae8fe2200" />

Ensimmäinen yritys meni pieleen, sillä kansion luvat eivät antaneet käyttäjän tehdä sinne uutta tiedostoa, sen korjattua saatiin uusi tiedosto luotua.

Seuraavaksi pitää tehdä uusi konfiguraatiotiedosto apachelle, jotta DNS-haku onnistuu ja ohjataan oikeaan IP-osoitteeseen:

<img width="1255" height="437" alt="image" src="https://github.com/user-attachments/assets/6d17319b-c74a-4182-8a01-466107504f3c" />

Ja tarkistaakseni, että ohjaus toimii oikein ja tarvittavat tiedostot on laitettu oikein voidaan kokeilla mennä niiden verkko-osoitteeseen, joka omalla kohdallani on http://tls-test015.linuxkurssi.xyz/editorfile.txt:

<img width="999" height="128" alt="image" src="https://github.com/user-attachments/assets/b307b986-60ff-46f1-8f09-9e7b23dc2cd8" />
<img width="996" height="174" alt="image" src="https://github.com/user-attachments/assets/535ff0b2-62bd-40b0-8a43-c98866e30bd9" />

Kuten kuvista huomaa on asetukset oikein ja tekstitiedosto saadaan haettua selaimen avulla, sekä etusivu toimii.

## TLS Certificate

Asennetaan certbot, jonka asennuksen olinkin tehnyt jo aikaisemmin: 

<img width="632" height="145" alt="image" src="https://github.com/user-attachments/assets/21347246-6d74-4494-ac38-39c91689e9ec" />

Jonka jälkeen huomataankin, että certbotti tarvitsee apachelle oman version, joka asennetaan pikaisesti:

<img width="1164" height="894" alt="image" src="https://github.com/user-attachments/assets/dd82b1c3-c79a-4187-808d-98498201c823" />


Seuraavassa osiossa pyydetään certbotin avulla SSL-sertifikaatti sekä päädomainille ja aladomainille. www-alkuinen on alidomain, jota ei teknisesti ottaen tarvitse, mutta se kannattaa ottaa. --apache kertoo, mitä käytetään todentamaan domaini, -d kertoo mille domainille/alidomainille haetaan sertifikaatti. Jätin asennusvaiheessa sähköpostin tyhjäksi, sillä en tarvitse päivityksiä sertifikaatin suhteen.

<img width="1260" height="608" alt="image" src="https://github.com/user-attachments/assets/ab945af4-58e3-4e2d-a14d-e44b6febc15e" />


Itse domaini, sekä sen www-alkuinen alidomaini näyttävät SSL-sertifikaatin olevan käytössä.

<img width="219" height="45" alt="image" src="https://github.com/user-attachments/assets/3162efea-a8ab-40c5-9b7a-6eb996883dfe" />

<img width="249" height="51" alt="image" src="https://github.com/user-attachments/assets/d966ab11-e2f6-43ad-a7ce-b237547dd7d6" />


Sertifikaatin uusinta voidaan testata tekemällä ns. kuivahajoitus, joka simuloi uusinnan ja varmistaa, että se toimii ilman, että itse uusinta suoritetaan. Se voidaan tehdä komennolla "sudo certbot renew --dry-run"
Voimme myös varmistaa, että uusinnasta vastaava ajastin on päällä ajamalla komento "systemctl list-timers | grep certbot". Alla olevassa kuvankaappauksessa kummatkin komennot ajettiin toimivasti ja nähdään, että SSL-sertifikaatin simuloitu uusiminen toimi, sekä certbotin ajasin on päällä.

<img width="1117" height="291" alt="image" src="https://github.com/user-attachments/assets/7f19f220-63f4-43f0-b741-0ecc9ebc4bb9" />

crt.sh ei ole tällä hetkellä toiminnassa, joten joudun käyttämään toista työkalua. Valitsin vaihtoehtoiseksi työkaluksi CertObserverin: https://certobserver.com/ct-search. Alla kuvakaappaus onnistuneesta SSL-sertifikaatin hausta CertObserver-työkalun avulla. 2 DNS SAN-sertifoitua domainia löytyi, jotka ovat itse domaini, sekä sen alidomaini www:

<img width="1436" height="517" alt="image" src="https://github.com/user-attachments/assets/66ebcd60-c424-4e2c-947b-6dee0104a05d" />


## Monitoring - curl in verbose mode

curl -v https komennon ajettuani komentokehotteeseen tulostuu seuraavat tiedot: 

<img width="1120" height="1128" alt="image" src="https://github.com/user-attachments/assets/81ed8a71-8bf8-4d4c-affd-f308e54a3ebb" />

Ylhäältä alas nähdään, että TCP (443) yhdisti HTTPS:n kautta sivulle, joka tiedetään käytetystä portista, joka on HTTPS-yhteyksissä 443, kun taas HTTP on portissa 80. Seuraavana tulee TLS kättely, jossa vaihdetaan salauksessa käytetyt avaimet ja luodaan itse salattu yhteys. Tiedon jakaminen ja lataaminen ei ala ennen kuin salaus on luotu ja palvelimen sertifikaatti on todennettu. Salauksen purkamiseen käytetään serverin kanssa vaihdettua salausavainta. Kättelyn jälkeen saadaan tietää, mitä SSL-versiota käytetään, joka on tässä tilanteessa TSLv1.3. Seuraavana nähdään sertifikaatti, sen voimaantulopäivä ja millon sen voimassaolo umpeutuu ja sertifikaatin myöntäjä, joka on Let's Encrypt. 

Lopussa saadaan itse sivun data, joka on tässä kohdassa index.html tiedoston sisältö.

curl -v http komennolla saadaan paljon suppeampi tieto:

<img width="827" height="579" alt="image" src="https://github.com/user-attachments/assets/855c8b37-0c30-4589-81f8-418b49fde194" />

Taas ylhäältä alas mennessä huomataan, että käytetäänkin porttia 80 ja suojaamatonta http-yhteyttä, TSL kättelyä ei tehdä, sillä salattua yhteyttä ei luoda. Sivu antaa virhekoodiksi 301. Nähdään myös, että http ei anna samaa dataa kuin https-versio, sillä sivu kertoo, että tiedot ovat siirretty https-sivulle. Palautettu data näyttäisi myös ohjaavan suoraan https suojatulle sivulle.

Apachen konfioguraatiosta nähdään, että portti 80 konfiguraatiotiedostossa on uudelleenohjaus https-sivulle.

<img width="973" height="412" alt="image" src="https://github.com/user-attachments/assets/37b2bb2d-e9f4-4f6a-aae2-9f2787ff9ed3" />

Jos kommentoimme uudelleenohjauksen pois päältä: 

<img width="709" height="130" alt="image" src="https://github.com/user-attachments/assets/f33043de-017b-462c-9698-07cbfe346477" />

Ja käynnistämme sen uudestaa sekä menemme curlin avulla http-sivulle uudestaan saamme datan näkyviin:

<img width="758" height="637" alt="image" src="https://github.com/user-attachments/assets/0d7915c0-6608-47f4-9871-cc4b619d1826" />

Huomataan, että uudelleenohjausta ei enää tapahdu, vaan sivu lähettää datan suojaamattoman protokollan kautta ja antaa yhteydenoton tapahtua suojaamattomasti.

## TLS - Summary

TLS luo suojatun yhteyden selaimen ja palvelimenä välille kättelyprosessilla, jossa kummatkin osapuolet jakavat todentavat itsensä digitaalisella sertifikaatilla ja luovat omat salausavaimet tiedon siirtämistä varten. Avaimen avulla data pystytään avaamaan sen saapuessa osapuolelta toiselle. Salauksen avulla varmistetaan, että pakettienkaappaus on hyödytöntä, sillä niiden avaamiseen tarvitaan kättelyprosessissa luotu avain. Suojaamattomissa yhteyksissä voidaan käyttää vaikka wireshark nimistä ohjelmaa tallentamaan dataa ja lukea sitä, peukaloida sitä, tai väärentää lähetettyä dataa matkalla man-in-the-middle-hyökkäyksellä. 

Esimerkkinä varas voisi kaapata pankkitilin kirjautumistiedot, lähettää uhrille näköissivun pankin sivuista ja kaapata käyttämättömän kertakäyttöisen tunnistekoodin, jolla pystytään tekemään yksittäinen siirto sillä varkaalla on nyt sekä kirjautumistunnus, autentikaatiotunnus sekä tarvittava kertakäyttöinen tunnus jolla itse siirron pystyy varmistamaan.

Lähteet: 

* Heinonen, J. s.a. Linux Exercises - Module 5 (TLS Certificates). Linux-palvelimet -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Luettu 21.09.2026

* MDN Web Docs 2026. 301 Moved Permanently. Mozilla. Luettavissa: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/301. Luettu: 21.9.2026.

* Super User 2026. Installing dig on Debian. Stack Exchange. Luettavissa: https://superuser.com/questions/141623/installing-dig-on-debian. Luettu: 21.9.2026.
