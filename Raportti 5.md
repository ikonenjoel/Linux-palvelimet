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




Lähteet: 

* https://superuser.com/questions/141623/installing-dig-on-debian
