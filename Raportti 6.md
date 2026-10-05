# Linux Exercises – Module 6 (Linux as a Development Workstation)

## Git

Löysin Gitin noreply sähköpostin asetuksista: 56021731+ikonenjoel@users.noreply.github.com

Gitin asennus onnistui sudo apt-get install git komennolla ja voimme tarkistaa, että se oikeasti on asennettu komennolla git -v:

<img width="323" height="67" alt="kuva" src="https://github.com/user-attachments/assets/218d2761-5441-486d-8607-3ace4db30926" />

Joka tulosti gitin ja sen version komentokehotteeseen.

Lisätään globaali git identiteetti seuraavilla komennoilla: 

<img width="1019" height="43" alt="kuva" src="https://github.com/user-attachments/assets/bd762926-b485-4777-8a9a-b4b950e0d41f" />

Jonka jälkeen voidaankin luoda uusi ssh avainpari: 

<img width="1168" height="28" alt="kuva" src="https://github.com/user-attachments/assets/68dbaf80-59fb-4601-b69f-142bf77a0047" />

-t ed25519 parametri kertoo, mitä algoritmia käytetään salauksessa, -C on kommenttikenttä, joka tässä tilanteessa on noreply-sähköpostini GitHubissa ja -f kertoo, mihin avain tallennetaan ja millä nimellä. Laittamalla sen -f parametrilla pystymme skippaamaan sen laittamisen promptina.

Seuraavaksi pitää luoda uusi konfiguraatiotiedosto jotta saamme ssh:n toimimaan, komennolla nano ~/.ssh/config pääsemme suoraan tekemään sitä: 

<img width="468" height="210" alt="kuva" src="https://github.com/user-attachments/assets/3b173c89-c067-40f2-b395-ad4efd126e78" />

Konfiguraatiolle pitää myös antaa oikeat oikeudet komennolla chmod 600 ~/.ssh/config. Voimme sen jälkeen käyttää cat ~/.ssh/github_key.pub joka antaa tarvittavan avaimen. Kun lisäämme avaimen githubiin saadaan seuraava näkymä, jossa nimesimme avaimen Debian VM:

<img width="1010" height="262" alt="kuva" src="https://github.com/user-attachments/assets/d65eade6-fc34-4c09-b211-9edc3d33cdcc" />

Testataan toimivuus kloonaamalla repositorio virtuaalikoneelle: 

<img width="1107" height="504" alt="kuva" src="https://github.com/user-attachments/assets/a95153c4-6213-4178-b7b9-3211ea2a6433" />

Loppuvaiheessa voidaankin lisätä tiedosto, lisätä se itse repositorioon ja puskea se gittiin: 

<img width="776" height="309" alt="kuva" src="https://github.com/user-attachments/assets/c4c83cd1-7276-4fcc-8b96-7a16879b2d17" />


## Your Development Workstation

Jos voisin rakentaa itselleni uuden työkoneen ja hankkia siihen tarvittavat oheislaitteet se olisi AMD Epyc pohjainen, tehokkaalla Nvidian näytönohjaimella ja siihen tarvittavat muistit/tallennustilat. Oheislaitteina olisi stereokuulokkeet, pöytämikki, piirtopöytä 3D-mallinnusta varten sekä laadukas hiiri ja näppäimistö. Dualboot windowsin ja linuxin välillä ja se tulisi 3D-mallinnukseen, ohjelmointiin sekä omien projektien pyörittämiseen.

