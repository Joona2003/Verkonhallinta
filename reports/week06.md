ZABBIX

0. Johdanto

Zabbix on avoimen lähdekoodin valvontajärjestelmä, jolla voidaan seurata esimerkiksi palvelimia, verkkolaitteita ja palveluita. Sen avulla voidaan kerätä tietoa järjestelmien toiminnasta, näyttää sitä dashboardeilla sekä luoda hälytyksiä ongelmatilanteista. Zabbixia käytetään erityisesti IT-ympäristöjen keskitettyyn valvontaan ja mahdollisten ongelmien havaitsemiseen.


1. Tutustuminen Zabbixiin ja termien selitys

Hosts

- Hostit ovat virtuaalisia tai fyysisiä laitteita, palveluita tai kokonaisuuksia joita halutaan valvoa ja seurata.

Templates

- Templatet ovat valmiita valvonta mittareita joita voidaan käyttää hostien valvonnassa.

Monitoring

- Monitoring on koko järjestelmän jatkuvaa valvontaa, jolla kerätään tieto analysoitavaksi. Monitoring näkymässä seurataan reaaliajassa dataa.

Dashboards

- Dashboardin avulla kerätään yhteen kaikki valvontatiedot ja mittarit. Kyseessä on siis ns. Työpöytä.

Alerts

- Alerts tekee hälytyksiä tai automaattisia toimia, jos jokin asetettu raja-arvo ylitetään. Hälytysten avulla ylläpitäjien ei tarvitse jatkuvasti tuijottaa työpöytiä.

Reports

- Reports on historiallista ja koottua tietoa valvotun ympäristön tilasta. Sieltä näkyy esim triggerit, audit logit, jne.



2. Web1, branch-client ja db1 lisääminen Hostiksi.


Lisäsin Web1, branch-clientin ja db1 -kontit seurattavaksi Zabbixilla ja määräsin Zabbix agentin seuraamaan ja välittämään konttien tietoja.

Zabbix agent2 tiedostosta piti mennä muokkaamaan oikeat ip osoitteet että yhteys pelaa.

Zabbix sai yhteyden kaikkiin kontteihin

Kuva kaikista lisätyistä laiteista imgaes-kansiossa nimellä "kaikkilaitteet"



3. Valvontamittarien analyysi

Nimi | Arvo | Selitys

CPU Usage | 1,5 % | Arvio kertoo kuinka paljon prosessoria käytetään sillä hetkellä esimerkiksi toimintojen pyörittämiseen. tätä arvoa on hyvä seurata jotta tiedetään kuormittaako jokin prosessoria liikaa.

Memory utilization | 36% | Tällä seurataan välimuistin (Ram) käyttöä. Hyvä pitää silmällä koska tämä kertoo milloin jokin saattaa kuormittaa välimuistia liikaa, joka voi aiheuttaa koneen kaatumisen. Myös vieressä olevia disk read/write arvoja kannattaa seurata.

Memory Usage | 1.1% | Tällä voidaan seurata levyn kuormitusta. Tämä on tärkeää jotta tiedetään paljonko levyllä on kuormitusta ja saadaan kirjoitusnopeus ylös.

Network traffic: received ja sent | 4.34kbps, 11.17kbps | Tällä seurataan verkossa liikkuvaa dataa, miten dataa saapuu ja lähtee verkon kautta. Tätä on hyvä seurata jotta saadaan ajoissa tieto mahdollisesta pakettihyökkäyksestä tietoon sekä voidaan seurata verkon liikennettä tarkemmin.

System Uptime | 5h 36min | Tätä seuraamalla pystytään katomaan onko kontti/kone ollut kauankin päällä ja pystyssä. Hyvä seurata jotta voidana nähdä jos kone kaatuu yhtäkkiä.



4. Dashboardin luominen

Loin dashboardin Web1 Muistin käytöstä, CPU kuormasta, levytilan käytöstä, verkkoliikenteestä sekä kaikkien kolmen kontin tilasta (uptime).

Kuva dashboard näkymästä images-kansiossa nimellä "Dashboard"


5. Triggerien luonti

Loin kaksi triggeriä, CPU-kuormitus ja Levytilan määrä. 

CPU-kuormituksen ehtona on että kuorimituksen määrä nousee yli 80% 2 minuutiksi. Jos ehto ylittyy, triggeri laittaa varoituksen eli vakavuusluokka on "Warning"

Levytilan määrän ehtona on alle 20% kokonaislevytilasta jäljellä. Jos ehto ylittyy, heittää triggeri varoituksen tästä käyttäjälle.

6. Hälytyksen simulointi


Ajoin kuormitusta prosessorille komennolla:

stress --cpu 8 --timeout 180


Sain triggerin toimimaan ja siitä tuli ilmoitus "problems" välilehdelle. Kuva images kansiossa nimellä "kuormitustrigger".


7. Häiriötilanne

Pysäytin web1 zabbix agent2 ja seurasin tilannetta. Zabbixissa ei tullut mitään ilmoitusta muuta kuin "ZBX" muuttui punaiseksi. Tälläiselle tilanteelle ei ollut nähtävästi triggeria valmiina, mikä on mielestäni kummallista. Dashboardissa näky kuinka data ei tule enään mitareihin.


8. Yhteenveto työkaluista

Tein yhteenvedon tekstinä sillä taulukko ei jostain syystä näy MD tiedostossa hyvin.

SNMP

SNMP:n avulla voidaan kerätä tietoa esimerkiksi verkkolaitteista ja palvelimista. SNMP ei itsessään tarjoa dashboardeja, vaan sen keräämää tietoa voidaan käyttää muissa valvontajärjestelmissä. Hälytyksiä voidaan tehdä esimerkiksi SNMP Trap -viesteillä. SNMP:n käyttöönotto on yleensä melko helppoa perusvalvontaan, mutta asetukset riippuvat valvottavasta laitteesta. SNMP skaalautuu hyvin erityisesti verkkolaitteiden valvontaan, ja sitä käytetään paljon yritysten verkkoinfrastruktuureissa.

 Prometheus

Prometheus kerää mittareita yleensä HTTP-yhteyden kautta. Sen avulla voidaan seurata esimerkiksi palvelimien suorituskykyä, prosesseja ja verkkoliikennettä. Dashboardeja voidaan tehdä esimerkiksi Grafanalla. Hälytyksiä voidaan toteuttaa Alertmanagerin avulla. Prometheuksen käyttöönotto vaatii yleensä Prometheus-palvelimen ja tarvittavat Exporterit. Se skaalautuu hyvin suuriin ympäristöihin ja sitä käytetään paljon esimerkiksi pilvi ja kontti ympäristöissä.
 Zabbix

Zabbix on kokonaisvaltainen valvontajärjestelmä, jolla voidaan kerätä tietoa esimerkiksi Zabbix-agenteilta, SNMP:n avulla ja muilla menetelmillä. Zabbix sisältää omat dashboardit sekä triggerit ja hälytykset. Käyttöönotto vaatii hostien, agenttien ja triggerien määrittämistä, joten se on hieman monimutkaisempi kuin pelkkä SNMP:n käyttöönotto. Zabbix soveltuu hyvin myös suuriin ympäristöihin ja sitä käytetään paljon yritysten IT-infrastruktuurin valvonnassa.

 Yhteenveto

SNMP soveltuu erityisesti verkkolaitteiden valvontaan. Prometheus soveltuu hyvin palvelimien, konttien ja pilviympäristöjen mittareiden keräämiseen. Zabbix puolestaan tarjoaa kokonaisvaltaisen valvontaratkaisun, jossa tiedonkeruu, dashboardit, hälytykset ja triggerit ovat samassa järjestelmässä.


9. Pohdinta


Mitä hyötyä keskitetystä valvonnasta on?

- Keskitetystä valvonnasta on hyödtyä siten, että kaikki oleellinen on käden ulottuvilla. Näät kaiken oleellisen heti sekä pystyt suorittamaan toimintoja samasta paikkaa.

Mitkä mittarit ovat mielestäsi tärkeimpiä?

- Mielestäni tärkeimmät mittarit ovat CPU kuormitus, levyn käyttö sekä verkonkäyttö. Näilä voidan seurata perustietoja laajasti mitää tapahtuu.

Millaisista tilanteista ylläpitäjän pitäisi saada hälytys?

- Ylläpitäjän pitäisi saada hälytys silloin, kun jokin raja-arvo ylittyy niin huomattavasti että se saattaa vaikuttaa koko ympäristön toimintaan negatiivisesti. Myös jos se voi aiheuttaa kaatumisen tai isompaa vahinkoa niin ilmoitus on tärkeä saada.

Missä tilanteissa käyttäisit Prometheusta?

Käyttäisin Prometheusta erityisesti palvelimien ja konttien suorituskyvyn ja mittareiden seurantaan. Se sopii hyvin esimerkiksi CPU, muistin, levytilan ja verkkoliikenteen seuraamiseen. Prometheus on hyvä valinta myös silloin, kun ympäristössä on paljon muuttuvia palveluita ja tarvitaan paljon tarkkaa mittausdataa.

Missä tilanteissa käyttäisit Zabbixia?

Käyttäisin Zabbixia silloin, kun halutaan valvoa koko IT-ympäristöä keskitetysti. Se on hyvä vaihtoehto myös silloin, kun tarvitaan valmiit dashboardit, triggerit ja hälytykset samaan järjestelmään.

Mitä valvontatoimintoja lisäisit tähän ympäristöön?

- Ei tule päällimäisenä mieleen mitään lisättävää. Ehkä vähän nopeammat shortcutit vaikka dashboardiin jos ongelmia tulee. Ilmoitus mittariin että "problem" jos siinä datassa tulee triggeri.
