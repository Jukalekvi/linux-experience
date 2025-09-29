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

# Sertifikaatio käyttäen Certbottia #
Käytimme tunnilla Certbottia sivustomme laadunvarmistuksen ja todistuksen luomiseen. Ohjelman käyttö vaikutti suhteellisen selkeältä, joten päätin mennä eteenpäin itse myös tällä ohjelmalla
