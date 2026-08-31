# Harjoitustehtävä

## 1. Basic commands

Tehtävänannossa käskettiin luoda home-hakemistoon uusia kansioita sekä teksitiedostoja alla olevan kuvan mukaisesti: <img width="889" height="289" alt="kuva" src="https://github.com/user-attachments/assets/adac493a-120f-4b26-858e-3da4e8f93d30" />

Toteutukseni: 

<img width="649" height="226" alt="kuva" src="https://github.com/user-attachments/assets/ae7f0b3e-77fe-4898-8f39-f5d4e9b51aaf" />

---

Seuraavaksi käsketään lisätä 10 eläintä ja 10 vihannesta/hedelmää tekstitiedostoon ja vaihtaa niiden nimet. 
Tein muokkaukset Nanolla ja tallensin tiedoston uudella nimellä, jonka jälkeen poistin vanhan tiedoston rm-komennolla. 

<img width="736" height="358" alt="kuva" src="https://github.com/user-attachments/assets/e3e6f366-0974-46c8-b65e-a521b62d194b" />

---

Seuraavaksi tiedostot piti varmuuskopioida /home/practice/docs kansioon joka toteutettiin cp-komennolla.

<img width="839" height="106" alt="kuva" src="https://github.com/user-attachments/assets/66e1f157-b305-419c-9767-f43e52bdcb4b" />

---

Poistin tehtävänannon mukaisesti animals.txt tiedostosta useamman rivin sekä poistin vegetables.txt tiedoston

<img width="861" height="538" alt="kuva" src="https://github.com/user-attachments/assets/033a5459-0bc1-47fe-ae18-4e79537effe4" />


<img width="874" height="545" alt="kuva" src="https://github.com/user-attachments/assets/7f9a36fc-77d5-4add-b7f2-c25f9b993fba" />


---

Viimeisenä käskettiin palauttamaan tiedostot sellaiseksi, kun ne olivat ennen muokkausta ja poistoa, tein sen kopioimalla /home/practice/docs-hakemistossa olevien tiedostojen päälle aikaisemmin tehdy varmuuskopiot. Kopioimisessa käytin *.txt, sillä tiedän, että kansiossa on vain haluamani tiedostot, joten säästän aikaa kopioimalla kaikki tekstitiedostot kansiosta.

<img width="831" height="524" alt="kuva" src="https://github.com/user-attachments/assets/ce824138-d620-493c-8880-148b13925f33" />


<img width="832" height="130" alt="kuva" src="https://github.com/user-attachments/assets/1b7106d3-bde9-403f-b0c0-f84b014a18f3" />


---

## haastekohta

Haasteena on tehdä tiedostoita yhdellä komennolla .tar-tiedosto ja sitten pienentää sen kokoa käyttäen gzippiä. Sain sen tehty komennolla tar -czf docs.tar.gz *.txt, jossa -c luo uuden arkiston, -z gzippaa sen ja -f antaa sille valitsemani nimen.


<img width="697" height="88" alt="kuva" src="https://github.com/user-attachments/assets/205946ca-3414-4343-a7e4-d82fe6445dda" />

---

Siirsin tiedostot uuteen gziptest kansioon ja käytin komentoa tar -xf niiden purkamiseen. Ohjeet miten nämä tehdään löytyivät tar --help komennolla.


<img width="721" height="78" alt="kuva" src="https://github.com/user-attachments/assets/e1e25a8d-bc23-4a34-8770-060eaa9462a1" />

## 2. Grep ja Pipe

Tehtävänannossa käsketään ajaa komento echo -e “apple\nbanana\norange\nApple pie” > fruits.txt, joka itselläni loi uuden tiedoston nimellä fruits.txt ja lisäsi siihen yhden rivin tekstiä, sillä kopioituna komento sisältää alkulainausmerkin, eikä linuxin ymmärtämää lainausmerkkiä, sen korjattuani teksti menee oikein eri riveille.

Seuraavaksi testataan grep-komentoa eri kehotteilla, jotka ovat -i, -n, -ni, -v. grep on ns. perushaku joka etsii vain ja ainoastaan "apple" sanalla kuten se on kirjoitettu, eli se ei löydä sanaa "Apple", sillä se ei ole kirjotetettu pelkillä pienillä kirjaimilla. -i taas ei välitä kirjainkoosta, eli se löytää kummatkin Apple ja Apple pie. -n näyttää linjanumerot, eli kertoo missä kohdassa tiedostoa ne ovat. -ni yhdistää aikaisemmat komennot -i ja -n. -v löytää kaiken, joka ei ole apple, mukaanlukien Apple pie, sillä se ottaa huomioon onko teksti kirjoitettu isolla kirjaimella vai ei.

Komento wc kertoo kirjainmäärän tekstissä, se lukee tekstiä ja kertoo monta riviä, sanaa ja kirjainta tiedosto sisältää.

---

Pipe (|) ottaa tulosteen vastaan ja lähettää sen eteenpäin syötteenä. Kokeilin alla olevassa kuvassa tehtävänannon mukaisia komentoja.

<img width="824" height="294" alt="kuva" src="https://github.com/user-attachments/assets/b606a358-372a-4f25-b754-584a1b1e5dba" />

cat-komento tulostaa tiedoston sisältöä komentoriville, käyttämällä "putkea" voimme antaa eteenpäin syötteen cat-komennolle. Ensimmäisessä kohdassa käytetään grep-hakua sanalla cat, toisessa kohdassa luetaan monta riviä tiedostossa on ja kolmannessa ne laitetaan aakkosjärjestykseen ja poistetaan tuplana olevat listauksesta.

### GPL-2 License

GPL-2 sisältää 338 riviä tekstiä. Sen sai selville komennolla cat GPL-2 | wc -l

Komento "grep GNU /usr/share/common-licenses/GPL-2" etsii GPL-2 lisenssistä kaikki maininnat sanasta GNU ja näyttää komentorivillä ne rivit joista se löytyy.

GPL-2 lisenssitiedosto sisältää sanan GNU 8 kertaa. 

Kaikki maininnat sanalla "license": 

<img width="821" height="518" alt="kuva" src="https://github.com/user-attachments/assets/aa5580f9-bfee-46e4-82cb-a04dce317fac" />

Jos taas halutaan löytää sana "license" ja ei välitetä millä kirjainkoolla sitä ollaan kirjoitettu voidaan käyttää parametria -i

Kokeilin komentoa "grep -l "Copyright" /usr/share/common-licenses/* | wc -l", joka etsii tiedostoja joissa on sana "Copyright" ja se etsii läpi kaikki tiedostot hakemistossa /* kohdan takia. Sen jälkeen se käyttää pipe-ominaisuutta antaakseen eteenpäin lisää parametreja jotka ovat wc -l, eli kuinka monta riviä sisältää valitun sanan.

Yhteenveto GPL-2 lisenssistä:
* Päätarkoituksen on takaa vapaus käyttää, mukata ja jakaa ohjelmistoa, sekä varmistaa, että ohjelmisto pysyy vapaana kaikille.
* Kuka tahansa saa käyttää ja suorittaa ohjelmaa mihin tahansa tarkoitukseen ilman rajoituksia tai maksuja.
* Jos muokkaat tai liität koodia osaksi toista ohjelmaa on siitä tuotettu lopputuote oltava lisensoitu samalla GPL-2-lisenssillä.
* Et saa asettaa loppukäyttäjälle ehtoja tai rajoituksia jotka supistavat GPL-2-lisenssin oikeuksia.
* Ei takuuta, ohjelmisto tarjotaan sellaiseaan ja ei sisällä takuuta toimivuudesta tai soveltuvuudesta.

### 3. btop

Asensin btop-ohjelmiston ja sain sen toimimaan. Sen binäärit löytyvät /usr/bin/btop hakemistosta. Konfiguraatiotiedostot löytyvät ./config hakemistosta. Siihen liittyviä konfiguraatioita ovat sen asetukset .conf tiedostossa sekä teeman konfiuraatiot omassa tiedostossaan.

<img width="607" height="84" alt="kuva" src="https://github.com/user-attachments/assets/06d0a1fd-5b09-417e-af5f-66209ada2793" />

---

Osittainen kuvakaappaus komennosta dpkg -L btop: 

<img width="825" height="530" alt="kuva" src="https://github.com/user-attachments/assets/3597661e-a77c-4d28-9f97-20f9f18495ff" />

Tiedostoja on yllättävän paljo, mutta suurin osa niistä on teemoihin liittyviä.

Tein tehtävänannon mukaisen varmuuskopion btop.conf tiedostosta ja lähdin muokkaamaan alkuperäistä, tehtyäni virheellisen muutoksen ohjelmisto korjasi sen itse, kun se ajettiin ja palautti oletusasetukset.

#### Kuormituksen generointi

ping -i 0.1 8.8.8.8 komennolla ei ole huomattavaa eroa btop:ssa, mutta yes > dev/null komennolla huomataan, että yksi prosessorin säie menee täydelle teholle. Kuvakaappauksen hetkellä se on säie C3. 

<img width="831" height="526" alt="kuva" src="https://github.com/user-attachments/assets/5e4bf9d2-cec4-4b3f-96aa-8d2f47040a7a" />

### 4. Oman komentokehote-applikaation asennus

Asensin nsnake-applikaation, ihan vain nostalgian vuoksi vanhoja matopelejä miettiessäni. Vaihdoin pelin asetuksia nopeammaksi

<img width="828" height="516" alt="kuva" src="https://github.com/user-attachments/assets/5d3482a8-7b85-4f32-a50a-65f94959017b" />


Lähteet: 

* Heinonen, J. s.a. Moduuli 2 - Harjoitustehtävät. Linux-palvelimet -opintojakson esitysmateriaali Moodlessa. Haaga-HElia ammattikorkeakoulu. Luettu 31.8.2026
