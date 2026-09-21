# Linux Exercises – Module 3 (Apache)

## Name-based Virtual Host

Asensin apachen komennolla apt install -y apache2, käynnistin ja laitoin sen käyttöön komennoilla systemctl start apcahe2 ja systemctl enable apache2.

Tarkistin selaimella apachen toimivuuden sekä curl http://localhost komennolla, että se näkyy myös komentokehotteen kautta.

<img width="2559" height="1439" alt="image" src="https://github.com/user-attachments/assets/2f109192-9f1f-4e64-9079-191d412939f0" />

<img width="1086" height="672" alt="image" src="https://github.com/user-attachments/assets/57e493e6-63f6-4db0-aadf-9b8a4a6154cc" />

Muutin debianin oletussivua komennolla echo ‘This is my new…’ | sudo tee /var/www/html/index.html, jolla saatiin tulokseksi alla oleva kuvakaappaus. 

<img width="641" height="322" alt="image" src="https://github.com/user-attachments/assets/c4d309ab-17a2-4934-b550-dbb609e5cb6f" />

Komennossa echo palauttaa antaman tekstin ja näyttää sen komentokehotteessa, tässä kohtaa 'This is my new...', pipe (|) ohjaa tekstin ja syöttää sen komennolle tee, tee-komento myös poistaa echo-komennon antaman tekstinpalautuksen ja samalla syöttää sen tiedostolle. Sudo antaa tarvittavat oikeudet ajaa komento, sillä /var/www/ on suojattu tavallisilta käyttäjiltä ja heillä ei ole tarvittavia oikeuksia muokata sitä.

Toinen tapa saada sama sama aikaan olisi avata itse index.html tiedosto sudo nano tai sudo vim komennolla ja kirjoittaa se itse. Kolmas olisi käyttää sudo bash -c "echo 'teksti' > .../index.html", jossa koko komento ajetaan sudo-komennon sisällä, joka onkin aasinsilta seuraavaan kohtaan, eli miksi sudo echo 'teksti' > .../index.html ei toimi, se johtuu siitä, että komento echo ajetaan korotetuilla oikeuksilla (sudo) ja ne päättyvät siihe, eli loput komennosta ajetaan ns. peruskäyttäjän oikeuksilla.

Muutin sivun localhost-osoitteesta site.local osoitteeseen menemällä /etc/hosts-tiedostoon sudo nano /etc/hosts komennolla. Asensin ufw:n komentokehotteen kautta, sekä testailin sen erilaisia toimintoja allaolevan kuvan mukaisesti. 

<img width="618" height="402" alt="image" src="https://github.com/user-attachments/assets/54016022-0855-4d64-a881-d05a50beafd7" />

Testaakseni yhteyden tietokoneestani virtuaalikoneeseen jouduin vaihtamaan asetuksista verkkosovittimen NAT muodosta bridged modeen, joka luo virtuaalikoneelle oman IP:n. 

<img width="1063" height="326" alt="image" src="https://github.com/user-attachments/assets/a9bd8c7b-52c2-4de6-b7f1-6945231a3edb" />

Ajoin tietokoneellani curl http://192.168.1.71 joka antoi tulokseksi alla olevan kuvassa olevan tuloksen.

<img width="394" height="120" alt="image" src="https://github.com/user-attachments/assets/1b1c36ed-ff30-48c0-bf88-ba99d2153c9b" />

Kun muutin sudo ufw deny 80/tcp komennolla portin suljetuksi niin saadaan alla oleva tulos. 

<img width="853" height="81" alt="image" src="https://github.com/user-attachments/assets/7eadbff1-0531-4440-bfce-e6c79a0446dc" />

Loin suoraan site1.com ja site2.com conf tiedostot ja käytin niitä varten apachen sivuilta löytyvää dokumentaatiota. 

<img width="953" height="391" alt="image" src="https://github.com/user-attachments/assets/d935b3e9-4749-4d46-9633-ad729d7abc50" />

<img width="728" height="212" alt="image" src="https://github.com/user-attachments/assets/91bc468c-f637-4f68-8fe9-e73eaeaa20bf" />

site1.com conf on samanlainen, mutta site2.com on korvattu site1.com tiedoilla.







Lähteet:

* https://httpd.apache.org/docs/current/vhosts/name-based.html Luettu 07.09.2026
* Heinonen, J. s.a. Moduuli 3 - Harjoitustehtävät. Linux-palvelimet -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Luettu 07.09.2026
