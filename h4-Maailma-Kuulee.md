# Tiivistelmä Karvisen ja Lehdon dokumentaatioista #
Susanna Lehdon dokumentaatiota kurssitoteutuksesta oli mielenkiintoista lukea. Hän oli selkeästi noudattanut Karvisen antamia ohjeita ja pyrkinyt rakentamaan toimivat verkkosivut. <br>
Dokumentaatio kertoo seuraavat pääpointit:
- Ensin ostetaan oma palvelin joltakin digitaaliselta palveluntarjoajalta
- Palvelin konfataan halutuilla asetuksilla ja se asennetaan verkkoon
- Palvelimelle asennetaan palomuuri ja se aktivoidaan käyttöön
- Käyttäjätunnukset luodaan ja root suljetaan
- Apache ja kotisivut asennetaan palvelimelle. Lisäksi tehdasasetuksilla varustettu kotisivu korvataan näkymään oikeana
- Sivut testataan muilla laitteilla, jotta voidaan varmistaa niiden näkyminen ja saavutettavuus julkisesti
- On todella tärkeää huomioida tietoturva (salasanat) ja tiedostaa missä tietokoneella tekee mitäkin komentoja milloinkin
# Oman palvelimen vuokraaminen #
Päätin käyttää tässä projektissa UpCloud nimistä palveluntarjoajaa. Kyseisen yrityksen valitsin siksi, että se vaikutti tunnilla tehdyn kokeilun perusteella laadukkaalta ja helppokäyttöiseltä. Lisäksi palvelimet ovat Suomessa mikä tuo itselleni turvallisuuden tunnetta. </br>
Kirjautumisen ja tilin vahvistuksen jälkeen sain käyttööni hieman "ilmaista" kokeilurahaa kun vahvistin pankkikorttini tiedot palveluntarjoajalle. Samalla annoin myös osoitetietoni ja puhelinnumeroni palvelulle. Päätin ottaa käyttöön 2-vaiheisen tunnistuskirjautumisen tietoturvan kohottamiseksi, authenticatorapp toimi puhelimen kautta loistavasti. 
# SSH avain #
En ollut aikaisemmin käyttänyt SSH-avaimia, joten päätin luoda sellaisen tätä projektia varten, koska se on ilmeisesti todella tietoturvallinen ratkaisu:

<img width="621" height="374" alt="image" src="https://github.com/user-attachments/assets/1bbb65b0-137a-4761-8c20-b801b77d8881" />

## Palvelimen luominen ##
Fyysisen palvelimen päätin ostaa Suomesta:

<img width="585" height="555" alt="image" src="https://github.com/user-attachments/assets/fbbb97e0-0d18-40bc-88ee-06d746a0e6a9" />

Otin palvelimelle hieman enemmän kiintolevytilaa, jos tuo 1 gigaa pääsisikin loppumaan: 

<img width="592" height="525" alt="image" src="https://github.com/user-attachments/assets/25b3c835-7d7c-4a3e-9da8-6145b740fa28" />

Ostin tarjoajan verkkosivuilta itselleni halvan palvelimen ja tein sen kurssin kautta tutuksi tulleen Debianin avulla:

<img width="430" height="627" alt="image" src="https://github.com/user-attachments/assets/ddc70008-1657-4660-85f4-ada33d3ac1c1" />

Lisäsin myös julkisen SSH-avaimen, jonka olin aikaisemmin luonut, palvelimen omaksi avaimeksi: 

<img width="358" height="300" alt="image" src="https://github.com/user-attachments/assets/e614e524-a7b3-4c59-bd3f-07f349737b44" />

Hetken kuluttua palvelin oli luotuna palveluntarjoajan ympäristössä: 

<img width="829" height="338" alt="image" src="https://github.com/user-attachments/assets/4d757f4f-3ef9-4f3c-ba3e-bc9bbed0f9aa" />

## Palvelimelle kirjautuminen, palomuurin asennus ja käyttäjätunnusten konfigurointi #

Otin verkosta talteen juuri luodun palvelimeni IP osoitteen: 80.69.173.37 <br>
Yritin sitten kirjautua palvelimelle terminaalissa ja onnistuin  lisäämään oman ssh-avaimen palvelimen vastineen itselleni: 

<img width="1073" height="284" alt="image" src="https://github.com/user-attachments/assets/dcae4583-e359-4384-ba4f-fed3b8d9f748" />

Sisälle palvelimelle päästyäni asensin tulimuurin ``sudo apt-get install ufw`` komennolla, tein siihen aukon ja enabloin tulimuurin käyttöön: 

<img width="787" height="117" alt="image" src="https://github.com/user-attachments/assets/74fc522f-d331-45b5-b569-e328b6131a28" />

Loin seuraavaksi käyttäjätunnuksen omalla nimelläni, annoin sille sudo oikeudet ja tarkistin että se löytyy palvelimelta, jukka oli muodostunut tiedostoihin:

<img width="737" height="475" alt="image" src="https://github.com/user-attachments/assets/326fb838-cb30-45ef-a252-9e52c8f62b53" />

Tämän jälkeen testasin vielä toisella terminaalilla että pääsenkö sisälle palvelimelle:

<img width="588" height="79" alt="image" src="https://github.com/user-attachments/assets/6a2cf1a5-5c45-4f2b-931e-02c41f7a6c8c" />

Koska kirjautuminen epäonnistui, menin selvittämään asiaa verkosta. Päädyin ensin tarkistamaan että ssh on asennettuna palvelimelle: 

<img width="915" height="259" alt="image" src="https://github.com/user-attachments/assets/b5ef13cc-a569-4e6b-8e62-9f66b2a8f6f9" />

Lopulta päädyin luomaan palvelimen omassa terminaalissa sinne ssh-tiedostokansion käyttäjälle jukka. Lisäsin sinne tiedoston, johon tallensin julkisen ssh-avaimeni ja annoin näille oikeudet:

<img width="978" height="134" alt="image" src="https://github.com/user-attachments/assets/81c0ae7c-c39b-40fc-a68e-a238f97d3a03" />

Tajusin myös syöttäneeni vahingossa IP:n tuohon echo-alkuiseen komentoon, joten kävin sitten suorittamassa komennon uudelleen julkisella avaimella. Tämän jälkeen yritin kirjautua erillisellä terminaalilla sisään jukka-käyttäjälle palvelimella:

<img width="797" height="269" alt="image" src="https://github.com/user-attachments/assets/43554eb1-be78-4d74-8b37-a73ab01355e6" />

Aluksi palvelin ei päästänyt minua sisään, mutta syy selvisi noin 2h kaivamisen jälkeen. Kielto johtui siitä että luodessani palvelimen jukka-kotihakemistoon ssh:lle authorized_keys tiedostoa, liitin tiedostoon vahingossa virheellisesti aluksi vain pitkän merkkijonon koko homman keskeltä (värjättynä kuvassa):

<img width="994" height="38" alt="image" src="https://github.com/user-attachments/assets/377cd12d-d647-4e57-8580-34d6b7b8d097" />

Kun liitin kaiken muunkin, pääsin sisälle toisesta terminaalista ja minun oli mahdollista jatkaa eteenpäin. Viimeisenä vaiheena käyttäjätunnuksissa oli rootin sulkeminen:

<img width="817" height="511" alt="image" src="https://github.com/user-attachments/assets/703bce12-a2ac-46ca-b1df-b7f306778309" />

Lopuksi käytin komentoa ``sudo service ssh restart`` jolla käynnistin ssh:n uudelleen ja sitten päivitin paketit ``sudo apt-get update`` ja ``sudo apt-get upgrade`` komennoilla

# Apache ja verkkosivujen viimeistely #

Seuraavaksi asensin apachen ``sudo apt install apache2`` komennolla ja tein palomuuriin reiän komennolla ``sudo ufw allow 80/tcp``. Päätin sitten testata verkkosivujen toimimista ja nehän näkyivätkin kauniisti oman tietokoneeni avulla: 

<img width="1287" height="996" alt="image" src="https://github.com/user-attachments/assets/3fea71f1-54bf-44e1-8b6d-b5bf20745267" />

Tein sitten vielä ``sudo nano /var/www/html/index.html`` komennon avulla seuraavanlaisen muokkauksen verkkosivuihini:

<img width="914" height="507" alt="image" src="https://github.com/user-attachments/assets/8117d664-ddf8-4981-9121-83c9b1f479f0" />

Testasin sivujen toimivuuden vielä omalla puhelimellani, pöytäkoneellani ja lähetin verkko-osoitteen kaverilleni, joka varmisti että sivut toimivat. Nyt minulla on toimiva palvelin!

<img width="1717" height="246" alt="image" src="https://github.com/user-attachments/assets/ef660c6d-5129-4bb9-adf9-24fc7e88693d" />

# Lähteet #
- Karvinen, Linux Palvelimet Alkusyksy 2025. Luettavissa: https://terokarvinen.com/linux-palvelimet/
- Lehto, Teoriasta käytäntöön pilvipalvelimen avulla (h4) 2022. Luettavissa: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
- Karvinen, First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS 2017. Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Upcloud, Upcloud palvelinympäristö 2025. Luettavissa: https://upcloud.com/
