# Linux Exercises – Module 7 (Shell scripting basics)

## Bash Shell

Luodaan ohjeistuksen mukaisesti kopio bash.bashrc-konfiguraatiosta, jonka jälkeen siirrytään muokkaamaan alkuperäistä, jotta saadaan Hello World tulostettua komentokehotteeseen aina kun sen avaa:

<img width="723" height="60" alt="kuva" src="https://github.com/user-attachments/assets/6a0ac561-30ba-4b2d-a1da-ae39d5eed545" />

Lisäämällä echo "Hello World" tiedoston loppuun saadaan se näkymään kun uusi komentokehote avataan:

<img width="297" height="64" alt="kuva" src="https://github.com/user-attachments/assets/5a7ca5ce-926b-44a7-bd42-54d740e56404" />

Päätin luoda aliakset komennoille ls -la ja apt update/install. Niiden lisääminen onnistuu laittamalla ne .bashrc tiedostoon alias {nimi}={komento}'. 

<img width="534" height="84" alt="kuva" src="https://github.com/user-attachments/assets/b75e6639-385f-46f1-9343-a78b331acd21" />

Kummatkin komennot toimivat haluamallamme tavalla.

<img width="759" height="196" alt="kuva" src="https://github.com/user-attachments/assets/7c1c507e-ce52-4266-b4c0-45c8a4b61408" />

Muutin histsizen koon viiteen, joka johti siihen, että komentokehote muistaa enää viisi viimeisintä komentoa.

<img width="524" height="177" alt="kuva" src="https://github.com/user-attachments/assets/54dc8d5b-8b67-4758-9ee8-1259c4a9519a" />

Ja tein siitä pysyvän muuttamalla bashrc tiedostoa:

<img width="219" height="83" alt="kuva" src="https://github.com/user-attachments/assets/21ac32c3-6ccb-4612-b659-c93f8900441a" />


<img width="440" height="257" alt="kuva" src="https://github.com/user-attachments/assets/59f13f0b-4652-4a25-b40a-9a4a94e378d1" />

Ja viimeisenä luodaan uusi shell scripti:

<img width="527" height="274" alt="kuva" src="https://github.com/user-attachments/assets/789786ae-d3a2-4d7a-bfd0-67ee48ef4b90" />

Ja ajetaan se:

<img width="695" height="226" alt="kuva" src="https://github.com/user-attachments/assets/97a7f4ff-1e50-41d2-b372-3c38080ab1d7" />


Lähteet:

* Heinonen, J. s.a. Linux Exercises - Linux Exercises – Module 7 (Shell scripting basics). Linux-palvelimet -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Luettu 07.10.2026
