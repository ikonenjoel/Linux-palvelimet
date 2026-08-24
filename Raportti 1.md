# Debian-linuxin asennus Oraclen virtualboxilla

## Osio 1

### Asennusprosessi

<img width="1391" height="876" alt="kuva" src="https://github.com/user-attachments/assets/c7342586-71ae-43cf-8c5d-af555d2f0e82" />

Boottasin Debian-live ympäristöön ja käynnistin asennuksen sitä kautta, asennus sujui ilman ongelmia.

<img width="1689" height="1028" alt="kuva" src="https://github.com/user-attachments/assets/a8bb6181-7890-483f-b50c-7d67e0ea5deb" />

Asennuksen jälkeinen reboot johti kirjautumispyyntöön jossa laitettiin valittu käyttäjä ja salasana.

Asensin VirtualBox Guest Additions-ajurit ja työkalut jotka mahdollistivat mm. copy-pasten "tietokoneiden" välillä.


# What is Open Source Software and Why use OSS

## Osio 2

Avoimen lähdekoodin ohjelmistot ovat kaikkien tarkasteltavissa, kopioitavissa, mukattavissa ja edellenjaettavissa. Ne eroavat suljetuista/kaupallisista ohjelmista olemalla täysin avoimesti kehitettyjä ja jaettavia, kun taas suljetut ohjelmistot eivät jaa lähdekoodian tai anna pääsyä siihen. Freeware ohjelmistot ovat taas ilmaisia käyttää, mutta lähdekoodi on suljettu ja tekijänoikeuden haltijan hallussa.

Avoin lähdekoodi on läsnä lähes kaikessa ohjelmistokehityksessä, tutkimusten mukaan jopa 97% kaupallisista koodikannoista sisältää avoimen lähekoodin komponentteja. Niiden antamat edut ovat yhtiöille suotuisia, maksuton koodi jota he voivat muokata omiin tarpeisiin, aktiivinen kehittäjäyhteisö ja läpinäkyvyys. Avoimuudella on myös rajoitteensa, esimerkkinä haavoittuvuudet joissain avoimen lähdekoodin komponenteissa, niiden löytäminen on paljon helpompaa avoimen lähdekoodin komponenteista kuin suljetun lähdekoodin.

### Avoimen lähdekoodin vaikutus nykyaikaiseen teknologiaan ja digitaaliseen infrastruktuuriin

Avoimen lähdekoodin projektit ovat ns. selkäranka digitaaliselle infrastruktuurille, suurin osa palvelimista pyörii avoimen lähdekoodin pilviympäristössä Linuxilla, sekä Android mobiililaitteet pohjautuvat linuxiin. Pilviteknologiasta löytyy myös useita avoimen lähdekoodin projekteja jotka pyörittävät mm. tietokantoja, esimerkkinä MySQL. 
Tekoälyboomin aikana on myös lisääntynyt avoimet suuret kielimallit, esimerkkeinä Kiinalainen DeepSeek tai Amerikkalainen Facebookin luoma Llama. Niiden ja muiden tekoälypohjaisten kielimallien opettamiseen käytetään todella usein avoimen lähdekoodin työkalua nimeltä PyTorch.

Harvoin jostain suuressa käytössä olevasta avoimen lähdekoodin komponentista löytyy tietoturvauhkia, jotka voivat vaikuttaa todella suureen määrään käyttäjiä, kuten Log4j, joka antoi hakkereille täyden pääsyn laittisiin jotka pyörivät päivittämättömällä Log4j versiolla.


Lähteet: 

* Coursera Staff. 31.12.2025. What is Open Source Software and Why Use OSS? Luettavissa: https://www.coursera.org/articles/what-is-open-source-software Luettu 24.8.2026
* IBM.com. What is the Log4j vulnerability? Luettavissa: https://www.ibm.com/think/topics/log4j. Luettu 24.8.2026
