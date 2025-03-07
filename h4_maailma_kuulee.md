# h4 Maailma kuulee

Tehtävänantona oli tehdä kaksi tiivistelmää sekä vuokrata oma virtuaalipalvelin. Palvelimelle on tarkoitus tehdä sille vaadittavat alkutoimet ja lopuksi asentaa sille vielä oma webbipalvelin.

Harjoituksessa käytetty kone:

Acer Nitro V16.

Käyttöjärjestelmä Windows 11 64-bit.

Prosessori AMD Ryzen 7 8845HS

Näytönohjain Radeon 780M Graphics 3.80 GHz.

Asennettu RAM 16GB.

Virtuaalikoneena Oracle VirtualBoxiin asennettu Debian.

![image](https://github.com/user-attachments/assets/0392d1e6-da5e-4c0c-b198-5b9ffe2ec975)

## Tiivistelmä Susanna Lehdon blogipostauksesta Teoriasta käytäntöön pilvipalvelimen avulla

Pilvipalvelimen vuokraus ja asennus:

-	Palvelinta voi päästä kokeilemaan ilmaiseksi GitHub Educationin kautta krediiteillä.
-	Maksuhälytykset on hyvä laittaa päälle välttyäkseen ylimääräisiltä maksuilta.
-	Käyttöjärjestelmäksi valitaan uusin versio Debianista.
-	Paketin muistiksi riittää 1GB ja kannattaa valita halvin tämän sisältävä paketti.
-	Serveri kannattaa valita tiedonsiirron nopeuden sekä alueellisten DGPR:n vaatimuksien perusteella. Fyysisen sijainnin kannattaa olla palvelimen käyttäjän ja serverin välillä mahdollisimman pieni.
-	SSH-avain on aina turvallisempi valinta autentikointimenetelmäksi kuin salasana.
  
Palvelin suojaan palomuurilla:

-	Otetaan yhteys palvelimeen terminaalin kautta (ssh root@10.0.0.1).
-	Ensin päivitetään ohjelmat komennolla sudo apt-get update.
-	Palomuuri asennetaan komennolla sudo apt-get install ufw.
-	Tehdään reikä muuriin porttia varten komennolla sudo ufw allow 22/tpc.
-	Palomuurin saa päälle komennolla sudo ufw enable.
  
Kotisivut palvelimelle:

-	Ensin tehdään palvelimelle uusi käyttäjä komennolla sudo adduser user. Luodaan hyvä salasana ja jätetään pyydetyt tietueet tyhjiksi.
-	Annetaan käyttäjälle sudo-oikeudet komennolla sudo adduser user sudo
-	Ennen root-tunnusten lukitsemista tarkastetaan luodun tunnuksen toimivuus joko kokeilemalla yhteyttä eri terminaalissa, tai katkaisemalla yhteys palvelimeen ja ottamalla uudella tunnuksella yhteyttä.
-	Root-tunnukset lukitaan komennolla sudo usermod –lock root.
-	Asennetaan uudella käyttäjällä päivitykset komennoilla sudo apt-get update, sekä sudo apt-get upgrade sekä sudo apt-get dist-upgrade.
-	Apachen saa asennettua komennolla sudo apt-get install apache2.
-	Luodaan toinen reikä palomuuriin komennolla sudo ufw allow 80/tcp.
-	Korvataan Apachen testisivu komennolla echo Hello world! |sudo tee /var/www/html/index.html.
-	Otetaan userdir-moduuli käyttöön komennolla sudo a2enmod userdir.
-	Apachen uudelleenkäynnistys muutosten päivittämiseksi sudo service apache2 restart, nykyään käytetään sudo systemctl restart apache2.
-	Netissä näkyvää index.html-tiedostoa muokataan käyttäjän julkisessa public_html- kansiossa.
  
Palvelimen ohjelmien päivitys:

-	Päivitykset asennetaan juuri luodun käyttäjän avulla komennoilla sudo apt-get update, sudo apt-get upgrade sekä sudo apt-get dist-upgrade.
  
(Lehto)

## Tiivistelmä Tero Karvisen artikkelista First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS

Serverin vuokraaminen

-	Luodaan uusi käyttäjä valitulle palveluntarjoajalle, tässä DigitalOcean.
-	Valitaan serveriksi Ubuntu 16.04 LTS.
-	Valitaan asiakkaita fyysisesti lähellä oleva serveri.
-	Luo SSH-avain tai käytä sinulle generoitua salasanaa.
-	Tarkista serverin IP-osoite yhteydenmuodostusta varten.
-	Otetaan SSH-yhteys palvelimeen terminaalissa komennolla ssh root@10.0.0.1.

Palomuuri

-	Tehdään ensin reikä SSH-yhteyttä varten komennolla sudo ufw allow 22/tcp.
-	Laitetaan palomuuri päälle komennolla sudo ufw enable.

Käyttäjän luonti

-	Luodaan uusi käyttäjä sudo adduser user
-	Lisätään käyttäjä ryhmiin sudo, admin ja adm komennoilla sudo adduser user sudo, sudo adduser user admin ja sudo adduser user adm.
-	Kokeillaan käyttäjän toimimista toisessa terminaalissa yrittämällä saada uusi yhteys juuri luodulla käyttäjällä user@10.0.0.1.
-	Käytetään vain vahvoja salasanoja.

Root-tunnuksen sulkeminen

-	Käytetään komentoa sudo usermod –lock root.
- Estetään SSH-kirjautuminen editoimalla sshd_config-tiedostoa:

$ sudoedit /etc/ssh/sshd_config
Muutetaan kohta PermitLogin yes –> no.

-	Sulkemisen jälkeen päivitetään vielä paketit sudo apt-get update ja sudo apt-get upgrade.

-	Muistetaan tehdä reikä Apachea varten komennolla sudo ufw allow 80/tcp.
  
(Karvinen)

## a)	Oman virtuaalipalvelimen vuokraus

19:30. Apuna käytin oppitunnin luentoa sekä Karvisen Linux-palvelinten kurssisivustoa. Yritin ensin käyttää GitHub Educationin krediittejä Digital Oceanin palvelimen vuokraukseen, mutta jostain syystä sivusto ei saanut maksukorttiani vahvistettua, ja päätin siirtyä kokeilemaan UpCloudia. Tämä palveluntarjoaja hyväksyi tietoni, ja pääsin vahvistamaan tilini.

![image](https://github.com/user-attachments/assets/c503da05-7a0f-45fd-bff8-5110ca88cc73)

Maksoin vielä 10 euroa päästäkseni kaikkiin ominaisuuksiin käsiksi.

![image](https://github.com/user-attachments/assets/53748ddf-c1cc-4604-9015-d5d486fade9e)

19:40. Ensimmäisen serverin asennus. Aloitetaan painamalla Servers-välilehdeltä Deploy server -nappia.

![image](https://github.com/user-attachments/assets/1216a0d7-e236-45e9-9816-d81c871b8a20)

Datasiirron nopeuden vuoksi serverin sijainti kannattaa valita oman tai asiakkaiden sijainnin perusteella. Myös alueen GDPR:n säädökset tulee ottaa valinnassa huomioon. Serveri on tulossa omaan käyttöön, joten Suomessa sijaitseva serveri oli luonnollinen valinta.

![image](https://github.com/user-attachments/assets/93abde77-0fce-4be0-b65c-dca9dd6306e8)

Oppitunnilla mainittiin, että 1GB muistia on riittävä koko kurssitöitä varten, joten valitsin huokeimman suunnitelman, josta minimimäärä muistia löytyy.

![image](https://github.com/user-attachments/assets/8fb05219-629a-44a6-a859-d71f0d89fb81)

En valinnut tietojen enkryptausta, enkä automaattisia varmuuskopioita.

Käyttöjärjestelmäksi valitsin tehtävänannon mukaisesti Debianin uusimman version.

![image](https://github.com/user-attachments/assets/a192f2df-b4a0-4cec-bdd1-2429a0b61056)

En muuttanut muita valmiiksi valittuja asetuksia.

![image](https://github.com/user-attachments/assets/82d7b16f-7249-40ab-8bdb-7e1fdadf396a)
 
Seuraavaksi piti valita tapa, jolla palvelimeen voi kirjautua sisään. Debianin kanssa ei ollut mahdollista käyttää salasanaa, luodaan siis SSH-avaimet.

![image](https://github.com/user-attachments/assets/4820503f-bb99-4ca1-b49c-7c1219678912)

19:45. SSH-avainten luonti onnistuu virtuaalikoneen terminaalin kautta. Karvisen kurssimateriaalien mukaisesti aloitetaan ensin päivittämällä ohjelmistot uusimpiin versioihin komennolla sudo apt-get update pienten salasanatypojen jälkeen.

![image](https://github.com/user-attachments/assets/19442a02-00e3-4490-8988-0a08c1e142fe)

Ladataan OpenSSH komennolla sudo apt-get -y install openssh-client.

![image](https://github.com/user-attachments/assets/10a4405a-03fe-48da-9bd8-b545956338e1)

Luodaan avain komennolla ssh-keygen ja painamalla enteriä kolmesti (oletuskansio hyvä, ei tarvitse passphrasea).

![image](https://github.com/user-attachments/assets/a37fbef0-3752-4fc1-8bc9-5100cb0f0cef)

Navigoidaan kansioon, jossa luotu julkinen SSH-avain sijaitsee komennolla cd home/essi/.ssh, tarkistetaan tiedostojen löytyvän komennolla ls. Mennään kopioimaan avain komennolla micro id_rsa.pub. 

![image](https://github.com/user-attachments/assets/bca94ac7-6448-49b0-80ce-0b329ab86890)

19:50 Tässä vaiheessa tulee mieleen, että avaimen kopiointia helpottaisi, jos olisi tajunnut tehdä serverin vuokraamisen virtuaalikoneen kautta. Etsin googlesta, kuinka pystyn kopioimaan helposti tekstiä virtuaalikoneen ja isäntäkoneen välillä. Löysin videon How to Enable Copy/Paste: Oracle Virtual Box, jossa neuvottiin muuttamaan virtuaalikoneen Advanced-asetuksista kohta Shared Clipboard Disabledista Bidirectionaliin ja tallentamaan muutokset. Tämä toimi, ja sain julkisen SSH-avaimen kopioitua.

![image](https://github.com/user-attachments/assets/76014f06-e807-4f0b-a3b5-2d09031ce68d)

Lisäsin SSH-avaimen serverin kirjautumistietoihin.

![image](https://github.com/user-attachments/assets/664033a2-871f-4d40-81ff-0ba7741581e2)
 
Vuokrasin yhden serverin ja valitsin hostnameksi sienikumpu. Lopuksi loin serverin painamalla Deploy.

![image](https://github.com/user-attachments/assets/091ac49e-dd8a-45d7-be9b-e4bb0e40f316)
 
Serveriä luotiin ja se saatiin luotua valmiiksi.

![image](https://github.com/user-attachments/assets/06a928ea-e324-41ba-9816-32f3f53be292)

Luotu serveri näyttää toimivan, ja tiedoista saamme yhteyden muodostukseen tarvittavan IP-osoitteen: 94.237.119.77.

![image](https://github.com/user-attachments/assets/d36ec0bb-59ba-4750-924d-7c94be5d6660)

(CyberSecc Brit, 2022; Karvinen T., 2025)

## b)	Alkutoimet omalla virtuaalipalvelimella

20:10. Karvisen artikkelin First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS mukaisesti aloitetaan ottamalla yhteyttä serveriin komennolla ssh root@94.237.119.77. Varmistetaan yhdistäminen kirjoittamalla yes ja enter. Yhdistäminen onnistuu.

![image](https://github.com/user-attachments/assets/48b12ebe-e2a1-45c9-8f10-d5dc0f5f1971)

Lisätään käyttäjä komennolla sudo adduser essi ja luodaan vahva salasana pyydettäessä.

![image](https://github.com/user-attachments/assets/fee1b34d-a5d8-4dfa-aaca-17cba4c2fb22)
 
Tehdään uusi sudo-käyttäjä komennolla sudo adduser essi sudo. Lisäsin itseni myös adm-ryhmään komennolla sudo adduser essi adm.

![image](https://github.com/user-attachments/assets/c8d5ff3c-05e2-4404-9112-91714ac65f96)

20:15. Siirrytään palomuurin asennukseen. Asennetaan ensin ohjelmien päivitykset komennolla sudo apt-get update, sekä Karvisen suosittelemat ohjelmat palomuurin lisäksi komennolla sudo apt-get -y install micro bash-completion openssh-client wget curl ufw.  Kun palomuuri on saatu asennettua, tehdään siihen ensin reikä SSH-yhteydelle komennolla sudo ufw allow 22/tcp.mSallitaan myös yhteys porttiin 80 komennolla sudo ufw allow 80/tcp Apachea varten. Sen jälkeen asetetaan muuri päälle komennolla sudo ufw enable.

![image](https://github.com/user-attachments/assets/ef2af7a8-6cb5-43f0-a691-78554552f96a)

Koska portti SSH-yhteydelle oli jo avattu, ei palomuurin päällekytkentä vaikuttanut serveriin muodostettuun yhteyteen.

20:25. Kopioidaan rootin asetukset, jotta luotu uusi käyttäjä pääsee kirjautumaan sisään. Käytetään komentoa sudo cp -rvn /root/.ssh/ /home/essi/ sekä sudo chown -R essi:essi /home/essi/.

![image](https://github.com/user-attachments/assets/564031b6-cdcf-44b1-b329-565e66cb4b8a)

Palataan takaisin lokaalille käyttäjälle komennolla exit.

![image](https://github.com/user-attachments/assets/67dbab52-cd76-4ebf-b7c7-9ad13683fa55)

Kokeillaan toimiiko luotu käyttäjä, otetaan yhteys serveriin komennolla ssh essi@94.237.119.77. Yhteys muodostettu onnistuneesti!

![image](https://github.com/user-attachments/assets/118dbb13-93e4-4b56-a302-765803e6e027)

20:35. Seuraavaksi suljetaan root-käyttäjä komennoilla sudo usermod --lock root sekä sudo mv -nv /root/.ssh /root/DISABLED-ssh/.
 
Lopuksi päivitin viimeisimmät ohjelmien tietoturvapäivitykset komennolla sudo apt-get upgrade.

(Karvinen T., 2017)

## c)	Webbipalvelimen asennus ja testisivun korvaaminen

20:40. Käytin muistin apuna Karvisen ohjeita Apachen käytöstä. Asennetaan ensin palvelimelle Apache2 komennolla sudo apt-get install apache2.

![image](https://github.com/user-attachments/assets/09b47a26-4ad8-473d-aa9c-dda88fe48f6e)

Kokeilin localhostin toimivuutta komennolla curl localhost ja vastauksena sain sivun HTML5-koodin. Sivusto siis toimii.

![image](https://github.com/user-attachments/assets/5dae384a-3ce0-43e4-b549-b8a2b3696713)

Muokataan oletussivua komennolla echo "Testaus-sieni"|sudo tee /var/www/html/index.html ja testataan komennolla curl localhost. Kaikki näyttää toimivan.

![image](https://github.com/user-attachments/assets/0f7e26e3-f954-442d-87e4-6c87005c35cd)

Menin vielä oman lokaalikoneeni selaimella kokeilemaan serverin toimivuutta – kaikki ok!

![image](https://github.com/user-attachments/assets/a59d0914-decc-4ece-973c-bd1f6fd85e16)

(Karvinen 2018)


## Lähteet:
Karvinen T., 2025. Linux-palvelimet, h4 Maailma kuulee. https://terokarvinen.com/linux-palvelimet/.

Karvinen T., 2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/.

Karvinen T., 2018. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/

CyberSecc Britt, 2024. How to Enable Copy/Paste: Oracle Virtual Box.   https://www.youtube.com/watch?v=DC5NngsIhcw. Katsottu 9.2.2025.

Lehto, S., 2022. Teoriasta käytäntöön pilvipalvelimen avulla (h4). https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
