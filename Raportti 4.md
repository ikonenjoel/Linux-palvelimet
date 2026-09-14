# Linux Exercises – Module 4 (Basic Configuration)

## Azure Virtual Machine

Alhaalla olevassa kuvankaappauksessa näkyy yhteys virtuaalikoneeseen SSH:n kautta, sekä salasanan vaihto.

<img width="710" height="274" alt="kuva" src="https://github.com/user-attachments/assets/ac2bdd1d-1f9d-498d-a949-1753548813d5" />

Seuraavaksi ajetaan päivitykset: 

<img width="742" height="240" alt="kuva" src="https://github.com/user-attachments/assets/a9563784-2036-4664-892c-c2b1a0255c4f" />

Tarkistetaan SSH:n status ajamalla komento sudo systemctl status ssh, jolla saadaan seuraava näkymä:

<img width="1399" height="469" alt="kuva" src="https://github.com/user-attachments/assets/05ba2462-e0af-4dbc-b30e-debab5d00aae" />

Active State ilmoittaa, että SSH on päällä ja toimii, tiedoista nähdään myös paljon resursseja se vie kohdista Main PID, Tasks ja Memory. 

## SSH key authentication

Seuraavaksi luodaan salasanaton yhdistys käyttäen key-pair tekniikkaa, se luokaan ajamalla komento "ssh-keygen -t ed25519 -C "linuxuser-auth", jolla saadaan seuraava kuva: 

<img width="718" height="446" alt="kuva" src="https://github.com/user-attachments/assets/c381696a-bfec-43b6-85dd-76492b09b995" />


-t kertoo kuvassa, mitä kryptografista tiivistettä on käytetty, joka on tässä tapauksessa ed25519. -C on kommenttikenttä, johon tässä laitoin "linuxuser-auth", jotta erotan sen muista.

Seuraavaksi siirretään lokaalilta Windows-tietokoneelta itse avain serverille ja tarkistetaan, että toimiiko se: 

<img width="1412" height="275" alt="kuva" src="https://github.com/user-attachments/assets/5f3c7538-a91e-4251-b8f3-b41d52e16e40" />

Komennolla haetaan ensin tiedosto joka annetaan (|) pipe-merkillä ja yhdistetään se seuraavan komennon syötteeksi, joka on tässä kohdassa ssh käyttämäämme virtuaalipalvelimeen. Luodaan uusi kansio ja annetaan sille oikeudet, jotka ovat tässä kohdassa 700, eli omistajalla on täydet oikeudet ja muilla ei mitään. ssh-avaimille annetaan oikeudeksi 600, koska ne eivät muuten toimi.

Kuvakaappauksesta huomataan, että kirjautuminen toimii ilman salasanaa, eli avaimet toimivat.

## Apache serverin asennus

Asennetaan apache komennolla "sudo apt install -y apache2", skipataan kysymykset -y valitsimella, joka sanoo kysymyksiin automaattisesti yes. Asentamisen jälkeen apache pitää laittaa päälle komennolla "sudo systemctl enable apache", ja sen toimivuus voidaan tarkistaa komennolla sudo systemctl status apache2. 

<img width="1418" height="485" alt="kuva" src="https://github.com/user-attachments/assets/043eb337-20ef-44d2-a76e-3b650771f5a9" />

Kuvakaappauksesta nähdään, että apache on päällä.

Muutin apachen etusivua ohjeiden mukaisesti ja nyt sivulla näkyy tämä: 

<img width="611" height="122" alt="kuva" src="https://github.com/user-attachments/assets/13f019e2-9d11-4d2d-bc20-a9175f3b6313" />

ja curl-komennolla tämä: 

<img width="422" height="44" alt="kuva" src="https://github.com/user-attachments/assets/9c7ad3bd-2171-44ac-8fe5-e45d90e8a02d" />

Luodaan ohjeiden mukaisesti uusi kansio ja annetaan siihen oikeudet:

<img width="814" height="65" alt="kuva" src="https://github.com/user-attachments/assets/3616d5f6-ce02-4c6b-94c2-ec2202148fbd" />

## ufw:n asennus ja konfigurointi

Asensin ufw:n komennolla "sudo apt install -y ufw" ja varmistin, että ssh on sallittu komennolla "sudo ufw allow 22/tcp"

<img width="445" height="81" alt="kuva" src="https://github.com/user-attachments/assets/986c0ff2-cee7-4b23-a592-4324f7dbb419" />

Sallitaan myös portit 80 ja 443: 

<img width="684" height="123" alt="kuva" src="https://github.com/user-attachments/assets/e4041cd5-b467-4666-9f3e-f7aa4f75c51c" />

## Networking

Ajetaan komento ip a jolla nähdään tietoa tietokoneen yhteyksistä, näen tietokoneen ethernet-portin IP:n, yksityisen IP:n. En näe julkista IP-osoitetta.

Seuraavaksi lähdentään analysoimaan ngrepin avulla HTTP-liikennettä

<img width="1435" height="762" alt="kuva" src="https://github.com/user-attachments/assets/8104a04c-5eac-43eb-a9e6-0766f4f9d1a0" />

Ngrepin keräämää dataa:

<img width="460" height="813" alt="kuva" src="https://github.com/user-attachments/assets/311afd36-6253-4bdb-bda3-9434760e457d" />

Alussa oleva T kertoo, että käytetään TCP-protokollaa, seuraavana on IP 10.xxx -> 20.xxx, joka kertoo mistä suunnasta data menee ja mihin, tässä kohtaa curli lähetti pyynnön virtuaalipalvelimelle. Lopussa nähdään myös käytetty portti joka on :80. Saadaan GET-pyynnöllä root-hakemisto "/" ja kerrotaan, että pyytäjä oli curl-sovellus ja sen versio.

Seuraavana HTTP palauttaa, että haku toimi, ja mitä palautetaan, joka on tässä kohtaa Apachen kautta text/html ja sen sisältö, eli <h1>This is a test</h1>. Kaikki näkyy kahdesti, koska ngrep ottaa ylös myös saman virtuaalikoneen sisällä toimivan curlin lähetyksen sekä palautuksen.

Seuraavan katsotaan SSH:n lähettämää dataa, ajetaan komento "sudo ngrep -d eth0 -W byline "" port 22".

<img width="1270" height="1314" alt="kuva" src="https://github.com/user-attachments/assets/bcaff6da-9fac-4003-867b-436ba19983bb" />

Dataa tuli paljon, oletattavasti sen takia, että olen yhdistänyt SSH:n kautta palvelimeen ja se jatkuvasti siirtää dataa komentokehotteeni ja palvelimen välillä. Näen IP:n ja oletettavasti mones pyyntö/palaututettu datapaketti se on ja oletettavasti dataa, joka on kryptattu, sillä SSH on salattu tiedonsiirtoprotokolla.

<img width="563" height="732" alt="kuva" src="https://github.com/user-attachments/assets/08520420-718e-4f53-8ffe-533dfad742bf" />


Näen tietokoneiden välillä dataa, joka lähetetään edes-takaisin, oletan, että !"#$%&... on jokin ennaltamääritetty data tai paketti, joka lähetetään testaamaan, että toimiko yhteys. ICPM on protokolla, jolla voidaan testata toimiiko yhteys, se lähettää dataa edes-takaisin avaamatta pysyvää yhteyttä ja sillä voidaan lähettää virheilmoituksia, kuten pingin kohdalla "ei saatu yhteyttä".

Sen avulla on helppo tarkistaa saako johonkin tiettyyn sivuun tai ip-osoitteeseen yhteyttä. 

<img width="805" height="248" alt="kuva" src="https://github.com/user-attachments/assets/68de8ebc-fc44-4a3a-b3f8-6f8fc77f2a10" />

tcpdump näyttää antavan ajan, joka kesti mennä ip-osoitteiden välissä kun dataa lähetettiin, datan koon (length) ja jostain syystä IP-osoitteen sijaan se antoi url-osoitteen.

Lähteet: 

* Heinonen, J. s.a. Moduuli 4 - Harjoitustehtävät. Linux-palvelimet -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Luettu 14.09.2026
