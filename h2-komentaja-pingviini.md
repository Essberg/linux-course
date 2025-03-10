# h2 Komentaja Pingviini

Harjoituksessa käytetty kone:

Acer Nitro V16.

Käyttöjärjestelmä Windows 11 64-bit.

Prosessori AMD Ryzen 7 8845HS

Näytönohjain Radeon 780M Graphics 3.80 GHz.

Asennettu RAM 16GB.

Virtuaalikoneena Oracle VirtualBoxiin asennettu Debian.

![image](https://github.com/user-attachments/assets/0392d1e6-da5e-4c0c-b198-5b9ffe2ec975)

## Command Line Basics Revisited:
-	Komentokehoitteet ovat olleet olemassa jo ennen Linuxia, Googlea tai Windowsia, ja ne ovat edelleen käytännöllisiä ja erittäin käytettyjä.
-	Komentorivillä työskentelet aina jossakin hakemistossa, juurikansio on ”/”.
-	Tabulaattorilla voit täydentää komentoja ja nopeuttaa työskentelyä ja nuolinäppäimillä saat kursoria liikuteltua.
-	Komentoja käytetään mahdollisimman pienillä käyttäjäoikeuksilla, sudo-komentoa käytetään vain kuin tarvitaan rajoittamattomia oikeuksia.
-	Oma huomio: ole tarkkana komentoja suorittaessa, sillä terminaali ei varoita kun olet tekemässä vääriä asioita.

(Karvinen)

## Harjoitus:

a)	Käytin ohjeena Karvisen Linux-kurssin tehtävänantoa. Päivitin ensin kaikki paketit uusimpiin versioihin, jonka jälkeen asensin micron komennolla sudo apt install micro.
 
![image](https://github.com/user-attachments/assets/b707a7dc-143e-41a2-9fe9-d4db03ff9bf6)
![image](https://github.com/user-attachments/assets/5ba43f42-b9fd-4490-9abd-95adb6cbfe5c)

(Karvinen)

b)	Asensin itselleni kolme uutta komentoriviohjelmaa. Valitsin bastetin, calcin sekä CMatrixin.  Kaikki kolme ohjelmaa saa asentumaan kerrallaan käyttämällä komentoa sudo apt-get install bastet calc cmatrix.

![image](https://github.com/user-attachments/assets/0b624f44-b88c-4cb6-9126-9458103a6101)

Bastet on terminaalissa toimiva tetris-kopio, jonka saa käyntiin komennolla bastet. Poistumaan pääsee painamalla ctrl-c.

![image](https://github.com/user-attachments/assets/f08e7d5e-81a0-4861-aea7-3210743157df)

Calc toimii laskimena terminaalissa, sitä on helppo käyttää komennolla calc jonka jälkeen laskutoimitus annetaan.

![image](https://github.com/user-attachments/assets/0c3ab81f-12d2-4bec-bbcb-82393d3196ce)

Cmatrix käynnistyy komennolla cmatrix, ja se täyttää terminaalin matrix-grafiikalla. Poistuminen ohjelmasta painamalla ctrl+c.

(Karvinen)

c)	Vaihdoin juurihakemistoon komennolla cd /. Listasin siellä olevat kansiot ja tiedostot komennolla ls. Vaihdoin sitten kotihakemistoon komennolla cd home ja listasin siellä olevat kansiot komennolla ls.

![image](https://github.com/user-attachments/assets/08f4534c-b834-4af6-86fc-434855ee1c0e)

Menin takaisin hakemistossa ylöspäin komennolla cd .. ja pääsin takaisin juurihakemistoon. Menin kansioon etc komennolla cd etc, ja listasin siellä olevat tiedostot komennolla ls.

![image](https://github.com/user-attachments/assets/77fadab5-9ce6-46d9-af84-01be98094ec2)

Menin kansioon fonts komennolla cd fonts, ja listasin siellä olevat kansiot komennolla ls. Menin lukemaan fonts.conf-tiedostoa komennolla less fonts.conf ja poistuin lukutilasta painamalla q.

![image](https://github.com/user-attachments/assets/9d7f128b-7835-4366-b907-ed61252f4482)
![image](https://github.com/user-attachments/assets/488bf947-c8af-4c3d-9967-293857a57441)

Kävin media-hakemistossa listaamassa siellä olevat tiedostot.

![image](https://github.com/user-attachments/assets/330a5dd1-b736-4240-abe0-5c6a66f35d8f)

Menin takaisin juurihakemistoon ja listasin tiedostot ja kansiot komennolla ls. Menin hakemistoon var komennolla cd var ja listasin tiedostot komennolla ls. Luin tiedoston alternatives.log komennolla less.

![image](https://github.com/user-attachments/assets/65c70606-e951-4f83-ade2-45c372f05cda)

(Karvinen)

d)	Grep-komennolla hain sanaa ”kissa” luomastani dokumentista kissa.txt, käytin komentoa grep ”kissa” kissa.txt. Hakiessani sanaa ”kissalla” ei komento löytänyt sitä, ennen kuin käytin komentoa grep -i ”kissalla” kissa.txt. Lisäämällä komentoon -i hakee se tekstiä ottamatta huomioon kirjainten kapitalisointia. Hain vinkkejä grepin käyttöön osoitteesta https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/.

![image](https://github.com/user-attachments/assets/5634f967-3004-40df-970b-03e0afce881e)

(Moorty, Karvinen)

e)	Käytin putkea katsoessani etc-kansion tiedostoja saadakseni ne näkymään näytöllinen kerrallaan.

![image](https://github.com/user-attachments/assets/01155edd-5ec4-4fab-a36a-3eb282c6dfb3)
![image](https://github.com/user-attachments/assets/6de2d059-5164-4dea-a21e-c0e73a78e5f9)

(Karvinen)
  
f)	Asensin koneelleni lshw:n komennolla sudo apt-get install lshw. Asennuksen jälkeen sain koneeni raudan listattua komennolla sudo lshw -short -sanitize 
Tuloksesta näkee oman koneeni prosessorin sekä näytönohjaimen. Sieltä löytyy myös virtuaalikoneelle asetetut parametrit, kuten 6000MB muistia sekä virtuaalinen CD-ROM.

![image](https://github.com/user-attachments/assets/2443cdee-e099-4acc-b361-ade895817e40)

(Karvinen)

## Lähteet:

Tehtävänanto: Karvinen T. 2025, h2 Komentaja Pingviini. Linux-palvelimet-kurssi. https://terokarvinen.com/linux-palvelimet/

Karvinen T., 2020. Command Line Basics Revisited. https://terokarvinen.com/2020/command-line-basics-revisited/

Karvinen T., 2009. Command Line Basics. https://terokarvinen.com/2009/command-line-basics-4/

Moorty, S. 2009. 15 Practical Grep Command Examples In Linux / UNIX. https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/



