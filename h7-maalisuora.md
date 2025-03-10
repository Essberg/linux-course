# h7 Maalisuora

Harjoituksessa käytetty kone:


Käyttöjärjestelmä Windows 11 64-bit.

Acer Nitro V16.

Prosessori AMD Ryzen 7 8845HS

Näytönohjain Radeon 780M Graphics  3.80 GHz.

Asennettu RAM 16GB.

Virtuaalikoneena Oracle VirtualBoxiin asennettu Debian.

![image](https://github.com/user-attachments/assets/b9d2e553-3f33-439b-ba10-d235ce528850)
 
Kurssin viimeisessä harjoituksessa tutustutaan shell scriptaukseen sekä muutamaan eri ohjelmointikieleen, ja tehdään omavalintainen laboratoriotehtävä kurssin menneiltä toteutuksilta. Lisäksi parantelin jo tekemiäni raportteja, ja asensin uuden virtuaalikoneen viimeisen tunnin tehtävää varten.

## Tehtävät a) ja c) 

A-kohdassa tehtävänä on ajaa ”Hei maailma” kolmella eri kielellä ja C-kohdassa tehdä oma uusi komento, jota kaikki käyttäjät voivat ajaa. Laitoin nämä tehtävät saman otsakkeen alle, sillä oli luontevaa tehdä ne peräkkäin.

## a) Hei maailma

9.3.2025 11:00. Aloitetaan päivittämällä virtuaalikoneen ohjelmistot ja tietoturvapäivitykset, jonka jälkeen hain ohjelmointikielien paketit Karvisen ohjeen mukaisesti:

```
$sudo apt-get update
$sudo apt-get dist-upgrade
$sudo apt-get install python3 gcc g++ openjdk-17-jdk golang-go ruby lua5.4
```

![image](https://github.com/user-attachments/assets/81a4faab-40f4-433b-b3ba-a56b666453b9)

Hetken odottelun jälkeen oli aika tehdä ensimmäinen komento. Valitsin kieliksi Python3:n, Rubyn sekä Luan.
Ohjeet kielien syntaxiin katsottu Karvisen artikkelista Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04. Käytin myös Karvisen Shell Scripting-artikkelia.
Aloitetaan Python3:lla. Tarkastin ensin, että olin kotikansiossa. Loin sitten heimaailma.py-tiedoston komennolla

```
$micro heimaailma.py
```

![image](https://github.com/user-attachments/assets/e30ce50f-3f64-4227-b4e2-4ae4d6387dde)

Lisäsin tiedostoon vaaditun syntaksin:

![image](https://github.com/user-attachments/assets/4a0da461-83f0-4205-93b5-ccc4b3458bc6)
 
Tallensin tiedoston, ja kokeilin komentoa:

```
$python3 heimaailma.py
```

![image](https://github.com/user-attachments/assets/b513e5d9-bb4c-4fbe-a75a-81b1b1c49ee7)
 
Komento toimi oikein!

Tehdään sama Rubyllä. Eli ensin luodaan tiedosto komennolla

```
$micro heimaailma.rb
```

Ja lisätään tiedostoon syntaksi:

![image](https://github.com/user-attachments/assets/91d4ab54-6fce-411a-9618-f8412a703daf)
 
Lopuksi kokeilin, toimiiko komento:

```
$ruby heimaailma.rb
```

![image](https://github.com/user-attachments/assets/6616c89d-3b0d-4f20-b391-5c923a853142)

Tämäkin toimi.

Luan kanssa tehdään samat askeleet: luodaan .lua-tiedosto microlla, lisätään syntaksi ja ajetaan komento tallennuksen jälkeen.

![image](https://github.com/user-attachments/assets/7a83c87e-0ce3-44cf-86ec-ba009bd2a58d)

![image](https://github.com/user-attachments/assets/5b9fefba-c446-4c7d-806b-410b22672e7f) 
 
11:50 Ja komento toimii.

(Karvinen)

## c) Oma komento kaikkien käyttäjien ajettavaksi

12:30. Päätin tehdä komennon bashilla. Tarkoituksenani on saada ohjelma tulostamaan tekstiä sekä kansion, jossa työskentelen ja vielä lisäksi aikaleiman. Lähteenä käytin Karvisen Shell Scripting -artikkelia.
Luodaan ensin microlla tiedosto:

```
$micro komento
```

Lisätään tiedostoon syntaksi, jossa echo tulostaa tekstin, pwd näyttää työskentelykansion ja date ajankohdan.

![image](https://github.com/user-attachments/assets/99a5b5e9-95ae-4eb7-a59c-0e4e6d52a097)

Testataan komento:

![image](https://github.com/user-attachments/assets/b3e75dcc-3d59-4da7-a074-1f1b00f9c7b2)

Annetaan oikeudet kaikille ryhmille ajaa komento ja tarkastetaan että suoritusoikeudet ovat oikein:

```
$chmod ugo+x komento
$ls -l komento
```

![image](https://github.com/user-attachments/assets/17bc6fdf-b2ac-4960-8987-ae93adf6b655)

Kopioidaan tiedosto kansioon /usr/local/bin/, jotta kaikki käyttäjät voivat ajaa sen missä vain.  Testataan myös.

```
$sudo cp komento.sh /usr/local/bin/
$komento
```

![image](https://github.com/user-attachments/assets/17774491-bbc7-4975-b5ab-f26a1462d34d)

Navigoin kotikansioon, ja pystyin sieltäkin ajamaan komennon:

![image](https://github.com/user-attachments/assets/277da87f-73af-4766-8d07-96f93fc42776)
 
Tein uuden käyttäjän essitesti, jotta pystyin testaamaan komennon ajamista toisena käyttäjänä. Lisätään käyttäjä komennolla

```
$sudo adduser essitesti
```

Ja vaihdetaan käyttäjää komennolla

```
$su essitesti
```

![image](https://github.com/user-attachments/assets/3c907910-f52a-443f-8d0c-c740dc9b7275)
 
Koetetaan ajaa komento:

![image](https://github.com/user-attachments/assets/62759b07-49c8-4f7d-bb64-c410acae0990)
 
12:48 Komento toimii toisellakin käyttäjällä!

(Karvinen)

## b) Raporttien loppusilaus

Tehtävänä oli käydä aiemmat raportit läpi, ja lisätä niihin puuttuvat lähteet. Lähteet olin jo merkinnyt aiemmin, mutta kävin lisäämässä ensimmäisiin raportteihin täsmennykset missä kohdassa mitäkin lähdettä oli käytetty. Lisäsin myös näihin väliotsakkeita helpottamaan lukemista.

## d) Vanha laboratorioharjoitus

14:00 Tehtävänä on valita jokin edellisten kurssitoteutuksien arvioitavista laboratorioharjoituksista, ja tehdä siitä itselleen soveltuvat kohdat. Päädyin edellisen toteutuksen tehtävään, joka löytyy osoitteesta https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-syksy-linux-palvelimet/?fromSearch=final%20lab. 
Tehtävä pitää suorittaa tyhjällä Linux-virtuaalikoneella, eli asensin sen ensin. Käytin muistin tukena Karvisen ohjetta Debianin asentamisesta VirtualBoxille, ja latasin viimeisimmän Debianin version, jonka löysin osoitteesta https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/.
 
![image](https://github.com/user-attachments/assets/8122d0c4-02a4-4d63-bbfc-2e5425937db0)

![image](https://github.com/user-attachments/assets/1f6cb924-b66a-466f-9964-41c95bd9c9cc)
 
Tyhjä kone asennettu. Boottauksen jälkeen asensin päivitykset ja palomuurin.

![image](https://github.com/user-attachments/assets/50703205-2f50-4ca5-8170-db5ba8d37640)

![image](https://github.com/user-attachments/assets/dc13eb3f-d2b5-4635-a696-54cb5eb957c4)

![image](https://github.com/user-attachments/assets/401420e2-c055-488f-a199-6231cad99b07)
  
14:40. Sitten sammutin virtuaalikoneen, ja tein siitä kloonin. Käytän tässä harjoituksessa kloonia, ja jätän alkuperäisen koneen omaa viimeistä labraa odottamaan.

![image](https://github.com/user-attachments/assets/72a834a7-2c89-485d-ac7b-139043a72d91)

![image](https://github.com/user-attachments/assets/48d21953-3e44-4c0d-87ac-f85dca3801d3)


## c) Ei kolmea sekoseiskaa – raportin suojaus Linux-oikeuksilla

22:30 Tehdään ensin raporttitiedosto, ja suojataan se niin, että vain oma käyttäjäni pystyy sitä katsomaan. Luodaan ensin käyttäjän kotihakemistoon kansio report ja sinne index.md-tiedosto:

```
$mkdir report
$nano index.html
```

![image](https://github.com/user-attachments/assets/fd46a913-e015-49c2-9eea-00a9d686c1b3)

Laitetaan tiedostoon nimi ja linkki kotitehtäväpakettiin:

![image](https://github.com/user-attachments/assets/56f08649-0c13-43b9-9d8a-465bcd5615f9)

Latasin tässä vaiheessa micro-editorin, sillä nano tuntui kömpelöltä käyttää (unohdin kuitenkin myöhemmin käyttää microa :).

```
$sudo apt-get install micro
```

![image](https://github.com/user-attachments/assets/aab4206c-ac0b-4aae-a9f2-2d5a8cc73cc7)

Katsoin tiedoston käyttöoikeudet komennolla

```
$ls -l index.md
```

![image](https://github.com/user-attachments/assets/7fb139ac-6041-400b-b3d1-b3b238932f6f)

Ryhmillä essi ja others oli lukuoikeudet, otetaan ne pois.

```
$chmod go-r index.md
```

Tarkastin oikeudet uudestaan, ja nyt vain käyttäjä essillä on oikeus lukea ja kirjoittaa index.md-tiedostoon.

![image](https://github.com/user-attachments/assets/2cdbb9c3-a40e-48d9-9c28-df54c67b6344)
 
## d) Howdy

Tarkoituksena on tehdä komento, jonka kaikki käyttäjät voivat suorittaa. Aloitetaan luomalla kotikansioon tiedosto howdy

```
$micro howdy
```

Lisäsin syntaksin, joka tulostaa tekstiä, working directoryn, listaa tiedostot kansiosta ja tulostaa ajankohdan.

![image](https://github.com/user-attachments/assets/b7afdf82-b907-465a-a0cd-45347b68ed5a)
 
Testasin komentoa:

```
$bash howdy
```

Sitten annoin kaikille oikeudet suorittaa komennon, ja tarkastin käyttöoikeudet:

```
$chmod ugo+x
$ls -l howdy
```

![image](https://github.com/user-attachments/assets/670566e3-9f3e-4ce6-86af-96adee35d2e5)

Kopioin lopuksi tiedoston kansioon /usr/local/bin/, jotta kaikki käyttäjät voivat ajaa sitä mistä tahansa hakemistosta, ja testasin komentoa eri hakemistossa.

```
$ sudo cp howdy /usr/local/bin/
```

![image](https://github.com/user-attachments/assets/f8d2338a-8531-4c5e-9b0d-0b33c5095a88)

```
$howdy
```

![image](https://github.com/user-attachments/assets/96cc1d4f-235a-479d-93fb-701abcad0d97)

## e) Python

Tein samat vaiheet kuin aiemmin tehtävänannossa. Aloitin lataamalla Python3:n komennolla

```
$sudo apt-get install python3
Sitten loin tiedoston heimaailma.py
$micro heitaasmaailma.py
```

![image](https://github.com/user-attachments/assets/6e006fb9-db4e-421b-bef2-352610bada24)

Ja lisäsin syntaksin:

![image](https://github.com/user-attachments/assets/6f151b88-7bb4-4d23-87c7-ca28c45843d1)
 
Kokeilin komentoa. Ensin se ei toiminut, ja huomasin sen johtuvan siitä, että yritin ajaa komentoa python, vaikka oikea muoto oli python3:

![image](https://github.com/user-attachments/assets/9304ba7d-9080-4117-92f3-677f3c882f7f)
 
23:15 Kehitysympäristö osoitettu toimivaksi.

## f) Etusivu uusiksi

Tehtävänä on asentaa Apache2 ja saada oma sivu näkymään koneen IP-osoitteessa.

10.3.2025 12:20 Latasin ensin Apache2:n

![image](https://github.com/user-attachments/assets/ddfb5d92-6eff-4440-bcd2-716dc17929d8)

Kokeilin, vastaako localhost terminaalissa komennolla $curl localhost (myös $curl 127.0.0.1 toimii), sekä virtuaalikoneen webbiselaimessa osoitteessa localhost. Toimii.  

![image](https://github.com/user-attachments/assets/f21c806a-50fb-4e62-b1aa-a53303707b7f)

![image](https://github.com/user-attachments/assets/62a284c4-bf2f-4453-b43f-a56c595e41ef)

Korvataan oletussivu ja testataan:

![image](https://github.com/user-attachments/assets/75b6a545-ce1a-4e07-b9c8-020e1ecec5cc)

Seuraavaksi muokkasin Apachen asetuksia.

![image](https://github.com/user-attachments/assets/6f2d08b5-5b45-4a07-a3e9-f3d12968ba8a)

Lisäsin virtual hostin tiedot.

![image](https://github.com/user-attachments/assets/cb51d74b-e9fa-4c68-81f0-708b182ccfff)

Enabloin sivun ja käynnistin Apachen uudestaan.

![image](https://github.com/user-attachments/assets/60d80e4c-f41b-447f-adff-32045c03dece)

Loin index.html-tiedoston

![image](https://github.com/user-attachments/assets/b4f721c5-9943-4f9c-850b-7623d0f01e29)

Ja laitoin sinne syntaksin ja tallensin.

![image](https://github.com/user-attachments/assets/513be6e3-3faf-408a-87be-443fcf57f455)
 
Disabloin oletussivun.

![image](https://github.com/user-attachments/assets/a2300334-a95f-4fd8-9114-97ae04a0bab8)

Potkaisin taas demonia ja testasin sivua selaimessa ja terminaalissa.

![image](https://github.com/user-attachments/assets/0887497c-e005-4a4a-86fc-d36cf370b9c0) 

![image](https://github.com/user-attachments/assets/81310617-54dd-405e-958f-0ea9e5c19cee)

13:00 Sivu toimii.

Tarkastin vielä oikeudet, jotta muutkin pääsevät tiedostoon käsiksi:

![image](https://github.com/user-attachments/assets/964e0b94-9bcf-4802-8cfa-16648990c70f)

Oikeudet ovat kunnossa.

Päätin labran tähän harjoitukseen.

(Essberg, Karvinen)

## e) Tyhjän virtuaalikoneen asennus

Loin jo aiemmin uuden virtuaalikoneen d-kohdassa, josta tein kloonin vanhaa labraharjoitusta varten. Asensin siihen vain päivitykset sekä palomuurin.

![image](https://github.com/user-attachments/assets/33ced2cd-a284-4952-9a27-e589d060cfaa)

![image](https://github.com/user-attachments/assets/e5bff1e7-b7bb-434b-9c03-2849a18fad0a)

## Lähteet:

Tehtävänanto: Karvinen T. 2025. h7 Maalisuora. Luettavissa: https://terokarvinen.com/linux-palvelimet/. Luettu 9.3.2025.

Omat edelliset kotitehtävät. Luettavissa: https://github.com/Essberg/linux-course/. Luettu 8.-10.3.2025.

Debian ISO ladattu: https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/. Ladattu 9.3.2025.

Karvinen T. 2018. Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04. Luettavissa: https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/. Luettu 9.3.2025.

Karvinen T. 2007. Shell Scripting. Luettavissa: https://terokarvinen.com/2007/12/04/shell-scripting-4/. Luettu 9.3.2025.

Karvinen T. 2024. Final Lab for Linux Palvelimet 2024 Autumn. Luettavissa: https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-syksy-linux-palvelimet/?fromSearch=final%20lab. Luettu 9.3.2025.

Karvinen T. 2024. Install Debian on Virtualbox – Updated 2024. Luettavissa: https://terokarvinen.com/2021/install-debian-on-virtualbox/. Luettu 9.3.2025.

Karvinen T. 2018. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. Luettavissa: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/. Luettu 10.3.2025.
