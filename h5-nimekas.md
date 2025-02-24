# h5 Nimekäs
Tehtävässä on tarkoitus luoda uusi name based virtual host sekä omat kotisivut. Lisäksi tarkoituksena on tehdä alidomainit ja analysoida eri sivustojen DNS-tietoja.

Käyttöympäristö:

Acer Nitro V16.

Käyttöjärjestelmä Windows 11 64-bit.

Prosessori AMD Ryzen 7 8845HS

Näytönohjain Radeon 780M Graphics 3.80 GHz.

Asennettu RAM 16GB.

Virtuaalikoneena Oracle VirtualBoxiin asennettu Debian.

![411495007-0392d1e6-da5e-4c0c-b198-5b9ffe2ec975](https://github.com/user-attachments/assets/3305b310-79a2-4570-827e-9cb746adb588)

## a) Nimi
21.2.2025 10:20-11:20 Tarkoituksena on vuokrata oma nimipalvelin. Käytin ohjeina luennolla Karvisen kertomia vinkkejä, sekä Lehdon blogipostausta muistin tukena. Päätin vuokrata nimen kurssilla suositellulta palveluntarjoajalta NameCheap, joka on (ainakin tällä hetkellä) luotettava toimija.  Valitsin domainnimen oman nimeni perusteella. Valitettavasti karlberg.com oli jo varattuna, mutta essikarlberg.com oli saatavilla ja päädyin vuokraamaan sen.

![image](https://github.com/user-attachments/assets/bf2afedd-73f6-4cc9-b0fb-b7657a506d29)

En valinnut ylimääräisiä lisäpalveluita.

![image](https://github.com/user-attachments/assets/b2c447b9-50c7-4dc9-9c0b-1e2a66e43c4d)
 
Täytettyäni vaadittavat tiedot, varmistin vielä osoitteen olevan oikein ja etten ollut valinnut mitään maksullisia lisäpalveluita.

![image](https://github.com/user-attachments/assets/f96fa6b7-d23f-416c-847e-22b751c2199e)
 
Maksoin tilauksen ja domainnimi oli onnistuneesti hankittu.

![image](https://github.com/user-attachments/assets/9bf4e529-9085-42fe-b928-60177dfa67e6)
 
Seuraavaksi ohjataan domainnimi virtuaalipalvelimelle, jonka edellisessä tehtävässä vuokrasin DigitalOceanista. Navigoidaan NameCheapin vasemman puolen valikosta kohtaan Domain List, ja siellä avataan Advanced DNS -välilehti.

![image](https://github.com/user-attachments/assets/1ce3bb70-faf5-46d6-9116-798b230c58c5)

Karvinen kertoi tunnilla, että Host Records-kohdassa olevat tietueet ovat turhia, ja poistin ne kaikki. Aloin luomaan uusia tietueita painamalla Add New Record.

![image](https://github.com/user-attachments/assets/e35d709a-9fbd-4fcd-b2bb-7560677c3323)
 
Loin uudet tietueet, lisäsin oman palvelimeni IP-osoitteen ja asetin TTL-arvoksi 5 min. TTL kertoo aikavälin, jolla palvelimella olevia tietoja haetaan ja päivitetään. Lopuksi tallensin valinnat.

![image](https://github.com/user-attachments/assets/bfba775f-a8dc-42e3-a97d-d56ef1f9e7d9)
 
Domainin essikarlberg.com pitäisi olla nyt toiminnassa, sillä olin tehnyt virtuaalipalvelimen asetukset jo aiemmassa tehtävässä. Jäljelle jää vielä sivuston testaus: navigoidaan webbiselaimella osoitteeseen essikarlberg.com. 

![image](https://github.com/user-attachments/assets/f5fb634f-e6ac-47ac-88db-712a0d3c0a81)
 
Nimi ohjaa oikealle palvelimelle, testisivu tulee näkyviin – kaikki kunnossa!

(Lehto, Karvinen)

## b) Based

24.2.2025 12:30 Tehdään uusi Name Based Virtual Host. Aloitetaan ottamalla yhteys palvelimeen virtuaalikoneen terminaalin kautta edellisessä harjoituksella luodulla käyttäjällä.

```
$ ssh essi@94.237.119.77
```

Päivitetään ohjelmat ja viimeisimmät tietoturvapäivitykset:

```
$ sudo apt-get install
$ sudo apt-get upgrade
$ sudo apt-get dist-upgrade
```

Seuraavaksi luodaan uusi Name Based Virtual Host ja lisätään tarvittavat tiedot.

```
$ sudoedit /etc/apache2/sites-available/sieni.example.com.conf
```

![image](https://github.com/user-attachments/assets/81ea4111-4fb7-46b2-a4ba-b6546421a257)
 
Laitetaan uusi sivu päälle ja potkaistaan demonia.

```
$ sudo a2ensite sieni.example.com
$ sudo systemctl restart apache2
```

(Karvinen)

## c) Kotisivu

13.00 Tehdään kotisivut. Ensin luodaan uusi index.html-sivu tavallisena käyttäjänä. Tein sivulle kansion.

```
$ mkdir -p /home/essi/publicsites/sieni.example.com/
```

Navigoidaan kansioon, ja luodaan sinne uusi index.html-sivu. Käytin sivun pohjana Karvisen lyhyttä HTML5-sivua.

```
$ nano index.html
```

![image](https://github.com/user-attachments/assets/68b018ef-0337-4ce2-a40a-68d5e1a4d754)
 
![image](https://github.com/user-attachments/assets/b55916b1-cb7b-43fe-84f0-ea4653424b70)

Tämän jälkeen testasin, toimiiko sivusto. Sivu ei päivittynyt uuteen, vaan sain edelleen aikaisemmin tehdyn sivun esiin.

![image](https://github.com/user-attachments/assets/0294280b-5e9f-4a5d-9626-8f8d88cb1a21)

13:30 Muistin, että alkuperäinen sivu pitää poistaa käytöstä, ja kävin etsimässä tiedoston ja disabloimassa sen.

![image](https://github.com/user-attachments/assets/5a3d64fc-e96b-4f7d-8658-cfb5da4d8713)

Jotain tapahtui, sillä etusivulle ei enää päässyt.

![image](https://github.com/user-attachments/assets/18be68b6-eb54-4401-9bb8-be42d4dde42d)
 
Kokeiltuani curlilla, sain tämän vastauksen:

![image](https://github.com/user-attachments/assets/95506006-65a1-4186-97ef-94f63ac4b698)

Eli kyseessä on käyttöoikeuksien puuttuminen. Lisätään oikeudet:

```
$ chmod ugo+w $HOME $HOME/publicsites/
```

![image](https://github.com/user-attachments/assets/f191555a-ef1e-4ab6-a840-372c734dc97d)

Käyttöoikeudet voi tarkastaa komennolla

```
$ ls -ld $HOME $HOME/publicsites/
```

Sain näkyviin tämän.

![image](https://github.com/user-attachments/assets/0612ca07-93e7-4fa4-85bc-f57238da7229)

Tässä vaiheessa tein kirjoitusvirheen, eli jätin rivin perään ylimääräisen hipsun. Terminaali jäi jumittamaan, ja suljin sen (tyhmästi) ruksista. Sitten sain seuraavan viestin yrittäessäni ottaa uudestaan yhteyttä serveriin:

![image](https://github.com/user-attachments/assets/b8327f4c-2229-4927-aada-1cb45161798b)
 
15:30 Minulla meni hetken aikaa, kun pohdin miten lähestyisin asiaa. Ensin kerkesin jo tehdä virtuaalikoneesta kopion, jotta voisin kokeilla aikaisemmalla kuvakkeella työskentelyä. Kuvake oli kuitenkin vanha, ja olisin joutunut tekemään paljon ylimääräistä työtä. Päädyin lisäämään uuden ssh-avaimen käyttäjälle UpCloudin ohjeiden mukaisesti. Generoin uuden ssh-avainparin.

```
$ ssh-keygen
```

Korvasin jo olemassa olevan avaimen.

![image](https://github.com/user-attachments/assets/3e0b7503-1458-4b15-a490-64694c13629f)

Navigoin kansioon ja kävin lisäämässä uuden avaimen UpCloudin kautta serverille.

![image](https://github.com/user-attachments/assets/0c6c1739-527c-4b08-987c-28343f1bfe44)

Tämänkään avulla en päässyt serveriin käsiksi.

![image](https://github.com/user-attachments/assets/fca2e294-64f6-4480-abc6-62d474af6e21)

16:15 Koska tietotekninen osaamiseni ei enää tässä vaiheessa riittänyt, ja liian itsevarmalla asenteella myöhäisessä vaiheessa aloitettu tehtävä alkoi tuntua mahdottomalta, päätin kirjoittaa tämän raportin loppuun, jotta kerkeän palauttamaan edes osan tehtävästä. Jatkan ratkaisun etsimistä. Lisään puuttuvat kohdat tähän samaan raporttiin viikon aikana.
(Karvinen, UpCloud)

## Lähteet:

Karvinen T., 2025. Linux-palvelimet, h4 Maailma kuulee. https://terokarvinen.com/linux-palvelimet/.

Karvinen T., 2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/.

Karvinen, T., 2012. Short HTML5 page. https://terokarvinen.com/2012/short-html5-page/

Lehto, S., 2022. Teoriasta käytäntöön pilvipalvelimen avulla (h4). https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/.

UpCloud, 2024. Managing SSH-keys. https://upcloud.com/resources/tutorials/managing-ssh-keys.

