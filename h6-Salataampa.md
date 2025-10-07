## Tiivistelmät ##
Let's Encrypt 2024: How It Works
- SSL/TLS-sertifikaatteja voi saada ilmaiseksi ja automaattisesti Let’s Encrypt -palvelusta.
- Domainin hallinta todistetaan DNS- tai HTTP-haasteilla (ACME-protokollan avulla).
- Sertifikaattien myöntäminen, uusiminen ja peruminen on automatisoitavissa ilman manuaalisia vaiheita.
- Sertifikaatit tallentuvat myös Certificate Transparency -lokeihin, mikä lisää luotettavuutta ja läpinäkyvyyttä.
  
The Apache Software Foundation 2025
- HTTPS otetaan käyttöön määrittämällä portti 443, sertifikaatti ja yksityinen avain Apache-konfiguraatiossa.
- Salausalgoritmien (cipher suites) valinnalla voidaan parantaa turvallisuutta, ja palvelin voi pakottaa vahvat salaukset.
- OCSP Stapling tehostaa ja nopeuttaa sertifikaattien peruutustarkistuksia.
- Apache voi vaatia asiakasvarmenteita (client certificates) tietyillä sivustoalueilla lisäturvana.
- SSL-lokitusta voidaan säätää tarkkuuden mukaan, mikä auttaa ongelmien diagnosoinnissa mutta voi lisätä kuormaa.

## Snapin asennus ##
Käytimme tunnilla Certbottia sivustomme laadunvarmistuksen ja todistuksen luomiseen. Ohjelman käyttö vaikutti suhteellisen selkeältä, joten päätin mennä eteenpäin itse myös tällä ohjelmalla. Homma lähti liikkeelle siitä, että päivitin kaikki ohjelmistot update ja upgrade-komennoilla, jonka jälkeen päätin asentaa Snapin koneelle. Tämän tein siksi, että Snap mahdollistaa Certbotin automaattisen sertifikaattien uudistamisen tasaisin väliajoin, kunhan muistan aina päivittää ohjelmistot:

<img width="686" height="424" alt="image" src="https://github.com/user-attachments/assets/332c9551-e771-446a-b959-27b3575a4e4d" />

Snapin asennuksen jälkeen virallinen dokumentaatio antoi ohjeet, että snapd täytyy asentaa vielä uudelleen snappia käyttämällä, jotta saadaan viimeisin version käyttöön:

<img width="551" height="76" alt="image" src="https://github.com/user-attachments/assets/2734d584-3af7-48bf-a494-d513c3fa9994" />

Päätin vielä testata snapin toimivuuden asentamalla ``sudo snap install hello-world`` komennolla yksinkertaisen hello-world ohjelman. Saatuani ilmoituksen *hello-world 6.4 from Canonical✓ installed* tarkisin snapin toimivuuden ja ajoin siihen asentamani hello-world ohjelman:

<img width="806" height="462" alt="image" src="https://github.com/user-attachments/assets/d6752444-8cf3-4d33-8545-bddccac8c36b" />

# Sertifikaatio käyttäen Certbottia #
Snapin asennuksen jälkeen aloin asentamaan Certbottia Snapin avulla:

<img width="562" height="54" alt="image" src="https://github.com/user-attachments/assets/06058729-3bed-45c6-b047-3257dc9befe3" />

Valmistelin Certbotin käytön vielä ennen sen ajamista:

<img width="643" height="38" alt="image" src="https://github.com/user-attachments/assets/d1d88575-509a-44b2-85e5-1d380d0beec3" />

Seuraavaksi yritin käyttää certbottia apachen yhteydessä mutta sain virheen siitä, etten spesifioinut ip-osoitteita asennuksen aikana:

<img width="763" height="306" alt="image" src="https://github.com/user-attachments/assets/d8bca488-32d1-43c2-be96-db32741be733" />

 Syötin seuraavaksi oman domainini jukkavirolainen.com asennuksen yhteydessä ja sitten sertifikaatin luonti onnistui:

 <img width="764" height="392" alt="image" src="https://github.com/user-attachments/assets/ed5c4f07-10d1-4ac4-8124-8bca9da0f903" />

# Vanhan domainin uudelleenohjaus #
 Sertifikaatin jälkeen https-osoitteella varustettu domain toimi halutusti: 
 
 <img width="1277" height="198" alt="image" src="https://github.com/user-attachments/assets/719aca32-aa54-49df-a2a2-0cd6a9e3cb51" />

 Ongelmaksi tuli nyt se, että www.jukkavirolainen.com osoitteeseen mentäessä ei automaattisesti ohjattu suojatulle s-versiolle, joten aloin korjaamaan tätä. Komennolla ``sudo nano /etc/apache2/sites-available/jukkavirolainen.conf`` avasin konffaustiedoston ja lisäsin sinne seuraavat asiat:

<img width="857" height="549" alt="image" src="https://github.com/user-attachments/assets/9f6e4939-b490-44cd-8345-e3e03e454bf7" />

Sitten aktivoin uuden sivun ja apachemoduulin:

<img width="569" height="91" alt="image" src="https://github.com/user-attachments/assets/8ea17a5d-f385-456b-a234-98c55841c083" />

Tämän jälkeen sivusto toimi lukollisesti. Sain vielä kaverin testaamaan www.jukkavirolainen.com sivustolla käymistä ja kaikki toimi moitteetta:

<img width="1603" height="124" alt="image" src="https://github.com/user-attachments/assets/8df3de5c-e5bd-4b48-812f-82006fb21a56" />

Testasin vielä SSL serveritestiä verkossa omalle domainille ja sain mielestäni tosi hyvän lopputuloksen:

<img width="1104" height="652" alt="image" src="https://github.com/user-attachments/assets/eaee47a6-331f-4484-a897-7b64f37f1070" />

# Lähteet #
- Karvinen, Linux Palvelimet Alkusyksy 2025. Luettavissa: https://terokarvinen.com/linux-palvelimet/
- Certbot, Certbot dokumentaatio 2018. Luettavissa: https://eff-certbot.readthedocs.io/en/stable/
- Let's Encrypt, How It Works 2025. Luettavissa: https://letsencrypt.org/how-it-works/
- Apache, SSL/TLS Strong Encryption: How-To 2025. Luettavissa: https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample
- Qualys inc, SSL Server Test 2025. Luettavissa: https://www.ssllabs.com/ssltest/
