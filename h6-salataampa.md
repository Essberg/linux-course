# h6 Salataampa

Käyttöympäristö:

Acer Nitro V16.

Käyttöjärjestelmä Windows 11 64-bit.

Prosessori AMD Ryzen 7 8845HS

Näytönohjain Radeon 780M Graphics 3.80 GHz.

Asennettu RAM 16GB.

Virtuaalikoneena Oracle VirtualBoxiin asennettu Debian.

![416247776-3305b310-79a2-4570-827e-9cb746adb588](https://github.com/user-attachments/assets/9b08a07c-57a8-4cdb-8379-decbce15047e)

Harjoituksessa on tarkoitus hankkia TLS-sertifikaatti Let’s Encryptiltä ja testata sen toimivuus. 

Aloitetaan tiivistämällä aiheeseen liittyviä artikkeleita.

## Let’s Encrypt – How It Works

-	Let’s Encryptin ja ACME-protokollan tarkoituksena on pystyä luomaan HTTPS-serveri sekä saada se hankkimaan selainten luottama sertifikaatti automatisoidusti ilman ihmisvälikäsiä.
-	Omistajuuden todistamiseksi Let’s Encrypt luo avainparit, joiden avulla se voi identifioida käyttäjän.
-	Ennen sertifikaatin myöntämistä hakijan on todistettava hallitsevansa serveriä – Let’s Encrypt esittää erilaisia haasteita, joihin serverin on kyettävä vastaamaan oikealla tavalla (esimerkiksi kokeillaan saadaanko tiettyyn polkuun luotua tiedosto, jonka CA pystyy lataamaan). Tiedoston mukaan lisätään salainen avain, jonka Let’s Encrypt tunnistaa tiedostoa käsitellessään.
-	Haasteiden onnistumisen jälkeen julkisesta avaimesta tulee avain, jolla serverille luotua sertifikaattia voi hallinnoida.
-	Validoinnin jälkeen hakija pyytää sertifikaattia Certificate Signing Requestilla, ja mikäli Let’s Encrypt pystyy varmistamaan julkisen ja salaisen avaimen, myöntää se sivustolle sertifikaatin ja ilmoittaa sen käyttöönotosta julkisiin sertifikaattilogeihin (Certificate Transparency (TC) logs). Sama toteutuu toisin päin, kun sertifikaatti halutaan sivustolta poistaa. 

(Let’s Encrypt)

## Using an existing, running web server

-	Porttia 80 käytettäessä pitää määrittää myös –http.webroot, jonne http-01-haaste kirjoitetaan.
-	Kansion on oltava julkinen, ja legolla on oltava oikeudet kirjoittaa kansioon, jotta validointi on mahdollista suorittaa.

(Lange)

## Basic Configuration Example

Virtuaalihostissa on oltava sertifikaatin käyttöä varten vähintään seuraavat tiedot:
-	Käytetty portti: 443
-	ServerName www.esimerkki.com
-	SSLEngine on
-	SSLCertificateFile “/home/user/.../www.esimerkki.com.conf”
-	SSLCertificateKeyFile “/home/user/.../www.esimerkki.com.key”

(The Apache Software Foundation)

## a)	Sertifikaatin hankinta

2.3.2025 21:00. Harjoituksessa käytin Karvisen luentoa, sekä kurssimateriaaleja. Aloitetaan harjoitus ottamalla yhteyttä serveriin komennolla

```
$ssh essi@94.237.119.82
```
Sitten asensin uusimmat ohjelmistot ja tietoturvapäivitykset:

```
$sudo apg-get update

$sudo apt-get upgrade
```

Karvinen suositteli käyttämään lego-ohjelmaa sertifikaatin hankintaan, aloitetaan siis sen asennuksella komennolla

```
$sudo apt-get install lego
```

![image](https://github.com/user-attachments/assets/bccb6772-db4a-4d9e-9912-4dd960b35b40)

Kokeillaan ensin sertifikaatin toimimista staging- eli testipalvelimella, jotta mahdolliset virheet eivät kuluta Let’s Encryptin tarjoamia yrityskertoja. Testiserverin saa käyttöön lisämäällä lego-komennon alkuun 

```
$ --server=https://acme-staging-v02.api.letsencrypt.org/directory
```
Testaus onnistui:

![image](https://github.com/user-attachments/assets/903f6a6a-4e00-4ccd-ad25-414098098a73)

Ennen varsinaisen sertifikaatin hankintaa, poistetaan legon luoma kansio, jonka sijainti määriteltiin komennon kohdassa “—path=/home/essi/lego/”. Käytetään komentoa

```
$rm -r /home/essi/lego/
```

![image](https://github.com/user-attachments/assets/9d009492-16e6-4a5c-a68b-6bc1ce767348)

21:15 Kansion poiston jälkeen ajoin varsinaisen sertifikaatin hankintaan tarvittavan komennon:

```
$ lego --accept-tos --email=essi.karlberg@gmail.com --domains=essikarlberg.com --domains=www.essikarlberg.com
--http --http.webroot=/home/essi/publicsites/essikarlberg.com/ --path=/home/essi/lego/ -–pem run
```

Sertifikaatin hankinta onnistui:

![image](https://github.com/user-attachments/assets/fae33f09-f91e-414c-8637-90068663750b)

Seuraavaksi otetaan sertifikaatti käyttöön sivustolle luodussa Name Based Virtual Hostissa. Avataan tiedosto komennolla

```
$sudoedit /etc/apache2/sites-available/essikarlberg.com.conf
```

Lisätään sertifikaatille oikeat parametrit, eli SSLEngine päälle sekä sertifikaatin ja sertifikaattiavaimen tiedostopolut. Käytetään uutta porttia 443.

```
<VirtualHost *:443> 
ServerName essikarlberg.com 
ServerAlias www.essikarlberg.com
      SSLEngine on
      SSLCertificateFile "/home/essi/lego/certificates/essikarlberg.com.crt"
      SSLCertificateKeyFile "/home/essi/lego/certificates/essikarlberg.com.key"
      DocumentRoot /home/tero/public_sites/tero.example.com/
      <Directory /home/tero/public_sites/tero.example.com/>
              require all granted
      </Directory>
</VirtualHost>
```

![image](https://github.com/user-attachments/assets/820c88e0-7b4d-46b1-8232-15a33b64defd)

Muokkausten jälkeen kytketään Apacheen SSL-moduuli päälle:

```
$sudo a2ensite ssl
```

![image](https://github.com/user-attachments/assets/c5e30589-6f93-42c1-b837-09d10f48c615)

Tein palomuuriin tarvittavan reiän:

```
$sudo ufw allow 443/tcp
```

![image](https://github.com/user-attachments/assets/5de2f424-bb19-46be-85a9-50f3f49743a0)

Lopuksi kävin lokaalikoneella sekä puhelimella tarkastamassa, että sertifikaatti oli päällä:

![image](https://github.com/user-attachments/assets/04f5da62-0107-4212-80f1-e872a43cd4fb)
 
21:30 Sivustolle mentäessä sertifikaatti on päällä!

(Karvinen)

## b)	A-rating

21:35 Oman sivustonsa TLS:n voi testata laadunvarmistustyökalulla. Käytin itse SSLLabsin työkalua, jota Karvinen suositteli kurssimateriaaleissa. Työkalu löytyy osoitteesta  https://www.ssllabs.com/ssltest/. 

![image](https://github.com/user-attachments/assets/9847b646-c6e7-46dc-96c1-b4b126944f68)

Syötin oman sivuni osoitteen, ja painoin submit. Työkalu antoi sivulleni arvioksi A, eli parhaan tuloksen.

![image](https://github.com/user-attachments/assets/c1c744b0-75a5-4869-8657-c7f5883c56e0)

Sivustoa alaspäin selatessa saa laajemman analyysin auki. Täältä näkee muun muassa sivun nimet ja aliakset, sertifikaatin voimassaoloajan ja myöntämisajankohdan sekä sen myöntäjän. Listauksen lopussa lukee myös sertifikaattiin luottavia tahoja, kuten Mozilla, Apple ja Android.

![image](https://github.com/user-attachments/assets/273407a1-1ddf-4972-8db3-07d1738e5bb5)

Analyysistä löytyy myös mahdolliset lisäsertifikaatit, tässä tapauksessa Let’s Encryptin tarjoama Root X1.

![image](https://github.com/user-attachments/assets/8304c9b9-1a1c-446d-97b8-0531ae503480)
 
Työkalu löytää myös serverin TLS-protokollia, ja kertoo ovatko ne käytössä. Käytössä ovat vain uusimmat versiot protokollista – TLS 1.3 ja TLS 1.2.

![image](https://github.com/user-attachments/assets/01be2887-84bd-4641-8532-3df8963e16ca)

Työkalu simuloi myös virtuaalisia kädenpuristuksia serverin ja clientin välillä. Huomion kiinnittää epäonnistunut yritys simuloitaessa Chrome 49 / XP SP3:lla tehtyä puristusta. Kävin etsimässä lisätietoa hakukoneesta, ja keskustelun perusteella vaikuttaisi siltä, että Let’s Encryptillä on ollut ongelmia jo pitkään käytettäessä Chromen versiota 49 Windows XP-käyttöjärjestelmällä. XP:llä on aiemmin ollut vaikeuksia tunnistaa käytetty Root X1-sertifikaatti.

![image](https://github.com/user-attachments/assets/fd5b927c-4cf9-4830-b9f5-e4292c54c608)
 
Analyysin loppuun oli vielä koottu yhteen testin suoritusajankohta sekä siihen käytetty aika, serverin käyttöjärjestelmä sekä sen hostname.

![image](https://github.com/user-attachments/assets/c89dcc40-8466-4675-936d-38ece2f73a72)
 
(Karvinen, SSLLabs, Booni3, Let’s Encrypt, von Pentz)

## Lähteet:

Karvinen T., 2025. Linux-palvelimet, h6 Salataampa. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu 2.3.2025.

The Apache Software Foundation, 2025. Apache HTTP Server Version 2.4 [Official] Documentation: SSL/TLS Strong Encryption: How-To. Luettavissa: https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample. Luettu 2.3.2025.

Booni3, 2019. Forge/LetsEncrypt SSL error "SSL_ERROR_NO_CYPHER_OVERLAP" TLS version incompatibility? Foorumipostaus. Luettavissa: https://laracasts.com/discuss/channels/forge/forgeletsencrypt-ssl-error-ssl-error-no-cypher-overlap. Luettu 2.3.2025.

Intgr, 2015. Foorumipostaus. Luettavissa: https://community.letsencrypt.org/t/lets-encrypt-certificates-do-not-work-on-xp-in-ie8-or-chrome/2654/11. Luettu 2.3.2025.

Let’s Encrypt, 2024. How It Works. Luettavissa: https://letsencrypt.org/how-it-works/. Luettu 2.3.2025.

Lange, 2024. Obtain a Certificate. Luettavissa: https://go-acme.github.io/lego/usage/cli/obtain-a-certificate/index.html#using-an-existing-running-web-server. Luettu 2.3.2025.

SSLLabs, 2025. SSL Server Test. Testaustyökalu käytettävissä: https://www.ssllabs.com/ssltest/. Työkalua käytetty 2.3.2025.

von Pentz C., 2017. Handshake failed when using builtin TLS package: no cipher suite supported by both client and server. Foorumipostaus. Luettavissa: https://groups.google.com/g/golang-nuts/c/neu_jKq9pYk?pli=1. Luettu 2.3.2025.

