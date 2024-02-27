 
 ## Tiivistelmä

 Tiivistelmä seuraavista sivuista:
 
 [The Apache Software Foundation: Name-based Virtual Host Support](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)
 
 [Tero Karvinen: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)
 
- Apache-nimipohjaiset virtuaalihostaukset (name based virtual hosts) mahdollistavat useiden sivustojen ylläpitämisen saman IP-osoitteen alla
- Yksinkertaistaa asetusten hallintaa ja säästää IP-osoitteita
- On tärkeää määrittää jokaiselle virtuaalihostille ServerName välttääkseen perityt nimet palvelimen peruskonfiguraatiosta
- ServerAliaksella voi määrittää lisänimiä virtuaalihostille
- Konfiguraation järjestys on merkityksellinen, ja ensimmäinen sopiva ServerName tai ServerAlias otetaan käyttöön

## Tehtävät
 
 ### Localhost vastaa

 Olin luennolla saanut tehtyä jo esimerkkisivun palvelimelle, ja se näkyi kuten pitää.
 
 ![image](https://github.com/RonjaVee/smial/assets/148786247/74755942-4100-4da7-9ec8-771772bebd0d)
 ![image](https://github.com/RonjaVee/smial/assets/148786247/73358757-35e0-418f-974d-5a1ad1ab27b7)
 
### Lokirivien tulkintaa

Kun lähdin tutkimaan lokitietoja, ei uusia merkintöjä lokeista (sekä error.log että access.log). Kokeilin vielä päivittää sivua, mutta uusia merkintöjä en saanut näkyviin.


![image](https://github.com/RonjaVee/smial/assets/148786247/ae464e72-57b9-4a4f-ae30-25696a2770a0)
![image](https://github.com/RonjaVee/smial/assets/148786247/2565e0d3-fa46-42e6-9094-3577d925950a)

Tältä loki näytti, eikä muutoksia tullut tehtävien jälkeenkään näkyviin:

![image](https://github.com/RonjaVee/smial/assets/148786247/a4a986be-1cad-4e28-a5d4-d7825a9b71a7)

Lähdin sitten vanhasta lokimerkinnästä tutkimaan, mitä kaikkea se kertoo. Kopioin merkinnän ja siirsin sen tekstieditoriin ja otin siitä kuvakaappauksen, sillä en saanut lokimerkintöjä järkevästi näkyviin
komentokehotteessa.

![image](https://github.com/RonjaVee/smial/assets/148786247/2bcea386-d422-43c7-893d-044018a704a2)


- 127.0.0.1: IP-osoite, josta pyyntö tulee. Tässä local hostin IP eli minun.
- ensimmäinen "-" : tunnistautuneen käyttäjän nimi (nyt tyhjä)
- toinen "-" : käyttäjän tunnus (nyt tyhjä)
- Seuraavaksi on aikaleima, jolloin pyyntö on tehty. Tässä kohti näkyy eri päivä kuin tehtävää tehdessäni oli.
- GET-kohdassa kerrotaan pyynnön tyyppi: tässä kohteena index.html ja pyynnön protokolla ja versio http/1.1
- Luku 304 on statuskoodi ja 247 kertoo, kuinka paljon dataa tavuina siirtyi palvelimelta kyselyn esittäjälle. Statuskoodi 304 tarkoittaa, ettei sivua olla muokattu sitten viime pyynnön, joten tiedonsiirtoa ei tehdä uudestaan, vaan sivusto näyttää välimuistiversion.
- "-"	:Tässä kohtaa tarkoittaa, ettei viittausta (refer) ole saatavilla, eli  tietoa siitä, mistä osoitteesta pyyntö tuli.
- Mozilla-kohdasta eteenpäin näkee käytetyn selaimen ja sen version.

Etsitty vastaukset täältä: 

Fitzpatrick, Scott. Understanding the Apache Access Log: View, Locate and Analyze. 14.1.2020. sumo logic. [https://www.sumologic.com/blog/apache-access-log/](https://www.sumologic.com/blog/apache-access-log/)

Ayooluwa, Isaiah. How to View and Configure Apache Access & Error Logs. 12.10.2023. Betterstack. [https://betterstack.com/community/guides/logging/how-to-view-and-configure-apache-access-and-error-logs/](https://betterstack.com/community/guides/logging/how-to-view-and-configure-apache-access-and-error-logs/)

Ahrefs. 304 Not Modified: What is 304 Not Modified Response? 2024. [https://ahrefs.com/seo/glossary/304-not-modified](https://ahrefs.com/seo/glossary/304-not-modified)


### Uusi name based virtual host

Lähdin luomaan uutta sivua edellisen tapaan ohjeen(linkki) mukaan. Aloitin luomalla konfiguraatiotiedoston. Tämä konfiguraatiotiedosto asettaa sivuston "hattu.example.com" toimittamaan tiedostoja hakemistosta
"/home/xubuntu/publicsites/pyora.example.com" ja vastaamaan pyyntöihin, jotka kohdistuvat sekä pyora.example.com -sivustoon. 

![image](https://github.com/RonjaVee/smial/assets/148786247/c4157557-90d6-41de-b024-5180eaa2ef50)


![image](https://github.com/RonjaVee/smial/assets/148786247/b7ababaf-0194-4feb-b2f6-e3473a38d62d)

Sitten kirjoitin sivustolle vähän tekstiä testatakseni, että se näkyy kuten pitää.

![image](https://github.com/RonjaVee/smial/assets/148786247/032d54cb-5f9f-4620-802d-5fe7e2617b96)

![image](https://github.com/RonjaVee/smial/assets/148786247/ac8c62a6-fc6a-4f8a-9dda-3314e08e6af8)

Poistin vanhan sivun sites-enabled -kansiosta.

![image](https://github.com/RonjaVee/smial/assets/148786247/0aff4e2a-0577-45db-bc71-3f84d33d35d0)

Käytin HTML-kieltä sivun laatimiseen. Index.html -tiedostoa voi muokata ilman sudoa, joten näitä kokeiluja voi tehdä ilman pääkäyttäjän oikeuksia. Käytin html-sivun pohjana: chrisvfritz. Simplest possible HTML template. 18.11.2014. Github. [https://gist.github.com/chrisvfritz/bc010e6ed25b802da7eb](https://gist.github.com/chrisvfritz/bc010e6ed25b802da7eb) Korjailin sitä kuitenkin sen verran, että meni validoinnista läpi sivulla ja muokkasin tekstiä [https://www.freeformatter.com/html-validator.html](https://www.freeformatter.com/html-validator.html)


![image](https://github.com/RonjaVee/smial/assets/148786247/c36b34f7-0ad0-4c41-9859-9e8065d13639)
![image](https://github.com/RonjaVee/smial/assets/148786247/dc41c37a-dbf3-4ea2-9e93-bb06b42598db)
![image](https://github.com/RonjaVee/smial/assets/148786247/9e3e79e6-af6e-4912-8c36-1057e86978ca)
![image](https://github.com/RonjaVee/smial/assets/148786247/e91574f5-2623-42fa-9335-b86b757a2f4d)


### Curl-komennot

Tein curl-komennon localhostista (IP-osoite 127.0.0.1). Komento näytti, mitä sivustolla näkyy (index.html -tiedoston sisältö).

![image](https://github.com/RonjaVee/smial/assets/148786247/d86b7b64-2171-4937-bd7b-aab17947f8ec)

Curl -I -komento näytti seuraavaa:

![image](https://github.com/RonjaVee/smial/assets/148786247/d4d8b516-b6ac-4432-b7d6-da9573ca07a8)

- HTTP/1.1 200 OK: Käytetty HTTP-protokolla ja versio sekä statuskoodi (200 OK = pyyntö onnistui)
- Server: Kertoo käytetyn web-palvelimen ja sen version, tässä toki Apache
- Date, eli komennon aikaleima, palvelimen aika vastauksen lähettämisen hetkellä
- ETag kertoo, mikä versio sivustosta näkyy (jos se muuttuu, on sivusto päivittynyt)
- Accept-Ranges:  Tarkoittaa, että palvelin tukee osapyyntöjä tavuina (bytes)
- Content-Length: 144: Vastauksen koko tavuina

Vastaukset etsitty täältä: 

Curl. Conditionals. 13.1.2024. [https://everything.curl.dev/http/conditionals](https://everything.curl.dev/http/conditionals)

Geeksforgeeks. HTTP headers | Accept-Ranges. 31.10.2019. [https://www.geeksforgeeks.org/http-headers-accept-ranges/](https://www.geeksforgeeks.org/http-headers-accept-ranges/)







### Lähteet (haettu 4.2.2024):

Pohjana tehtävänanto: Karvinen, Tero. Linux Palvelimet 2024. 1.11.2024. [https://terokarvinen.com/2024/linux-palvelimet-2024-alkukevat/#h3-hello-web-server](https://terokarvinen.com/2024/linux-palvelimet-2024-alkukevat/#h3-hello-web-server)

[The Apache Software Foundation. Name-based Virtual Host Support. 2023. [https://httpd.apache.org/docs/2.4/vhosts/name-based.html](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)

Karvinen, Tero. Command line basics revisited. 3.2.2020. [https://terokarvinen.com/2020/command-line-basics-revisited/](https://terokarvinen.com/2020/command-line-basics-revisited/)

Karvinen, Tero. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. 10.4.2018. [https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)

Fitzpatrick, Scott. Understanding the Apache Access Log: View, Locate and Analyze. 14.1.2020. sumo logic. [https://www.sumologic.com/blog/apache-access-log/](https://www.sumologic.com/blog/apache-access-log/)

Ayooluwa, Isaiah. How to View and Configure Apache Access & Error Logs. 12.10.2023. Betterstack. [https://betterstack.com/community/guides/logging/how-to-view-and-configure-apache-access-and-error-logs/](https://betterstack.com/community/guides/logging/how-to-view-and-configure-apache-access-and-error-logs/)

Ahrefs. 304 Not Modified: What is 304 Not Modified Response? 2024. [https://ahrefs.com/seo/glossary/304-not-modified](https://ahrefs.com/seo/glossary/304-not-modified)


chrisvfritz. Simplest possible HTML template. 18.11.2014. Github. [https://gist.github.com/chrisvfritz/bc010e6ed25b802da7eb](https://gist.github.com/chrisvfritz/bc010e6ed25b802da7eb)

Curl. Conditionals. 13.1.2024. [https://everything.curl.dev/http/conditionals](https://everything.curl.dev/http/conditionals)

Geeksforgeeks. HTTP headers | Accept-Ranges. 31.10.2019. [https://www.geeksforgeeks.org/http-headers-accept-ranges/](https://www.geeksforgeeks.org/http-headers-accept-ranges/)

#

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. [http://www.gnu.org/licenses/gpl.html](http://www.gnu.org/licenses/gpl.html)

#

päivitetty lähteitä tekstin lomaan sekä näytetty validoitu html 6.2.2024.

 
 
 

 

 
 
 
 
 
 
