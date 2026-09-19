WEEK 03 Raportointi



1. Johdanto

Prometheus on järjestelmän valvontaan ja hälyttämiseen perustuva avoimen lähdekoodin ohjelmisto. Se ei tavanomaiseen tapaan odota tiedon saapumista, vaan käy itse noutamassa tiedot "scrape" perjaatteella HTTP_päätepisteistä. Tiedot tallennetaan sen jälkeen aikasarjoina, jonka avulla ne voidaan tunnistaa metrisen nimen ja arvojen mukaan. Tällä mahdolistetaan tarkka suodattaminen ja teitojen ryhmittely. Prometheuksen ohella käytetään usein oheisia komponentteja kuten Node exporter, PromQL, Alertmanager ja Grafana. Prometheuksen keräämä tieto saadaan esille Grafanan kautta, joka mahdollistaa datan visualisoinnin "dashboardien" avulla.

Monitotointi on datan jatkuvaa keräämistä, analysointi sekä vertailua ja tietojen visualisiointia. Monitoroinnilla voidaann näyttää esim "dashboardeissa" järjestlemän tietoja ja tilaa ilman, että jokaista tietoa tarvitsee alkaa itse anaysoimaan.



Monitorointi on tärkeää koska sillä varmistetaan sovellusten toimintavarmuus, turvallisuus ja suorituskyky.




2. Node Exporterin asennus ja käyttöönotto


Kirjaudutaan Web1 koneelle:

- docker exec -it clab-hamk-verkonhallinta-golden-web1 bash

Asennetaan työkalut komenolla:

- apt update
- apt install wget tar -y


Selvitetään uusin Node Exporterin versio, tässä kohtaa se on 1.12.1 joten sillä mennään. Asennetaan se komennolla:

- wget https://github.com/prometheus/node_exporter/releases/download/v1.12.1/node_exporter-1.12.1.linux-amd64.tar.gz

Asennuksen jälkeen puretaan paketti komennolla:

- tar xvf node_exporter-*.linux-amd64.tar.gz

Kun purku on valmis siirrytään hakemistoon (huomaa että alemmassa komennossa on oikea versio):

- cd node_exporter-1.12.1.linux-amd64


Kun hakemistoon on siirrytty, käynnistetään node exporter komennola:

- ./node_exporter


Jätetään monitorointi auki.


2. Noden exporterin testaus ja tarkistus

Avataan uusi Terminaali (powershellissä) ja kirjaudutaan taas sisälle web1:

- docker exec -it clab-hamk-verkonhallinta-golden-web1 bash

Kokeillaan että Node exporter vastaa:

- curl http://localhost:9100/metrics

Node exporter vastaa, näkyy suuri määrä mittareita kuten "node_cpu_seconds_total" sekä "node_disk_writes_merged_total".

Otin kuvakaappauksen tästä ja se löytyy "images" kansiosta nimellä "ExporterTest"


2.1 Prometheuksen testaus

 Avataan Prometheus komennolla:

- http://localhost:9090.

Avataan "status" -> "targets". Web1 näkyy tilassa "Up". Kuva näkymästä löytyy images kansuiosta nimellä "PrometheusPalvelin".


2.2 Grafanan testaus


Kirjaudutaan Grafanaan ja avataan se:

- http://localhost:3000/

Grafanassa sisällä olessa lisätään uus yhteys vasemmalta valikosta "Connections" -> "add new connection". Etsitään Prometheus ja lisätään "Server URL" - kohtaan osoiteeksi "http://prometheus:9090"

Yhteys on onnistui ja "curl" meni perille. Onnistuneesta yhteydestä löytyy kuva "images" kansiosta nimellä "PrometheusYhteys".



3. Dashboardien luominen

Nyt luodaan Dashboard ja siihen paneelit mitkä valvovat Web1-koneen prosessorin, muistin, levytilan, saapuvan- ja lähtevän verkkoliikenteen tilaa. Tässä hyödynnetään aikaisemmin asennettua Node Exporteria tiedon keräämisessä.


Grafanassa luodaan uusi Dashboard kohdasta "dashboards" -> "Create new dashboard".

Nimetään dashboard "Golden Topology Monitoring". Kun dashboard on luotu niin lisätään sinne uusi paneeli jolle annetaan nimeksi "CPU Usage %".


Tiedot se saa kun promQL sijoittaa:

- 100 - (avg by(instance)
(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)



Sitten "Run Query" (sininen nappi). lopuksi oikeasta yläkulmasta "Save"

Nyt Näkyy dashboardissa Web1 Noden keräämä CPU kuormitus Prosentteina.

Sitten luodaan ylemmän perjaatteen mukaa toinen paneeli nimellä "Memory Usage %"


Komento Queryyn on: 

- (node_memory_MemTotal_bytes -
 node_memory_MemAvailable_bytes)
/
node_memory_MemTotal_bytes
* 100

Sitten sama Proseduuri kun ylempänä ja lopuksi "Save".


Seuraavaksi luodaan uusi näkymä levyn käytölle. Tälle nimeksi "Disk Usage %".

Query tälle on: 

100 -
(
node_filesystem_avail_bytes
/
node_filesystem_size_bytes
* 100
)


Vikaksi luodaan vielä kaksi paneelia, samalla perjaatteella kuin ylemmät. Nimet ovat "Network Receive" ja "Network Transmit"

Nimensä mukaan toinen mittaa saapuvaa verkkoliikennettä ja toinen lähtevää.




4. Kuormituksen generointi

Kuormitin ohjeiden mukaisesti levyä komennoilla:

- dd if=/dev/zero of=testfile.img bs=1M count=500

ja CPU:ta:

- yes > /dev/null


Huomasin piakkoin kuinka prosessorin  ja levun käyttö kasvoi huomattavasti dashboardia seuraamalla. Prosessorin kuormitus kävi noin 80 - 90 % tasolla jonkun aikaa, kun taas levy noin 50 - 60 % tasolla. Muutos oli huomattava verrattuna kuormittamattomiin arvoihin jotka huitelehtivat huomattavasti pienempinä molemmissa. Verkkoliikenne pysyi kokoajan samana, eikä samanalaista piikkiä näkynyt. Network receive ja Transmit ovat molemmat vakaalla tasolla.

Näyttökuva muuttuneista paneeleista löytyy images-kansiosta nimeltä "Grafanamuutos"



5. SNMP VS Prometheus



1. Tiedonkeruu:

Prometheus kerää tiedon aktiivisesti "vetämällä" (Pull), eli palvelin vierailee säännöllisesti kohteiden HTTP-sivuilla lataamassa kaikki tiedot kerralla selkeänä tekstinä.

SNMP tekee perinteiset kyselyt (poll) ja hälytykset, joissa tiedot haetaan UDP-paketteina numeeristen OID-tunnisteiden avulla tai laite lähettää hälytyksen itse suoraan palvelimelle.


2. Käyttöönotto:

Prometheuksen käyttöönotto on on monimutkaisempi. Node exporterin asennus sekä konfigurointi kohdelaitteeseen ja dashboardin luominen grafanaan vaaditaan. 

SNMP ei vaadi "fyysistä" mittaristoa näyttämiseen, esim grafana. SNMP asennus on tämän takia nopeampaa.



3. Mittarien määrä:

SNMP visualisointiin on mahdollista saada erilaisia mittareita millä luetaan OID-arvoja. Valmiiksi SNMP:n kanssa ei tule mitään mittareita mitä hyödyntää.

Prometheus ja Grafan kautta saa valmiita mittareita jotka saa jalostettua tarpeisiin. Ne ovat helpompia lukea ja tulevat valmiina paketteina kunhan PromQL -kyselyn muokkaa tarpeita vaativaksi.


4. Visualisointi:

SNMP ei itsessään tarjoa kunnollista graafista visualisointia, vaan tarvitaan erillinen järjestelmä.

Prometheus voidaan yhdistää Grafanaan, jossa mittareista voidaan tehdä helposti graafeja ja dashboardeja. Mittarit ovat muokattavissa sekä niitä voi lisätä aina lisää eri ominaisuuksille.


5. Hälytysmahdollisuudet:

SNMP Hälytykset vaativat yleensä erillisen monitorointijärjestelmän SNMP varten.

Prometheuksen kanssa voidaan käyttää Alertmanageria hälytysten tekemiseen ja lähettämiseen.


6. Soveltuvuus pilviympäristöihin:

SNMP Soveltuu hyvin esimerkiksi verkkolaitteiden valvontaan, mutta ei ole yhtä joustava dynaamisissa ympäristöissä.

Prometheus Soveltuu paremminpilvi- ja konttiympäristöihin, joissa palvelimia ja palveluita voidaan luoda ja poistaa nopeasti.


6. Pohdinta


Opin harjoituksesta Prometheuksen käytön, yhdistyksen Grafanaan sekä erot Prometheuksen ja SNMP:n välillä. Grafanan käyttö  sekä dashboardin luominen ja näkymien lisääminen tuli tutuksi. Myös kyky lukea PromQL -kyselyitä ja lukea saatua dataa kehittyi harjoituksen aikana. Prometheuksen ja Grafanan välisen suhteen ymmärtäminen auttaa jatkossa tulevissa harjoituksissa sekä tehtävissä.




1. Mitä hyötyä Prometheuksesta on verrattuna SNMP:hen?

Prometheuksen hyötynä on se, että sillä voidaan kerätä palvelimista paljon erilaisia mittareita ja tallentaa niitä aikajärjestyksessä. Prometheus toimii hyvin yhdessä Grafanan kanssa, jolloin tietoja voidaan tarkastella selkeinä graafeina ja dashboardeina. SNMP on enemmän kyselyihin perustuva ratkaisu ja sitä käytetään paljon esimerkiksi verkkolaitteiden monitorointiin. SNMP:n mukana ei tule valmista graafista näkymää.

2. Millaisia mittareita ylläpitäjän kannattaa seurata jatkuvasti?

Ylläpitäjän kannattaa seurata ainakin prosessorin käyttöä, muistin käyttöä, levytilan käyttöä ja verkkoliikennettä. Myös palveluiden toimivuudesta ja palvelimen kuormituksesta on hyödyllistä saada tietoa. Näin mahdolliset ongelmat voidaan huomata ennen kuin ne aiheuttavat suurempia häiriöitä.

3. Mitä tietoa dashboardisi tarjoaa ylläpitäjälle?

Dashboard näyttää palvelimen tärkeimpiä tietoja helposti luettavassa muodossa. Siitä voidaan nähdä prosessorin, muistin ja levyn käyttö sekä verkon tulevan- ja lähtevän liikenteen määrä. 

4. Mitä uusia mittareita lisäisit dashboardiin?

Lisäisin järjestelmän uptime-ajan. Lisäksi olisi hyödyllistä seurata palveluiden toimintaa, jotta mahdollisesti kaatuneet palvelut huomattaisiin nopeasti.

5. Miten monitorointitiedosta voisi olla hyötyä vianetsinnässä?

Monitorointitiedosta voitaisiin nähdä, milloin ongelma on alkanut ja mitä palvelimella tapahtui juuri ennen ongelmaa. Esimerkiksi jos prosessorin käyttö on noussut yhtäkkiä lähes sataan prosenttiin, voidaan tutkia mikä aiheutti kuormituksen. Myös muistin, levytilan ja verkkoliikenteen muutokset voivat auttaa löytämään vian syyn. Historiatiedon avulla voidaan verrata palvelimen normaalia toimintaa ongelmatilanteeseen.
