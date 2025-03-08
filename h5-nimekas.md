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


## Raportin loppuosa on tehty 1.-2.3. sekä 8.3.2025.

1.3. 20:15. Viikon luennolla käytiin kotitehtävää läpi, ja sain sieltä paljon vinkkejä tähän tehtävään. Päätin ottaa kokonaan uuden serverin käyttöön, sillä pelkäsin tekemieni SSH-avainten muutoksien vaikeuttavan tehtäviä. Lisäksi ajattelin, ettei serverin vuokraamisen ja alkuasetuksien teon kertaus tekisi pahaa. Kävin siis vuokraamassa uuden serverin UpCloudilta ja valmistelin sen asetuksineen käyttöä varten. Seurasin tässä omaa edellistä raporttiani muistin virkistämiseksi.

Serverin vuokrauksen jälkeen kävin vielä ohjaamassa vuokraamani nimen essikarlberg.com uuteen, juuri vuokratun palvelimen IP-osoitteeseen NameCheapin sivujen kautta. Tämä oli helppo tehdä korvaamalla aiemmin luodut A-recordit uudella IP-osoitteella.

(Essberg, Karvinen)

## b) Based

Tässä vielä tiivistettynä toimet, jotka tehtävässä ennen ongelmien alkamista kerkesin tehdä:

 -	Otetaan palvelimeen yhteys, päivitetään ohjelmat:
  
```
$ssh essi@94.237.119.82
$sudo apt-get update
$sudo apt-get upgrade
```

 -	Ensin loin uuden Name Based Virtual Hostin essikarlberg.comille oikeilla tiedoilla:

![image](https://github.com/user-attachments/assets/94b3b1f6-d092-4d6d-8daa-467aff8a2511)

 -	Luodaan sivustolle kansio komennolla
  
```
$ mkdir -p /home/essi/publicsites/essikarlberg.com/
```

 -	Loin uuden index.html-tiedoston peruskäyttäjänä:

```
$nano index.html
```

 -	Laitetaan sivusto päälle

```
$sudo a2ensite essikarlberg.com.conf
```

 -	Potkaistaan demonia

```
$sudo systemctl restart apache2
```

Tähän asti olin edellisellä kerralla päässyt, ja tälläkään kertaa ei etusivu näkynyt oikein. Tarkastelin syytä Apache2:n error-logeista komennolla

```
$sudo tail -f /var/log/apache2/error.log
```

![image](https://github.com/user-attachments/assets/71cf7b6d-3743-45e8-b122-304b2873eb50)
 
2.3.2025 15:25. Karvinen kertoi kurssin luennolla, että käyttäjälle other pitää antaa suoritusoikeudet (x) kansioon, jossa sivusto sijaitsee sekä lukuoikeus (r) html-tiedostoon. Annetaan oikeudet komennoilla

```
$chmod o+x /home/essi/publicsites/
$chmod o+x /home/essi/publicsites/essikarlberg.com
$chmod o+r /home/essi/publicsites/essikarlberg.com/index.html
```


![image](https://github.com/user-attachments/assets/93cdc524-795a-4854-bee2-9fb2ad0da845)

![image](https://github.com/user-attachments/assets/17260f09-7460-4ca5-b26c-f5759767ed59)

![image](https://github.com/user-attachments/assets/4d34e5b2-a04d-4742-8a93-c8937ade23de)

Testataan toimivuutta curlilla:

```
$curl 94.237.119.82
```

![image](https://github.com/user-attachments/assets/09c07f78-ae28-4b27-a649-16da2ebe9c2e)

Sain vastaukseksi testisivun, eli jotain oli vielä pielessä. Katsotaan taas Apache2:n error-logia:

![image](https://github.com/user-attachments/assets/80b6cd2f-3312-49d9-9d9e-713166dc9c34)

![image](https://github.com/user-attachments/assets/e7b6ac88-0446-408c-ab07-b8f3e22089e3)

Eli edelleen oli kyse oikeuksien puuttumisesta. Päätin googlettaa virheviestin, ja löysin Stackoverflowsta keskustelua ongelmastani. Ilmeisesti suoritusoikeudet pitää antaa myös home-kansiolle, jotta ohjelmalla on oikeus avata kohdekansio. Annetaan oikeudet:

```
$chmod o+x /home/essi/
```

Ja tarkastetaan vielä kansion käyttöoikeudet:

```
$ls -l
```

![image](https://github.com/user-attachments/assets/6d6e7045-c97c-469d-aa58-0a8ea3ff6668)

Testataan aukeaako sivu oikein nyt:
 
Ja sehän toimii!

![image](https://github.com/user-attachments/assets/8bd95e66-c937-48e9-84c3-e11137e19279)

(Karvinen, Stackoverflow)

## c) Kotisivu

Tehtävänä oli luoda lisää alasivuja peruskäyttäjänä, sekä linkittää ne toisiinsa.

16:00. Aloitetaan luomalla uudet alasivut. Navikoidaan ensin sivuston kansioon:

```
$ cd /home/essi/publicsites/essikarlberg.com/
```

Luodaan kansioon uudet tiedostot blogi.html ja projektit.html.

```
$micro blogit.html
$micro projektit.html
```

Lisätään tiedostoihin HTML-koodit, joissa eri alasivut linkitetään toisiinsa:

![image](https://github.com/user-attachments/assets/de993959-1210-4723-b5e5-a5097662be43)

![image](https://github.com/user-attachments/assets/aec12f94-2d5f-4c0e-ba69-1ab2d4c1a78a)
 
Linkityksien teon kävin katsomassa GeeksforGeeksien dokumentaatiosta, ja muuten käytin jo aiemmin opittua hyväkseni koodin luonnissa.

Lisäsin samat linkitykset myös index.html-tiedostoon, jotta sivut olisivat myös sitä kautta linkitettyinä toisiinsa.

Seuraavaksi oli aika kokeilla linkkien toimivuutta ja menin selaimella osoitteeseen essikarlberg.com. Linkitykset näkyivät, ja myös ohjasivat oikeille alasivuille:

![image](https://github.com/user-attachments/assets/4b6370f6-a721-4a21-bf51-1df6044e5442)

![image](https://github.com/user-attachments/assets/a86d436e-43be-4a1e-ace3-8c361e001c6f)

![image](https://github.com/user-attachments/assets/3d1231fe-0d4a-4069-993a-2a127adf1adc)

(GeeksforGeeks)

## d) Alidomain

16:50. Tarkoituksena on hankkia kaksi alidoimainia, sekä ohjata ne osoittaamaan sivuston etusivulle. Katsoin tähän vinkkejä Apachen documentoinnista sekä NameCheapin ohjeista.

Aloitetaan tekemällä NameCheapin domainasetuksien kautta kaksi uutta alidomainia esimerkki.essikarlberg.com sekä linuxkurssi.essikarlberg.com. Tein nämä lisäämällä sivustolle kaksi uutta A-recordia ja ohjasin ne palvelimen IP-osoitteeseen saadakseni sivun etusivun näkymään alidomaineja käytettäessä.

![image](https://github.com/user-attachments/assets/393798a2-f38c-4473-8831-6c764adc0fec)

Seuraavaksi kävin katsomassa, toimivatko sivut. Sain esiin vain testisivun molemmilla alidomainella, sillä en ollut vielä käynyt muokkaamassa sivun Name Based Virtual Host-tiedostoa.

![image](https://github.com/user-attachments/assets/29ea3f8b-cd96-4ffb-9991-068fe9d66717)

![image](https://github.com/user-attachments/assets/7ab77d18-8702-4896-8d06-24f9a89c3a24)

Seuraavaksi siis muokataan essikarlberg.com.conf tiedostoa komennolla:

```
$sudoedit /etc/apache2/sites-available/essikarlberg.com.conf
```

Apachen oman ohjeistuksen mukaisesti lisäsin alidomainien tiedot ja ohjasin ne sivuston etusivulle. Alidomainit saa ohjattua nimeämällä ne ServerName-kohdassa, ja laittamalla DocumentRootiksi etusivun tiedostopolun:

![image](https://github.com/user-attachments/assets/4c868287-97d0-486e-8696-c17247ef2162)

Tiedoston tallentamisen jälkeen laitoin sivun päälle ja käynnistin Apachen uudelleen.

```
$sudo a2ensite essikarlberg.com.conf
$sudo systemctl restart apache2
```

![image](https://github.com/user-attachments/assets/a804b4fd-b9b9-465f-a3f1-d9afc28716c4)

![image](https://github.com/user-attachments/assets/87bbced9-058a-4d25-98e3-8307856fa90b)
   
17:30 Jäljellä oli vielä alidomainien testaus, eli kirjoitin selaimeen linuxkurssi.essikarlberg.com sekä esimerkki.essikarlberg.com.

![image](https://github.com/user-attachments/assets/841b0c48-d6c4-4782-8aa1-f85d15b4c2c1)

![image](https://github.com/user-attachments/assets/aaa978e0-4802-4067-9a93-db70b8211e4c)

Molemmat alisivut ohjasivat oikein etusivulle!

(Apache Software Foundation, NameCheap)

## e) DNS-tietojen tutkiminen

8.3.2025 20:10-21:00. Tässä kohdassa on tarkoitus käyttää dig- ja host-komentoja DNS-tietojen vertailuun.

Avasin virtuaalikoneeni terminaalin, ja kokeilin komentoa

```
$dig essikarlberg.com
```

![image](https://github.com/user-attachments/assets/fc011189-8513-4aac-809e-a933c22d4052)

Se ei kuitenkaan toiminut, eli minulla ei ollut asennettuna ohjelmaa, jolla komennon voisi suorittaa. AskUbuntusta löysin postauksen, jossa neuvottiin asentamaan dnsutils-ohjelma komennolla

```
$sudo apt-get install dnsutils
```

![image](https://github.com/user-attachments/assets/2cfce5bf-7f8b-49f1-8b8d-877dcf8ad53a)

Asennuksen jälkeen ajoin dig-komennon uudestaan:

![image](https://github.com/user-attachments/assets/53fa7105-85d5-4c3c-8573-205b0321eac5)

Tehtävässä kerrottiin, ettei dig-komento näytä automaattisesti kaikkia tietueita. Luin Dig Command Manualia, jossa kerrottiin, että komento hakee automaationa vain A-tietueita. Mikäli haluaa saada kaikki tulokset näkyviin, tulee komento antaa muodossa

```
@dig essikarlberg.com any
```

![image](https://github.com/user-attachments/assets/d21c8f80-c819-4314-b4b5-b6a1ead8cf6c)

Komennolla sain enemmän tietueita näkyviin. Katsoin apua tietojen tulkintaan artikkelista Linux and Unix dig Command Examples.

Answer sectionin kentät kertovat domainin nimen, TTL-arvon, luokan (IN eli internet), haetun tietueen tyypin (A) sekä viimeisenä IP-osoitteen. NS-tietue kertoo domainin serverin nimen. Lisäksi löytyy hakuun käytetty aika (Query time), koska haku tehtiin ja kuinka suuri vastaus oli (msg size).

Tein haun myös osoitteelle google.com

```
$dig google.com any
```

sekä pienemmän yrityksen sivuille arcandia.fi

```
$dig arcandia.fi any
```

![image](https://github.com/user-attachments/assets/3d1bb92a-32a1-4e4b-b988-1ccf2e132924)

![image](https://github.com/user-attachments/assets/676fbe5f-5fd9-4b7a-a297-63dd1d6f557d)

Google.com antoi enemmän tietueita, ja vastasi pyyntöön nopeammin kuin oma sivustoni. MX-tietue kertoo email-serverien nimet ja AAAA IPv6-osoitteen. Huomasin, että sivuston IPv4-osoitteen TTL on huomattavasti pienempi kuin omani.

Arcandian sivustolla oli kolme eri IPv4-osoitetta, ja sähköpostiservereitäkin oli 5 kappaletta. Sivun vastausaika oli pienempi kuin omani, mutta suurempi kuin googlella, ja palautetun viestin koko oli hauista suurin.

Seuraavaksi kokeilin host komentoa kaikkiin kolmeen sivuun:

```
$host essikarlberg.com
$host google.com
$host arcandia.fi
```

![image](https://github.com/user-attachments/assets/31804f28-8a27-4fb4-81df-95a18982d189)

![image](https://github.com/user-attachments/assets/4dcd8b4c-0607-4b6b-bf2d-ff3cb3837509)

![image](https://github.com/user-attachments/assets/8b01d169-0e34-45d7-bad7-fe0b3543f2b9)

 
Komento tuo näkyviin domainin IPv4-osoitteita, IPv6-osoitteita sekä sähköpostiserverit. Komennolla voi hakea myös IP-osoitteen avulla domainin nimen.

(Karvinen, Oli, DiG GUI, Gite)

## Lähteet:

Tehtävänanto: Karvinen T., 2025. Linux-palvelimet, h5 Nimekäs. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu 24.2.2025.

Karvinen T., 2025. Linux-palvelimet, h4 Maailma kuulee. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu 24.2.2025.

Karvinen T., 2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/. Luettu 24.2.2025.

Karvinen, T., 2012. Short HTML5 page. Luettavissa: https://terokarvinen.com/2012/short-html5-page/. Luettu 24.2.2025.

Lehto, S., 2022. Teoriasta käytäntöön pilvipalvelimen avulla (h4). Luettavissa: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/. Luettu 24.2.2025.

UpCloud, 2024. Managing SSH-keys. Luettavissa: https://upcloud.com/resources/tutorials/managing-ssh-keys. Luettu 24.2.2025.

Päivitetyn version lisälähteet:

Apache Software Foundation, 2025. Name-based Virtual Host Support. Luettavissa: https://httpd.apache.org/docs/2.4/vhosts/name-based.html. Luettu 2.3.2025.

Essberg, 2025. H5 Nimekäs. Luettavissa: https://github.com/Essberg/linux-course/blob/main/h5-nimekas.md. Luettu 1.3.2025.

GeeksforGeeks, 2024. HTML <a> href Attribute. Luettavissa: https://www.geeksforgeeks.org/html-a-href-attribute/. Luettu 2.3.2025.

GiorgosK, 2018. Apache - Permissions are missing on a component of the path. Foorumipostaus. Luettavissa: https://stackoverflow.com/questions/25190043/apache-permissions-are-missing-on-a-component-of-the-path/. Luettu 2.3.2025.

NameCheap, 2025. How do I set up host records for a domain? Luettavissa: https://www.namecheap.com/support/knowledgebase/article.aspx/434/2237/how-do-i-set-up-host-records-for-a-domain/. Luettu 2.3.2025.

DIG GuI, 2025. Dig Command Manual. Luettavissa: https://www.diggui.com/dig-command-manual.php. Luettu 8.3.2025.

Oli, 2011. Foorumipostaus. Luettavissa: https://askubuntu.com/questions/25098/how-do-i-install-dig. Luettu 8.3.2025.

Gite, 2024. Linux and Unix dig Command Examples. Luettavissa: https://www.cyberciti.biz/faq/linux-unix-dig-command-examples-usage-syntax/. Luettu 8.3.2025.

Gite, 2024. Linux and Unix host Command Examples. Luettavissa: https://www.cyberciti.biz/faq/linux-unix-host-command-examples-usage-syntax/. Luettu 8.3.2025.

