# Alkutiivistelmä #
Virtuaalisia palvelimia voidaan konfiguroida ja määrittää kahdella tavalla: Joko nimipohjaisesti tai IP:n perusteella. Nimipohjainen toimintamalli on yksinkertaisempi ja helpompi, sillä DNS ja Apache-palvelin konfiguroidaan tunnistamaan ServerName ja ServerAlias-määrityksillä. Apache käsittelee <VirtualHost> osion, joka määritetään aikaisempien konfiguraatioiden perusteella. Jos näitä ei ole, Apache käyttää automaattisesti periytyviä järjestelmäasetuksia, joten itse määritetyt konfiguraatiot ovat parempia.<br></br>
Tero Karvisen verkkosivu antaa nopeat ohjeet nimipohjaisen virtuaalihostin valitsemiseen. Tämän hyöty on se, että voimme käyttää useita verkkosivuja samalla IP-osoitteella. Ensin asennetaan Apache ja sen  jälkeen asetukset konfataan kuntoon. Tämän jälkeen normaalina käyttäjänä voidaan luoda verkkosivu, jonka asetuksia sudoeditillä muokkaamisen jälkeen sivua voidaan testata selaimessa ja kaiken pitäisi toimia.

# Apacheen tutustuminen #
Ensin päätin uudelleenkäynnistää Apachen ja tarkistaa että kaikki toimii, serveri lähti käyntiin odotetusti ilman ongelmia:

<img width="749" height="687" alt="image" src="https://github.com/user-attachments/assets/6f116dcc-b77a-4265-ba4e-9ad612ab7b4f" />

localhost vastasi myös minulle muokkaamastani index-sivusta:

<img width="783" height="192" alt="image" src="https://github.com/user-attachments/assets/f8ad5eb3-d4ae-44b8-a0f6-339198a1cb8a" />

Kun komentopäätteellä ajetaan ```sudo tail -f /var/log/apache2/access.log``` komento, saan seuraavan lopputuloksen lokitiedoissa:

<img width="1232" height="38" alt="image" src="https://github.com/user-attachments/assets/01757280-48f3-4cd7-a32d-257776ec7a70" />

## Selityksiä lokitiedoille ##
- **127.0.0.1** kertoo sivustolla vierailevan käyttäjän tietokoneen IP-osoitteen. Nyt osoitteena on localhost, koska sivun lataus on tehty omalta koneelta
- **[02/Sep/2025:20:43:41 +0300]** kertoo päivämäärän  ja kellonajan, jolloin Apache vastaanotti verkkopyynnön. +0300 on tarkentava tieto aikavyöhykkeestä
- **"GET /index.html HTTP/1.1"** on tarkentava tieto metodista, jota käytettiin. GET on HTTP-pyyntö, jolla haetaan eli pyydetään dataa verkkosivulta. /index.html kertoo miltä sivulta pyyntö tarkemmin tehtiin ja mikä resurssi oli kyysessä. HTTP/1.1 kertoo pyynnön olevan HTTP-protokollan 1.1 version mukainen
- **304 248 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"** kertoo, että palvelin vastasi HTTP-koodilla 304 (Not Modified), eli selain voi käyttää välimuistissa olevaa versiota, joten koko sivua ei lähetetty uudelleen. Vastauksen koko oli 248 tavua, referer-tieto puuttui eli sivu avattiin suoraan. Loppu näyttää, että pyyntö tehtiin Firefox-selaimella Linux-koneelta.

# Uusi verkkosivu #
Liikkeelle lähdettiin luomalla uusi tiedostorakenne ja sitten tekemällä kansioon index.html-niminen tiedosto: 

<img width="482" height="66" alt="image" src="https://github.com/user-attachments/assets/95f4f9ca-b300-43bb-a644-874c2f152ae3" />

Tiedostoon päätin sitten tehdä hyvin yksinkertaisen ja riisutun näköisen verkkosivun: 

<img width="723" height="238" alt="image" src="https://github.com/user-attachments/assets/d70d64a0-cc5d-4f9a-84a6-ff3aaa7f603e" />

Yritin tämän jälkeen päästä verkkosivulle selaimellani, mutta en onnistunut menemään sinne sillä Firefox esti käyttöni:

<img width="683" height="389" alt="image" src="https://github.com/user-attachments/assets/e0410953-e161-4a3a-9a86-05e6a6bacc6e" />

Muutin tiedostoni konfiguraatiot kuntoon:

<img width="971" height="262" alt="image" src="https://github.com/user-attachments/assets/dc82dba8-8676-454e-b20a-fd9dff401b02" />

Siitä huolimatta curleja tarkastelemalla tiedostot eivät olleet saaneet oikeuksia:

<img width="566" height="276" alt="image" src="https://github.com/user-attachments/assets/99d3332e-9ff5-4151-b332-c1e53a3833f8" />

Olen tehnyt myös seuraavat muutokset: 
```
sudo mkdir -p /var/www/hattu.example.com
sudo cp -r ~/www/hattu.example.com/* /var/www/hattu.example.com/
sudo chown -R www-data:www-data /var/www/hattu.example.com
sudo chmod -R 755 /var/www/hattu.example.com
```

<img width="636" height="154" alt="image" src="https://github.com/user-attachments/assets/cc7d8171-95d1-4df2-bdc0-c29e32c06ad4" />

<img width="738" height="215" alt="image" src="https://github.com/user-attachments/assets/9a3f3163-bd58-4a9e-971c-6892844863ab" />

## Lähteet ##
- Karvinen, Linux Palvelimet Alkusyksy 2025. Luettavissa: https://terokarvinen.com/linux-palvelimet/
- Karvinen, Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address 2018. Luettavissa: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/
- Apache, Name-based Virtual Host Support 2025. Luettavissa: https://httpd.apache.org/docs/2.4/vhosts/name-based.html
- Curl, Curl-ohjelman käyttö. Luettavissa: https://curl.se/docs/
Disabloin turhat sivustot ja enabloin muutoksiin tehdyt versiot. Hosteja tarkastellessa minulla ei ollut muita kuin nuo joita muokkasin mutta tästäkään huolimatta en saanut tehtävää eteenpäin. Jos joku keksii näihin ratkaisua, otan ehdotuksia mieluusti vastaan!
