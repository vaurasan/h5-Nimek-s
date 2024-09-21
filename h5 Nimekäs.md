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


## a) Kotisivu
#### Tehtävä: Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. Jos sinulla on oikea palvelin Internetissä, kannattaa käyttää sitä. Käytä name based virtual hosting tekniikkaa. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.






## Otsikko




## Otsikko


## Lähteet

UpCloud. Faq. Luettavissa: https://upcloud.com/resources/tutorials/use-ssh-keys-authentication. Luettu 20.9.2024<br>
UpCloud. How to regain access to a server that was deployed using SSH keys. Luettavissa: https://upcloud.com/resources/tutorials/regaining-access-to-a-server-that-was-deployed-using-ssh-keys. Luettu 21.9.2024<br>

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html<br>
Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com<br><br>
Kirjoittanut <em>Santeri Vauramo</em>, 2024
