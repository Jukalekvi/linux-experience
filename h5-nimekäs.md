# Nimipalvelun käyttö ja domainin osto #
Päätin ostaa tähän tehtävään oikean kunnon Domainin omalla nimelläni. Päädyin käyttämään Namecheap-nimistä palvelua, sillä sen kautta Domainin osto vaikutti halvimmalta vaihtoehdoista joita kävin läpi. Namecheap oli myös verkossa surffailun ja oppitunnilla saatujen tietojen mukaan turvallinen palvelu käyttää <br>  </br>
Ensin rekisteröidyin palveluun:

<img width="666" height="872" alt="image" src="https://github.com/user-attachments/assets/8aaf8d2e-7faa-45fc-b68e-c9998ab011eb" />

Samalla tavalla kuin palvelinta hankittaessa, päätin myös aktivoida tällä palveluntarjoajalla kaksivaiheisen sisäänkirjautumisen tietoturvan vuoksi: 

<img width="1179" height="349" alt="image" src="https://github.com/user-attachments/assets/6f8431ad-4f30-4064-bb60-60f8f7732f3c" />

Päätin ostaa domainin jukkavirolainen.com ja otin sen kerralla kahdeksi vuodeksi, jotta sitä ei tarvitse olla heti uusimassa. Sain syötettyä NEWCOM649 nimisen alennuskoodin uutena palvelun käyttäjänä. Sivusto itse mainosti tätä koodia minulle ja suosittelenkin muillekin sen käyttöä jos palvelu ei ole ennestään tuttu:

<img width="1267" height="709" alt="image" src="https://github.com/user-attachments/assets/47d89314-c52c-4f19-9273-a6f883957d55" />

Jotta sain oston suoritettua, tuli minun ensin syöttää sivustolle osoitetietojeni lisäksi puhelinnumeroni ja sähköpostini. Sen jälkeen syötin pankkikorttini tiedot palveluntarjoajalle. Yritys tarjosi myös mahdollisuutta automaattilaskutukseen siten, että he ostaisivat domainin minulle uudelleen sitten kun sen käyttöoikeus olisi vanhentumassa mutta tätä ominaisuutta en halunnut käyttää.

<img width="737" height="362" alt="image" src="https://github.com/user-attachments/assets/86d67a98-9fbd-479d-a5da-e245631d20ca" />

Lopultaolinkin saanut ostettua domainin itselleni:

<img width="870" height="692" alt="image" src="https://github.com/user-attachments/assets/40a628a1-1010-4baa-a0d2-a1ed1bda1fc4" />

# Sivuston osoitteen käyttöönotto #

Kun domain oli ostettu, sen asetuksista pääsi muuttamaan domainin URL-osoitteen sitten, että alkuperäinen palvelimen IP-osoitteen käyttö ohjaakin käyttäjän jukkavirolainen.com:iin:

<img width="1127" height="154" alt="image" src="https://github.com/user-attachments/assets/3718d7df-a899-43ce-a327-4902c5092648" />

Alle kymmenen minuutin kuluttua lähes kaikki palvelimet whatsmydns.net sivustolla ilmoittivat että muutokset olivat onnistuneet:

<img width="1165" height="892" alt="image" src="https://github.com/user-attachments/assets/926de151-4ebf-4827-9bd8-93324849335d" />

Noin kahden tunnin odottelun jälkeen sivut toimivat moitteettomasti:

<img width="1723" height="309" alt="image" src="https://github.com/user-attachments/assets/a57db013-d87e-49f2-b5bc-a07e810654ee" />

## Alidomainit ##

Lopuksi lisäsin verkkosivulle kaksi uutta alidomainia tehtävänannon ohjeiden mukaisesti:

<img width="1119" height="384" alt="image" src="https://github.com/user-attachments/assets/7669e1d3-8390-4030-a7c2-a14324160c38" />

Hetken odottelun jälkeen myös nämä alidomainit toimivat moitteettomasti:

<img width="1721" height="162" alt="image" src="https://github.com/user-attachments/assets/3a5d82b5-9079-48de-affc-0ca9ae119323" />
<img width="1722" height="190" alt="image" src="https://github.com/user-attachments/assets/bfbdffe1-67e5-443a-88e6-324807765459" />

## Host & Dig ##

Kun sivusto ja domainit olivat kunnossa, lähdin kokeilemaan tehtävänannossa mainittuja komentoja. Ensin asensin host-ohjelman ``sudo apt install host`` komennolla ja lähdin sitten tutkimaan omia ja Googlen palveluita tämän komennon avulla:

<img width="788" height="230" alt="image" src="https://github.com/user-attachments/assets/f466f18e-b5df-49d4-8fce-dc0d6c3ee5b1" />

Tulokset näyttävät että jukkavirolainen.com on oikeasti IP osoitteella 80.69.173.37 ja jälkimmäinen osa kertoo että kyseinen palvelin vastaanottaa kyseisen domainin sähköpostin tietyllä prioriteetilla. Googlella puolestaan tietoa tuli hieman enemmän. Hostilla saamme selville sekä IPv4 että IPv6 osoitteet, handlen ja siihen sidottuja HTTP-palveluita. <br>
Jotta dig-komento saatiin toimimaan, täytyi asentaa isompi DNS utils paketti komennolla ``sudo apt install dnsutils``. Tämän jälkeen sain jukkavirolainen.com sivustosta huomattavasti enemmän dataa irti:

<img width="705" height="396" alt="image" src="https://github.com/user-attachments/assets/b840edda-177f-4540-b1bb-7229112791b0" />

Google.com puolestaan näytti tältä: 

<img width="719" height="392" alt="image" src="https://github.com/user-attachments/assets/4e666536-c726-4507-b69e-5fa2befc4034" />

