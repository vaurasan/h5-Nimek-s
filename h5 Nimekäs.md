# h 5 Nimekäs

#### Oma Host kokoonpanoni:

| Komponentti | Kuvaus | Lisätiedot |
| :---        |    :----:   |          ---: |
| Emolevy | MSI B550-A PRO | ATX, AM4 |
| Prosessori   | AMD Ryzen 9 5900X | 12-Core 3.70 GHz |
| RAM   | G.Skill  Ripjaws V |  32GB (4x8GB) DDR4 3600MHz, CL 16, 1.3  |
| Näytönohjain   | Sapphire PULSE AMD Radeon RX 7900 GRE        | 16GB     |
| Kovalevy   | Kingston 1TB        | A2000 NVMe PCIe SSD M.2      |
| Kovalevy   | Crucial 512GB        | MX100 SSD     |
| Kovalevy   | Crucial 256GB        | MX100 SSD     |
| Virtalähde   | Asus 750W TUF Gaming Gold        | ATX 80 Plus      |
| Kotelo   | Phanteks Enthoo Pro       |  Full Tower      |

Käyttöjärjestelmä: Windows 11 Pro 23H2

## aa) Tämä ei kuulu tehtävänantoon 

*20.9.2024 klo 16:55*

#### Edellisenä läksynä vuokrasin DigitalOceanista palvelimen, joka sijaitsee Saksassa. Nyt kun viime oppitunnilla käytiin läpi SSH-avaimella kirjautuminen, vuokraan palvelimem UpCloudista, koska haluan kotimaisen palvelimen.

Aluksi käyn DigitalOceanissa poistamassa aiemmin vuokraamani "Dropletin"

![digitalDroplet](https://github.com/user-attachments/assets/461941dc-b62e-4858-a40e-b6fd76662dbf)

Nyt, kun vanha palvelin on tuhottu, on aika käydä luomassa SSH-avainpari virtuaalikoneelleni luennolla tekemieni muistiinpanojen avulla:

![sshohje](https://github.com/user-attachments/assets/45a43c56-d71e-4a39-8db5-55fd8bb6004f)

Luonnin jälkeen käyn kopioimassa julkisen avaimen UpCloud-palvelimen luontia varten.

![historia](https://github.com/user-attachments/assets/fa90b43d-ea7d-44d7-b740-1fd5adfc0b77)

UpCloud haluaa aluksi varmistaa että en ole robotti:

![captcha](https://github.com/user-attachments/assets/88e77d01-bf39-493c-ab9d-33ce5fcf458c)

Aloitetaan palvelimen vuokraaminen: ``+Deploy a new server``, valitsen sijainniksi Helsinki, halvin mahdollinen 3€/kk maksava palvelin riittää mainiosti, sillä se on parempi kuin kalliimpi halvin palvelin DigitalOceanissa.

![halvin](https://github.com/user-attachments/assets/aa565685-5175-4d7c-9c4e-498f260b6ac0)

Luonnollisesti valitaan Debian Linux käyttöjärjestelmäksi. Jätetään varmuuskopiot ja muut ylimääräiset palvelut pois. Lisätessä SSH-avainta ilmeni pieni ongelma, en ollut tajunnut, että koko litania tulee kopioida, eikä ainoastaan hämärän näköinen kirjoitus.

![sshokkey](https://github.com/user-attachments/assets/a7cd5cc2-98d3-4ebe-b684-6ad077e7641b)

Pienen perus-säädön jälkeen sain palvelimen toimintaan, nyt täytyy tehdä pienimuotoinen sijoitus UpCloudille, jotta palvelimeni pysyy hengissä.

![upCloudi](https://github.com/user-attachments/assets/7fa3fc10-3dae-4084-af82-81213623d342)

Nyt laitan palvelimen tulille ja samat alkusäädöt, kuin aiemmassa läksyssä. Mikäli ongelmia ei ilmene, en tähän enää vaihe vaiheelta kirjaa kaikkea.

*klo 17:25, aikaa kului 30min*

*root*-käyttäjänä pääsin sisälle palvelimeen luomaan käyttäjätunnuksen ja antamaan sille tarvittavat oikeudet, mutta yhdistämisessä on ongelmia. Täytyy lukea [täältä](https://upcloud.com/resources/tutorials/use-ssh-keys-authentication) lisää ongelman ratkaisemiseksi.

![failedConnect](https://github.com/user-attachments/assets/06fa17b0-9fca-4a03-9404-7a9d99c54899)

*21.9.2024*

Jätin homman sikseen, kun olin jo väsynyt päivästä. Tänään aamulla kävin säätämässä uudelleen. Menin ensin UpCloudin sivuilta "console" näkymään, kun olin onnistunut vaihtamaan SSH-avaimen lennosta ja lukitsemaan itseni ulos. UpCloudilla on onneksi tämmöinen palvelu, josta pääset selaimella palvelimelle sisään käyttämällä salasanaa, jolla kirjaudutaan UpCloudin nettisivuille.

![Consolee](https://github.com/user-attachments/assets/83904dea-aa39-4698-8c38-839ad50d931d)

Hyödynsin tätä [ohjetta](https://upcloud.com/resources/tutorials/regaining-access-to-a-server-that-was-deployed-using-ssh-keys)

Consolen avulla pystyin muokkaamaan palvelimen SSH-kansion tiedostoja. ``sudo nano /etc/ssh/sshd_config``, sieltä muutin ensin *.conf tiedoston pois käytöstä, laitoin salasanakirjautumisen päälle, sekä sallin SSH-avaimella kirjautumisen, joka oli mystisesti mennyt pois päältä. Tämän jälkeen lähetin palvelimelle vielä oman SSH-public-avaimen komennolla ``ssh-copy-id santeri@94.237.35.220``, kävin muuttamassa *.conf tiedoston takaisin sallituksi, nyt saatoin kirjautua palvelimelle ilman salasanaa. 

![ilmansala](https://github.com/user-attachments/assets/972a582f-90d6-4017-ae72-68912c3da92b)

Tämän jälkeen tein perus asennukset ``sudo apt-get update``, ``sudo apt-get install ufw micro apache2``, tein palomuuriin reiät ``sudo ufw allow 22/tcp``, ``sudo ufw allot 80/tcp``, laitoin palomuurin päälle ``sudo ufw enable``

## a) Kotisivu
#### Tehtävä: Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. Jos sinulla on oikea palvelin Internetissä, kannattaa käyttää sitä. Käytä name based virtual hosting tekniikkaa. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.

*21.9.2024 klo 13:34*

Toisella kurssilla tehdään parhaillaan kotisivuja, jotka myöhemmin lisään tänne. Nyt kuitenkin teen hyvin yksinkertaiset html-testisivut.

Lähden muistelemaan aiemmista tehtävistä, ajoin seuraavat komennot, samalla laitoin micro-editorin oletukseksi

![histapache](https://github.com/user-attachments/assets/cd2d0c4e-90cf-4b08-8f07-719b58964684)

Tässä vaiheessa kirjasin publicsites/santerivauramo.com:iin:

![publicsites](https://github.com/user-attachments/assets/85a46afe-abb1-4e35-bade-a9715d4cde12)

~/publicsites/santerivauramo.com$ kansiossa luon index.html tiedoston komennolla ``micro index.html``, lähden rakentamaan aiemman testisivun päälle, lisään vain linkit kahteen muuhun sivuun samassa kansiossa. Katson vielä ohjeita html:n kirjoittamiseen [täältä](https://www.w3schools.com/html/). Validoin koodin [täällä](https://validator.w3.org/nu/#textarea). Index näyttää tältä:

![indexi](https://github.com/user-attachments/assets/a07ffdc9-e54d-4296-9f1a-4b0cbc7ed0ea)

Tässä vaiheessa sivu ei edes toimi, jotakin on unohtunut. Kokeilen ``sudoedit /etc/hosts`` ja lisään santerivauramo.com:n sinne. (myöhemmin tajusin, että tämä oli nimipalvelua simuloidessa tarpeellinen, ei tässä)

![edithosts](https://github.com/user-attachments/assets/ff631608-49a5-433b-8624-85355bcc8f59)

Kuten kuvassa lukee, täytyy tämän toimiakseen käydä ``/etc/cloud/templates/hosts.debian.tmpl``:ssä lisäämässä tiedot myös sinne. Kävin myös [tämän](https://www.codingcommanders.com/LAMP/apache_default_page.php) ohjeen mukaan poistamassa apachen perus index.html:n ja santerivauramo.com näyttää nyt tältä:

![indexiOn](https://github.com/user-attachments/assets/5a20da86-1f9c-4651-9fe1-02bf2920c010)

Ei ihan vielä se mitä haetaan. Luen asioita [täältä](https://www.veeble.org/kb/how-to-setup-apache-to-host-a-website-in-linux/) ja myös [täältä](https://stackoverflow.com/questions/1484595/how-to-resolve-var-www-copy-write-permission-denied). Kävin luomassa /var/www kansioon santerivauramo.com kansion, vaan eipä ollut oikeuksia, joten annoin itselleni oikeudet

![chmod777](https://github.com/user-attachments/assets/3c0628d3-cd2a-487e-b85c-4fc54fc8ab14)

Kävin luomassa public_html kansion ja santerivauramo.com.conf tekstitiedoston

![comconf](https://github.com/user-attachments/assets/0fd3683d-7b1f-40e0-845d-61eda5584140)

Eipä ollut tarkoitus luoda public_html kansiota, vaan tekstitiedosto. ``rm -r public_html/``, eli poistan kansion ja luon public_html tekstitiedoston ``micro public_html``, sinne laitan seuraavaa: 

![htmlekatoka](https://github.com/user-attachments/assets/eb4efdbf-aeaf-4147-aeb5-53cdd887f968)

Järjen mukaan tämän pitäisi toimia, kun teen samaan kansioon eka.html ja toka.html tiedostot. Nyt olen saanut apachen kohtalaiseen solmuun:

![imagesolmussa](https://github.com/user-attachments/assets/4e0f2b48-3380-4abc-8d21-afc1c01b0812)

Pistää silmään rivi jossa lukee ``AH00526: Syntax error on line 3 of /etc/apache2/sites-enabled/santerivauramo.com.conf:``, täytynee mennä muokkaamaan ``/etc/apache2/sites-enabled/santerivauramo.com.conf``

Kävin poistamassa tuon koko tiedoston, muuten en saanut apachelle tehtyä mitään, nyt pystyy taas potkimaan demonia. Loin tiedoston uudestaan seuraavilla tiedoilla:

![imnanovirtual](https://github.com/user-attachments/assets/f1570e08-d655-4d52-a901-dc32dcd152dc)

santerivauramo.com sanoo: "404 Not Found". Kello on nyt 15:15, pidän pienen tauon ja katson samalla videon: https://www.youtube.com/watch?v=1CDxpAzvLKY.

*klo 15:45* jatkan vielä hetken ennen ruokailua ja lenkkiä.

https://httpd.apache.org/docs/2.4/vhosts/ Täältä löytyi komento ``apachectl -S``, joka näyttää seuraavaa

![imagerrorias](https://github.com/user-attachments/assets/7c431cd3-d5fa-4e4e-8750-42584a4d3c9b)

*klo 16:05, tauko*

*klo 18:35* lenkin ja suihkun jälkeen sain uutta virtaa ranteisiin. Yritän https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-20-04 tämän ohjeen avulla tehdä uusiksi tekemättömän.

![consoleoikeus](https://github.com/user-attachments/assets/d8c286a4-b641-4326-8a8a-5d7ef37d33da)

Loin /var/www kansioon omien sivujen kansion, jonne loin public_html-kansion, tämänhän loin jo aiemmin, mutta ymmärsin ohjeet väärin. Seuraavaksi annoin itselle oikeudet muokata kyseistä kansiota ja loin samanlaisen index.html tiedoston minkä aiemmin loin muualle. Muutin ``sudo micro /etc/apache2/sites-available/santerivauramo.com.conf``:sta seuraavanlaisen:

![servernamealias](https://github.com/user-attachments/assets/87cf48ea-10a8-4d7d-a5bd-a3439a3b26fb)

Nyt demonin potkaisun jälkeen pääsin sivuille. Olin jo aiemmin sallinut ``sudo a2ensite santerivauramo.com.conf``:n, ja disabloinut default conffin, joten niitä ei tarvinnut enää nyt tehdä.

![Ekatoimii](https://github.com/user-attachments/assets/20e452a2-a6ab-4571-ba97-fa6d82f601bb)

Nyt vaan kopioin html:t kahteen tiedostoon, joten saan linkit toimimaan. www.santerivauramo.com

Huomasin että vasta ``sudo chmod -R 777 /var/www/`` komento antoi luvan muokata tiedostoja normaalin käyttäjän oikeuksin.

Loin kansioon siis ``index.html``, ``eka.html``, ja ``toka.html``-tiedostot. Sisällöt näyttävät kutakuinkin kaikissa tältä:

![sivuthtml](https://github.com/user-attachments/assets/3dbbd079-1c2e-40fc-ade4-33a66c977845)

Piti vielä muokata linkit näyttämään tältä, jotta ne toimivat:

![linkit](https://github.com/user-attachments/assets/babc40c2-a32d-47b1-b285-3560772bce08)

Jostain syystä windowsin chromella ei nyt toimi tuo sivu, mutta kännykällä pääsin ja kaikki linkit toimivat.

*klo 19:18* ei tullut hienoja ja aikaa kului, paljon tässäkin oppi asioita, parempi tehdä virheet tässä vaiheessa, homma jatkuu aikaisintaan seuraavana iltana

## b) Alidomain

#### Tehtävä: Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com).

Aloitan lukemalla ensin A-tietueesta ja CNAME-tietueesta, ennen kuin laitan kellon juoksemaan. Ensin googlasin mikä on tietue englanniksi, koska sitä ei ole tullut aiemmin vastaan, vastaus: record. Namecheapin domainpalvelun omaavana, hain tietoa hakusanalla "A-record namecheap" ja löysin varsin hyödyllisen ohjesivun: https://www.namecheap.com/support/knowledgebase/article.aspx/319/2237/how-can-i-set-up-an-a-address-record-for-my-domain/.

*22.9.2024 klo 17:44*

Kirjaudun Namecheap palveluun ja menen "Domain List", ja sieltä "Manage", ja "Advanced DNS", sama mistä lisättiin nimipalveluun palvelimen IP-osoite alunperin. En ole ihan varma tämän toiminnasta, mikä voisi mennä pieleen, kokeilen tällaisella nimellä:

![arecord](https://github.com/user-attachments/assets/909b9c38-b6c1-4f09-be23-33c52359e1a3)

Menin palvelimelleni ja tein ``/var/www/linuxkurssi-a/public_html/`` kansion ja sinne ``index.html`` tiedoston.

![linuxatietue](https://github.com/user-attachments/assets/099b6dac-3b44-4ddc-89a0-967553e15171)

Kopioin myös .conf tiedoston ja muutan sieltä tietoja:

![tiedotarecord](https://github.com/user-attachments/assets/f05fde87-cc26-44be-a4c9-35c017524601)

Nyt kun menen https://linuxkurssi-a.santerivauramo.com/ sivulle, tulee sama index.html sivu, joka aiemmin, eli ei toimi näin. Käyn muuttamassa tuon /linuxkurssi-a kansiossa olevan html-tiedoston joksikin muuksi, kuin index.html. ``mv index.html testi-a.html``, nyt kokeilen uudestaan nettisivua. Ei toimi vieläkään, täytyy odotella ja samalla lukea CNAME-tietueesta lisää ja palata asiaan.

*klo 18:03*



## Otsikko


## Lähteet

Nair, N. 2024. How to setup Apache Web Server to host a website in Linux. Luettavissa: https://www.veeble.org/kb/how-to-setup-apache-to-host-a-website-in-linux/. Luettu 21.9.2024<br>
Stackoverflow. Keskustelu. Luettavissa: https://stackoverflow.com/questions/1484595/how-to-resolve-var-www-copy-write-permission-denied. Luettu 21.9.2024
UpCloud. Faq. Luettavissa: https://upcloud.com/resources/tutorials/use-ssh-keys-authentication. Luettu 20.9.2024<br>
UpCloud. How to regain access to a server that was deployed using SSH keys. Luettavissa: https://upcloud.com/resources/tutorials/regaining-access-to-a-server-that-was-deployed-using-ssh-keys. Luettu 21.9.2024<br>
Validator. W3Scools. Luettavissa: https://validator.w3.org/nu/#textarea. Luettu 21.9.2024<br>
W3Schools. HTML. Luettavissa: https://www.w3schools.com/html/. Luettu 21.9.2024

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html<br>
Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com<br><br>
Kirjoittanut <em>Santeri Vauramo</em>, 2024
