# h3 Hello Web Server

Name Based Virtual Host Support
-	Nimeen perustuvan hostaamisen avulla pystyt käyttämään useampaa hostia yhdessä IP-osoitteessa. Serveri saa hostin tiedot HTTP headersien kautta käyttäjältä.
-	Name based virtual hosting on yleensä yksinkertaisempi käyttää, sillä sinun tarvitsee koskea vain DNS serverin asetuksiin ja konfiguroida nämä Apachen  tunnistettaviksi.
-	Hakiessaan käyttäjän pyyntöä, serveri vertaa ensin lähetettyä tietuetta  VirtualHost-nimeen. Jos näitä on useampi samanlainen, vertaa serveri seuraavaksi tietuetta ServerNameen, ja vielä ServerAliakseen mikäli yhtäläisyyksiä nimeämisessä oli yhä.

Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address
-	Hae ensin apache2 webbiserveriksi.
-	Muokkaukset webbisivuun ja serverin asetuksiin tehdään peruskäyttäjänä.
-	Demonia saa potkaistua komennolla sudo systemctl restart apache2.
-	Sivua voi testata komennolla curl localhost tai lataamalla sivun selaimessa.

a)	Testasin, että webbipalvelimeni vastaa osoitteesta localhost. Käytin komentoa curl localhost terminaalissa, ja sain vastauksen Pyora pyorii. Katsoin myös selaimella, että localhost-osoitteen sivu toimii. Näkyvä sivusto on sama, joka oppitunnilla tehtiin ja toimii oikein.
 
![image](https://github.com/user-attachments/assets/6b15b685-7070-462b-8596-1b3448c018fb)

![image](https://github.com/user-attachments/assets/7702163c-5df2-43bf-96f7-e1a98bca91f4)


 
b)	Komennolla sudo tail /var/log/apache2/access.log pääsee katsomaan apachen access logia. Siitä löytyy pyynnön tehneen laitteen IP, aikaleima, käytetty komento (GET) ja pyydetty resurssi (HTTP/1.1). 304 on saadun vastauksen statuskoodi: 304 tarkoittaa ettei resurssia ole muokattu edellisen käynnin jälkeen. 247 viittaa siirretyn datan määrään tavuissa. Lisäksi logista löytyy käyttöjärjestelmä sekä pyyntöön käytetty selain.
 
![image](https://github.com/user-attachments/assets/d76fd40b-32df-4507-abf3-d2ec4a1e8aba)


c)	Tehdään uusi name based virtual host komennolla sudoedit /etc/apache2/sites-available/hattu.example.com.conf. Lisätään tiedostoon tarvittavat tiedot:

![image](https://github.com/user-attachments/assets/588ccf17-a7e5-4dfd-a2e0-4172726f8fb3)


Laitetaan uusi sivu päälle komennolla sudo a2ensite pyora.example.com, ja aiemmin oppitunnilla tehty sivu pois päältä komennolla sudo a2dissite pyora.example.com. Tämän jälkeen potkaistiin demonia komennolla sudo systemctl restart apache2, jotta muutokset saatiin vahvistettua.

![image](https://github.com/user-attachments/assets/21a5b6af-bfb6-4ddc-8897-f2a725600c88)


d)	Tehdään kansio webbisivulle peruskäyttäjänä komennolla mkdir -p /home/essi/publicsites/hattu.example.com/. 

![image](https://github.com/user-attachments/assets/17a8f4ec-e660-4d7e-a4ff-5db1dbbecca3)

 
Navigoidaan tähän kansioon ja luodaan sinne index.html komennolla nano index.html. Tehdään tiedostosta validi HTML5-sivu:

![image](https://github.com/user-attachments/assets/71e848ca-75dd-4564-8def-ce53ac538d88)


Testataan toimiiko kaikki tehdyt muutokset menemällä selaimella osoitteeseen localhost. Kaikki (title, h1 ja p) toimii:

![image](https://github.com/user-attachments/assets/25cd28f2-d37c-469f-b9dd-0d2de662aeae)

 
e)	Komennolla curl localhost voin testata terminaalin kautta, vastaako juuri tekemäni sivusto pyyntöihin. Vastauksena saan sivuston sisältämän HTML5-koodin. 

![image](https://github.com/user-attachments/assets/be8715b3-7efa-4d3f-9f62-a66335db0c23)


Komennolla curl -I ‘Host: hattu.example.com’ localhost pääsee käsiksi sivuston headerseihin, eli otsakkeisiin. Sieltä löytyy käytetty serveri (Apache/2.4.62), päivämäärä ja aika, edellisen muokkauksen aikaleima sekä sisällön tyyppi (html/text).
 
![image](https://github.com/user-attachments/assets/9cd48369-c26b-43f9-adfe-d49f144794f3)

f)	Hankittu GitHub Education -linsenssi.

![image](https://github.com/user-attachments/assets/895a5710-d783-405a-8b8b-c814c91c236a)


## Lähteet:

The Apache Software Foundation, 2023. Apache HTTP Server Version 2.4 Documentation, Name-based Virtual Host Support. https://httpd.apache.org/docs/2.4/vhosts/name-based.html

Fitzpatrick S., 2020. Understanding the Apache Access Log: View, Locate and Analyze. https://www.sumologic.com/blog/apache-access-log/

MDN web docs, 2024. HTTP Headers. https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers

Karvinen T., 2025. Linux-palvelimet, h3 Hello Web Server -harjoitus. https://terokarvinen.com/linux-palvelimet/

Karvinen T., 2018. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/
