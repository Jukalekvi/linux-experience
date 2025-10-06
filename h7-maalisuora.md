# Hei maailma #
Viimeiseen isoon tehtäväpalautukseen olen päättänyt valita kolme kieltä, joista kahden käytöstä minulla on kokemusta ja yhden jota en ole käyttänyt aikaisemmin. Tutut kielet itselleni ovat java ja python. Tuntematon kieli on C. Valitsin tutut kielet kertauksen perusteella ja siksi että koodit näyttäisivät vähän erilaisilta. C-kieleen päädyin tuntemattoman kohdalla siksi, että se on kiehtonut minua kauan ja olen ymmärtänyt että sen potentiaali kirjoittaa nopeaa koodia on todella suuri.

## Bash ja Shellscript ##
Lähdin liikkeelle siitä, että loin kansion hello ``mkdir`` komennolla. Sinne lisäsin ensimmäiseksi bashillä tekemäni hello world ohjelman, joka toistaa vain echo-ohjelman sisällään:

<img width="824" height="517" alt="image" src="https://github.com/user-attachments/assets/55b28b8c-f425-440a-9efd-c26eeb8ce180" />

Kun bash-tiedosto oli luotu, tarkastelemalla tiedostoa huomasin, että tiedoston luominen itsessään nanolla ei sille oikeuksia suorittaa sen scriptiä. Tämän vuoksi annoin x-oikeuden ajaa scripti tälle hello.sh tiedostolle, jonka jälkeen se voitiin suorittaa. Sitten yritin ensin suorittaa scriptin kirjoittamalla tiedoston nimen mutta tajusin ohjeita luettuani, että scripti täytyy etsiä ``./``-alkuisesta polusta:

<img width="556" height="250" alt="image" src="https://github.com/user-attachments/assets/e543a26c-9565-4b0d-8a1c-873bc9434133" />

## Java ##
Kun olin saanut ensimmäisen scriptini tehtyä, päätin lähteä kokeilemaan hello worldin luomista Javan avulla. Ensin minun piti asentaa JDK eli javan kehitysympäristö ``sudo apt install default-jdk`` komennolla. Tämän jälkeen aloin muokata tiedostoa, jonka olin luonut ``nano helloworld.java`` komennolla:

<img width="818" height="515" alt="image" src="https://github.com/user-attachments/assets/ed8c420b-aac6-4afd-9b5b-2a18235c5324" />

Kun yritin mennä eteenpäin ohjelman kääntämiseen, huomasin että olinkin unohtanut ; merkin  printlinen lopusta, sillä Linux ilmoitti minulle virheellisestä syntaxista. Kävin korjaamassa tiedoston ja huomasin myös tehneeni klassisen virheen siinä, että julkisen luokkani nimi helloWorld oli eri kuin tiedostoni nimi helloworld. Kävin muuttamassa vielä luokan identtiseksi tiedoston nimen kanssa ja tämän jälkeen ajoin ``javac helloworld.java`` nimisen komennon, joka kääntää JDK:n avulla tiedoston suoritettavaan muotoon. Sen jälkeen pääsin viimein suorittamaan ohjelmani javalla. Erityishuomiona bashiin verrattuna on se, että javaa suoritettaessa tiedostopäätettä .java ei tarvita samalla tavalla kuin bashin kanssa .sh tarvitaan:

<img width="498" height="40" alt="image" src="https://github.com/user-attachments/assets/5a12ff1d-d19c-4b81-9878-b41b025a31a0" />

Huomasin myös, että kääntäjän käyttäminen ja scriptin ajaminen javalla loivat hello-kansioon minulle .class päätteisen tiedoston, jonka sisältö oli seuraavanlainen:

<img width="1163" height="512" alt="image" src="https://github.com/user-attachments/assets/ce46ea84-f963-4510-ac77-13657f0cae1d" />

## C ##

Lopulta pääsin käsiksi C-kielen opetteluun voidakseni kirjoittaa Hello Worldin. Luin 

## Lähteet ##
Karvinen, Linux palvelimet alkusyksy 2025. Luettavissa: https://terokarvinen.com/linux-palvelimet/
