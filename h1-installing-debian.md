# Raportin kirjoittaminen

Karvinen, T. (2024) ohjeistaa raportoimaan hyviä käytäntöjä noudattaen:

-	Raportoidessa kerrot tarkkaan mitä teet ja mitä tapahtui.
-	Käytä imperfektiä.
-	Raporttia kannattaa kirjoittaa heti tehdessä sähköiseen muotoon.
-	Raportissa olevat tulokset on pystyttävä toistamaan.
-	Käytä aikaleimoja, mainitse oma käyttöympäristösi.
-	Kuvaa tekemisesi tarkoin: mitä komentoa käytit, minkä virheviestin sait, millä todensit tehtävän epäonnistuneen, missä ohjelmassa virhe tapahtui.
-	Käytä huolellista ja helppolukuista tekstiä.
-	Muista viitata lähteisiin.

(Karvinen)
  
# FSF Free Software Definition

Free Software Foundation määrittelee vapaat ohjelmat seuraavien kriteerien mukaan:

-	Free softwarella tarkoitetaan ohjelmia, joita on vapaus käyttää, kopioida, jakaa, opiskella, muuttaa ja kehittää loppukäyttäjänä (suomeksi vapaa ohjelma).
-	Free ei viittaa ohjelman maksuttomuuteen vaan sen käyttöoikeuksiin.
-	Jotta ohjelma luokitellaan vapaaksi ohjelmaksi, tulee sen taata käyttäjilleen neljä vapautta:
- Vapaus käyttää ohjelmaa valitsemallaan tavalla.
- Vapaus tutkia ohjelmaa ja muuttaa sitä itselleen sopivaksi – lähdekoodi pitää olla saatavilla.
- Vapaus jakaa ohjelmistoa eteenpäin auttaakseen muita.
- Vapaus jakaa muokattua ohjelmaa ja lähdekoodia eteenpäin.

(Free Software Foundation)

# Virtuaalikoneen asennus
-	Tein harjoituksen 19.1.2025 omalla Acer Nitro V16 -kannettavallani Windows-käyttöjärjestelmällä.
-	20:00 latasin Debianin iso-imagen osoitteesta http://mirrors.dotsrc.org/debian-cd/12.9.0-live/amd64/iso-hybrid/debian-live-12.9.0-amd64-xfce.iso.
-	20:05 latasin ja asensin VirtualBoxin osoitteesta https://www.virtualbox.org/wiki/Downloads.
-	20:10 loin virtuaalikoneen ohjeiden (Karvinen T., 2024) mukaisesti: 
  - Tyyppi: Linux
  - Versio: Debian (64-bit)
  - Muistille tilaa 6000MB
  - Loin uuden virtuaalisen kovalevyn ja allokoin sille 60GB tilaa, tyyppi VDI.
  - Syötin Debianin ISO-imagen virtuaaliseen CDROMiin.
-	20:20 boottasin Debianin live-versioon.
-	20:22 testasin järjestelmän toimivuutta menemällä web-selaimella osoitteeseen google.com – hiiri, näppäimistö, näyttö sekä internet toimivat.

![image](https://github.com/user-attachments/assets/9201f7e1-ab3c-4138-b082-e51b7e84d808)
  -	Järjestelmän kello ei tässä vaiheessa vielä näyttänyt oikeaa aikaa.
-	20:35 aloitin asentamaan Debiania virtuaalikoneelle työpöydältä löytyvän Install Debian -ohjelman avulla.
  - Valitsin kieleksi American English, lokaatioksi Helsinki (Suomi), näppäimistön asetukset suomeksi.
  - Valitsin erase disk, ei kryptausta.
    
![image](https://github.com/user-attachments/assets/28cda398-69e1-4ab2-ae27-ec9807296dfa)
  - Nimesin koneen ja käyttäjän.
  - Valitsin lopuksi "install".
-	20:50 Debian oli asentunut, valitsin “Restart now” sekä klikkasin “Done”
-	21:00 uudelleenkäynnistyksen jälkeen pääsin kirjautumaan.

![image](https://github.com/user-attachments/assets/3b214d1b-ba99-45b2-bd3c-fcda550557d3)

-	21:05 testasin käyttöjärjestelmän toimivuutta menemällä web-selaimella osoitteeseen www.wikipedia.org – kaikki toimi normaalisti.
-	Debian asennettu onnistuneesti.

![image](https://github.com/user-attachments/assets/a4a673c5-2f61-48a4-8e35-5b500da2efec)

(Karvinen)

## Lähteet 
Free Software Foundation, Inc. What is Free Software? https://www.gnu.org/philosophy/free-sw.html

Karvinen T. 2006. Raportin kirjoittaminen. https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

Karvinen T. 2024. Install Debian on VirtualBox – Updated 2024. https://terokarvinen.com/2021/install-debian-on-virtualbox/

Tehtävänanto: Karvinen T.  2025, Linux-palvelimet. Harjoitus 1., Oma Linux. https://terokarvinen.com/linux-palvelimet/
