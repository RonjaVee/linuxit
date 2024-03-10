## Tiivistelmä

Tiivistelmä ohjeista:
Karvinen, Tero. Django 4 Instant Customer Database Tutorial. 13.2.2022. [https://terokarvinen.com/2022/django-instant-crm-tutorial/](https://terokarvinen.com/2022/django-instant-crm-tutorial/)

Karvinen, Tero. Deploy Django 4 - Production Install.13.2.2022. [https://terokarvinen.com/2022/deploy-django/?fromSearch=django](https://terokarvinen.com/2022/deploy-django/?fromSearch=django)

- Asenna tarvittavat paketit ja työkalut (micro, pwgen) 

- Luo virtuaaliympäristö (virtualenv) ja aktivoi se 
  > virtualenv --system-site-packages -p python3
  
  > env/source env/bin/activate

- Asenna Django ja tarkista sen versio
  > django-admin --version

- Luo uusi Django-projekti
  > django-admin startproject "nimi"
  
  > cd "nimi"

- Käynnistä palvelin ja avaa tervetulonäkymä (raketin kuva)
  > ./manage.py runserver

- Avaa hallintaliittymä osoitteessa http://127.0.0.1:8000/admin/
  
- päivitä tietokannat ja luo pääkäyttäjä
  > ./manage.py makemigrations
  
  > ./manage.py migrate
  
  > ./manage.py createsuperuser

- Luo uusi sovellus CRM:lle, määritä mallit ja rekisteröi ne hallintaliittymässä
  > ./manage.py startapp crm
  
  > "nimi"/settings.py -> crm kohtaan INSTALLED_APPS
  
- Mukauta asiakkaiden nimien näyttöä hallintaliittymässä
  > crm/models.py
  
  > class Customer(models.Model):
    name = models.CharField(max_length=160)

    def __str__(self):
        return self.name
  
- Käynnistä palvelin ja lisää asiakkaita hallintaliittymän kautta
  >./manage.py runserver

- Asenna Apache WSGI-moduuli
  >sudo apt-get -y install libapache2-mod-wsgi-py3
  
- Tarkista, että luotu syntaksi on ok ja käynnistä Apache uudelleen
  > /sbin/apache2ctl configtest
  
  > sudo systemctl restart apache2

- Poista DEBUG-tila käytöstä ja määritä ALLOWED_HOSTS
  > cd -> cd publicsites/"nimi"/ -> micro "nimi"/settings.py
  
  > DEBUG = False
  
  > ALLOWED_HOSTS = ["localhost", "nimi"]

- Kerää staattiset tiedostot

- Tarkista, että Apache palvelee Django-projektia

- Tarvittaessa tee vianetsintää käyttäen Apache- ja Django-lokkeja




## Tehtävät

### Oman koneen tiedot

AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

RAM: 16,0 Gt

64-bittinen käyttöjärjestelmä, x64-suoritin

Windows 10 Pro, versio 22H2

##


Aloitin tarkastamalla, miltä localhost näyttää selaimessa.

![image](https://github.com/RonjaVee/smial/assets/148786247/840ca3aa-a701-48e3-b2ef-8ef6c0f6742e)


Katsoin, mistä lähteestä index.html luettiin, ja siellä näkyikin aikaisemman tehtävän hattu.example.

![image](https://github.com/RonjaVee/smial/assets/148786247/af543439-a686-4df7-a48f-43ddc7133a09)


Laitoin päälle ronjaesim.com:in, sillä halusin varmistaa, että asiat toimivat niin, että ymmärrän, mitä tapahtuu, kun teen muutoksia. Sain selaimeen näkymään haluamani tekstin.

![image](https://github.com/RonjaVee/smial/assets/148786247/b04a3816-1410-4819-8aea-812fcae18b1c)

![image](https://github.com/RonjaVee/smial/assets/148786247/2d36d2d0-9fd6-4755-9d97-15f99eebcfe6)

![image](https://github.com/RonjaVee/smial/assets/148786247/2ff9395c-7cb5-40e9-8ee8-cf609364e4c3)

Lähdin sitten toteuttamaan Djangon käyttöönottoa käyttäen pohjalla tätä ronjaesim.com:ia, mutta myöhemmin tajusin, ettei uudessa projektissa saa olla pistettä, joten luodessani Djangolla myöhemmin uutta projektia, se sai nimeksi pelkkä ronja.

![image](https://github.com/RonjaVee/smial/assets/148786247/8d8df696-317e-4e8a-8282-0aa1aebc7b79)

Tarkistin, että konfiguraatiotiedosto on kunnossa.

![image](https://github.com/RonjaVee/smial/assets/148786247/08c5167e-bac9-4e76-8efa-287b6e818cdb)

Loin uuden virtualenvin.

![image](https://github.com/RonjaVee/smial/assets/148786247/ae604672-a30e-4c3d-a461-4df288f90fe3)

Loin uuden hakemiston virtuaaliympäristöön.

![image](https://github.com/RonjaVee/smial/assets/148786247/a529c4e7-28b4-4ee6-9f6a-cecaea954a86)

Siirryin luomaani virtuaaliympäristöön.

![image](https://github.com/RonjaVee/smial/assets/148786247/595f89aa-2816-477a-b3d1-d45354323deb)

Loin requirements.txt -tiedoston, jonne kirjoitin django, ja tarkistin vielä catilla, että siellä lukee mitä pitääkin.

![image](https://github.com/RonjaVee/smial/assets/148786247/148e46c9-84eb-4c6e-81f5-aea939bdcf8d)

Sitten latasin Djangon, ja versio näytti oikealta, eli asennus onnistui.

![image](https://github.com/RonjaVee/smial/assets/148786247/19ea351e-07df-423f-ab9d-cdefed4d7f01)

![image](https://github.com/RonjaVee/smial/assets/148786247/e6f65d47-ce37-457b-9e0f-33e232716a53)

Tässä kohti minulla tuli ongelmia projektin luomisessa, ja syötin ChatGPT:lle "django-admin startproject ronjaesim.com causes an error ronjaesim.com is not a valid project name". Vastaukseksi sain, ettei projektinimessä saa olla pistettä.

![image](https://github.com/RonjaVee/smial/assets/148786247/5ce2b854-46a6-438f-bdf1-0eceecc92be5)

Tässä välissä sekoilin hetken kokeillen vähän kaikkea, mutta homma jatkoi etenemistään, kun aloitin uuden projektin "ronja".

![image](https://github.com/RonjaVee/smial/assets/148786247/35c633cb-e7f5-4f72-8220-c41f76a39b4c)

Koska punaisessa tekstissä oli kehoitus käyttää komentoa python manage.py migrate, suoritin komennon tässä kohtaa.

![image](https://github.com/RonjaVee/smial/assets/148786247/08cad852-12b5-4944-b906-c24eac52a425)


Käynnistin palvelimen, ja sain rakettisivun näkyviin osoitteessa 127.0.0.1:8000.

![image](https://github.com/RonjaVee/smial/assets/148786247/00b13344-d369-4f39-af5d-d9a554c5a3d8)

![image](https://github.com/RonjaVee/smial/assets/148786247/b55fb79f-27aa-46f3-892d-0e0965b4509f)

Sitten suoritin Karvisen ohjeen mukaisesti migraatiokomennot, mutta havaitsin, että komennot toimittivat samaa asiaa, kuin aikaisemmin punaisella tekstillä lukenut komento.

![image](https://github.com/RonjaVee/smial/assets/148786247/ff834533-8169-4ae8-aacf-775c7e18f509)

Sitten loin uuden superuserin. Salasana meinasi vahingossa jäädä tyhjäksi klikkausvirheen takia, mutta onneksi se ei ollut sallittua.

![image](https://github.com/RonjaVee/smial/assets/148786247/0d1fecf1-1ff4-4278-957e-828870a28642)

![image](https://github.com/RonjaVee/smial/assets/148786247/9b1c6512-a508-4ab8-a7bf-c9a5a9c831f6)

Tässä vaiheessa selaimessa näkyi seuraavaa, ja olin varma, että jokin oli pahasti pielessä.

![image](https://github.com/RonjaVee/smial/assets/148786247/49b6e56c-edad-424c-9aec-07efd5398d73)

Jatkoin kuitenkin Karvisen ohjeen mukaan luomaan customer databasea lisäämällä modelsit ja rekisteröimällä adminin.

![image](https://github.com/RonjaVee/smial/assets/148786247/5b27cf3e-cd29-4bc7-a741-ce1fb5eabe6e)

![image](https://github.com/RonjaVee/smial/assets/148786247/3e4a68af-68df-4e09-9023-a9548e1b2bd3)

![image](https://github.com/RonjaVee/smial/assets/148786247/37752430-1912-414e-bea2-102619c588be)

Nyt selaimessa näkyi se, mitä pitääkin, ja pääsin kirjautumaan adminina.

![image](https://github.com/RonjaVee/smial/assets/148786247/b52d4291-e77d-4e5c-86bd-8065d61fa870)

Customers-kohtaa ei näkynyt, joten tarkastin crm.admin/py:n, ja sieltä löytyikin kirjoitusvirhe (models-kohdasta s-kirjain). 

![image](https://github.com/RonjaVee/smial/assets/148786247/ea90c16a-3cec-4644-8d0e-8183e0b20c70)

![image](https://github.com/RonjaVee/smial/assets/148786247/8fe2bdbf-bace-41db-ace9-8a6cc94c5e7a)

Vielä tilanne ei korjaantunut, ja tarkistin vielä crm/models.py:n ja annoin migraatiokomennot. 

![image](https://github.com/RonjaVee/smial/assets/148786247/59734e67-0f0b-4e56-acf6-8abe342d69ba)

Sivu näytti edelleen samalta. Korjasin vielä uudestaan ohjeen mukaan, mutta sekään ei korjannut tilannetta.

![image](https://github.com/RonjaVee/smial/assets/148786247/28d04d65-565c-4af2-ab69-ecae5ae175b1)

Sitten huomasin ohjeesta kohdan, joka jäi suorittamatta. Kun laitoin ronja/settings.py -tiedostoon crm:n INSTALLED_APPS -kohtaan ja päivitin tietokannat, ja homma eteni.

![image](https://github.com/RonjaVee/smial/assets/148786247/c22d5949-beed-4958-8d64-b2f647621d62)

![image](https://github.com/RonjaVee/smial/assets/148786247/7c11838e-5f4d-448b-b43c-b459f7feb051)



### Lähteet


Kurssi: Tero Karvinen, 2024: Linux Palvelimet 2024 alkukevät, [https://terokarvinen.com/2024/linux-palvelimet-2024-alkukevat/](https://terokarvinen.com/2024/linux-palvelimet-2024-alkukevat/)

Karvinen, Tero. Django 4 Instant Customer Database Tutorial. 13.2.2022. [https://terokarvinen.com/2022/django-instant-crm-tutorial/](https://terokarvinen.com/2022/django-instant-crm-tutorial/)

Karvinen, Tero. Deploy Django 4 - Production Install.13.2.2022. [https://terokarvinen.com/2022/deploy-django/?fromSearch=django](https://terokarvinen.com/2022/deploy-django/?fromSearch=django)

OpenAI: ChatGPT, versio 3.5. 4.3.2024




