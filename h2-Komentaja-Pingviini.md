# Tiivistelmä komentorivistä #
- Komentorivi on nopea ja tehokas työkalu, jota käytetään yhä Linuxissa ja BSD:ssä sen automaation ja hallittavuuden vuoksi.
- Perusliikkuminen ja tiedostonhallinta: ``pwd, ls, cd, less, nano, mkdir, mv, cp, rm`` — näillä liikutaan, muokataan ja hallitaan tiedostoja.
- Etäkäyttö SSH:n avulla: ssh avaa turvallisen etäyhteyden ja scp siirtää tiedostoja palvelimelle.
- Apua ja tehokkuutta: ``man, --help``, komentohistoria (``history, ctrl-R``) ja sarkain-täydennys nopeuttavat työskentelyä.
- Hakemistorakenne ja oikeudet: tärkeimmät kansiot ovat ``/, /home/, /etc/, /var/log/``; järjestelmän ylläpitotoimet vaativat sudo-oikeudet.
- Ohjelmien hallinta: ohjelmat asennetaan ja poistetaan komennolla ``apt-get``; päivitys tehdään komennolla ``sudo apt-get update``.
# Micro-editori #
Lähdin liikkeelle tässä tehtäväkokonaisuudessa ohjeidenmukaisesti sillä että asensin micron:

<img width="935" height="573" alt="image" src="https://github.com/user-attachments/assets/2d66b93e-b90b-4dc1-946f-087045f34cfb" />

Päätinkin sitten tallentaa yksinkertaisen echo-komennon kaikutesti nimisenä tiedostona järjestelmääni testatakseni miten micro-editori toimii:

<img width="1249" height="222" alt="image" src="https://github.com/user-attachments/assets/20a83e4b-2393-4b3c-9999-339a90734acd" />

# Kolme ohjelmaa #
Ensimmäisenä kolmesta ohjelmasta päätin asentaa viimeksi hampaankoloon jääneen cowsay ohjelman: 

<img width="417" height="242" alt="image" src="https://github.com/user-attachments/assets/930c1ba0-9dea-4306-8201-ff677d68dad7" />

Ohjelma asentui puhtaasti komennolla ``` sudo apt install cowsay ```

Toisena ohjelmana komentorivillä päätin asentaa fzf-ohjelman: https://github.com/junegunn/fzf
 ``` sudo apt install fzf ```

Asennuksen jälkeen ajoin ohjelman käyntiin kirjoittamalla fzf komentorivillä. Tämä kyseinen ohjelma muun muassa helpottaa tiedostojen hakemista tiedostoa etsimällä ja näyttää missä tiedostorakenteissa kohde on. Tässä esimerkki ohjelman käytöstä kun etsin sillä aikaisemmin luomaani kaikutesti-tiedostoa:

 <img width="821" height="245" alt="image" src="https://github.com/user-attachments/assets/e1295fd7-8b32-4fee-9ef5-c3949e6bda3a" />
 
Viimeisenä ohjelmana päätin ladata tmux nimisen ohjelman, joka mahdollistaa terminaalin pilkkomisen useisiin osiin yhden ikkunan sisällä. Myös tämä tapahtui perinteisellä install-komennolla. Get-komennon avulla nämä kolme listattua ohjelmaa olisi tietysti voinut asentaa samanaikaisesti kirjoittamalla ohjelmien nimet välilyöntien kera komentosarjaan.

<img width="818" height="551" alt="image" src="https://github.com/user-attachments/assets/0dfc4511-cc58-4c78-8fb5-6445410931b2" />

# FHS #
## / ##
Linuxin koko tiedostorakenne eli kaikki virtuaalisessa käyttöjärjestelmässäni on tämän ``/`` hakemiston sisällä:

<img width="414" height="394" alt="image" src="https://github.com/user-attachments/assets/c3e5502b-82a2-4063-bd4e-53203f5122fc" />

## /home & /home/jukka ##
Kotikansio /home sisältää kaikkien käyttäjien omat kansiot. Minulla tällä hetkellä tiedostorakenteessa vain yksi käyttäjä:

<img width="257" height="72" alt="image" src="https://github.com/user-attachments/assets/71ef5f28-9982-4add-9e83-29632c153414" />

/home/jukka sisältää käyttöjärjestelmän käyttäjän jukka kaikki tiedostot ja toimii kyseisen käyttäjän kotihakemistona. Tämä on ainoa paikka järjestelmässä, jonne jukka voi tallentaa dataa ilman erillisiä oikeuksia:

<img width="295" height="200" alt="image" src="https://github.com/user-attachments/assets/2c028c0e-e50e-496e-bd5b-695be89c9a45" />

## /etc, /media & /var/log ##

Etc-kansio sisältää paljon tärkeitä asioita, kuten käyttäjätilien perustiedot, salasanat, DNS-palvelinten määritykset ja shellin asetukset. Kun ajan ``` tree /etc/ -L 1 ``` komennon komentorivissä, saan 125 hakemistoa ja 94 tiedostoa lopputulokseksi.

/media/ puolestaan toimii liitospisteenä eli mount pointina kaikille irrotettaville medioille kuten muistitikuille ja kovalevyille: 

<img width="641" height="197" alt="image" src="https://github.com/user-attachments/assets/a3b1aa85-c6be-40bd-aec5-ac65d7106fcb" />

/var/log/ on myös todella tärkeä kansio, sillä se pitää sisällään kaikki järjestelmän ja sovellusten lokitiedostot. Sieltä on mahdollista toisinsanoen tarkastella koneen käyttöhistoriaa ja mitä on tehty tai esimerkiksi asennettu milloinkin:

<img width="679" height="670" alt="image" src="https://github.com/user-attachments/assets/f2eb049b-0cef-4a57-94ca-5bce9dd5e009" />

## Grep ja | ##
Grepin avulla asioiden etsiminen helpottuu Linuxissa huomattavasti, kun sitä oppii käyttämään. Alla oleva komento etsii käyttäjän jukka tietueen käyttäjätiedostoista:

<img width="748" height="48" alt="image" src="https://github.com/user-attachments/assets/e2759339-a50b-4e8e-8c4a-9ffec5c69e51" />

i-kirjaimen avulla komentoa saadaan muutettua niin, että grep etsii kaikki rivit, joissa esiintyy bash (kirjainkoolla ei ole väliä) :

<img width="731" height="72" alt="image" src="https://github.com/user-attachments/assets/1fc654ed-45c7-495d-ac46-ccc5a15db27a" />

Grepin voi myös yhdistää putkeen |. Alla olevassa esimerkissä ``` ps aux ``` listaa kaikki käynnissä olevat prosessit ja ``` grep ssh ``` suodattaa tuloksista vain ne rivit, joissa esiintyy ssh (esim. sshd-palvelin tai ssh-asiakas). Putki mahdollistaa näiden kahden komennon yhteistuloksen:

<img width="1255" height="95" alt="image" src="https://github.com/user-attachments/assets/4cda87eb-a397-42af-9980-0da9b15c2330" />

# Koneen rauta #
Viimeisenä osana viikon tehtäviä asensin tietokoneen "fyysisiä" komponentteja tarkastelevan ohjelman ja suoritin sen. Komentokehote näytti koneeni sisällön:

<img width="668" height="663" alt="image" src="https://github.com/user-attachments/assets/a9bb01a4-58e9-4103-8343-c416db790baa" />

# Lähteet #
- Karvinen, Linux Palvelimet Alkusyksy 2025. Luettavissa: https://terokarvinen.com/linux-palvelimet/
- Karvinen, Command Line Basics Revisited 2020. Luettavissa: https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited
- Micro, Micro editori 2025. Luettavissa: https://github.com/zyedidia/micro#installation
- Fzf, Commandline finder 2025. Luettavissa: https://github.com/junegunn/fzf
- Gnu org, Grep 2025. Luettavissa: https://www.gnu.org/software/grep/manual/grep.html
