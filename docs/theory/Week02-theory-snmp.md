# Miksi verkkoa valvotaan? 

Tietoverkko on yksi organisaation tärkeimmistä teknisistä järjestelmistä. Käytännössä lähes kaikki palvelut ovat tavalla tai toisella riippuvaisia toimivasta verkosta. Verkon kautta käytetään esimerkiksi pilvipalveluita, sähköpostia, tiedostopalveluita, toiminnanohjausjärjestelmiä ja verkkopalveluita. 

Verkon käyttäjät odottavat palveluiden olevan käytettävissä jatkuvasti. Tämän vuoksi verkon toimintaa on seurattava jatkuvasti ja mahdollisiin ongelmiin on pystyttävä reagoimaan nopeasti. 

Verkon valvonnan tavoitteena on: 

varmistaa palveluiden käytettävyys 

havaita häiriöt mahdollisimman nopeasti 

tunnistaa suorituskykyongelmat ennen niiden vaikutusta käyttäjiin 

kerätä tietoa kapasiteetin suunnittelua varten 

helpottaa vianmääritystä 

tukea verkon kehittämistä pitkällä aikavälillä 

Ilman jatkuvaa valvontaa verkon ylläpito perustuu pitkälti arvailuun ja käyttäjien vikailmoituksiin. 



# Verkon ylläpidon haasteet 

Nykyaikainen tietoverkko koostuu tyypillisesti useista eri teknologioista ja järjestelmistä. 

Yksinkertaisessakin ympäristössä voi olla: 

* reitittimiä 
* kytkimiä 
* langattomia tukiasemia 
* palvelimia 
* virtualisointialustoja 
* pilvipalveluita 
* tietoturvalaitteita 
* useita internet-yhteyksiä 

Jokainen näistä voi muodostaa häiriötilanteen lähteen. 

Esimerkiksi käyttäjän näkökulmasta ongelma voi näyttäytyä yksinkertaisesti seuraavasti: 

"Verkko ei toimi." 

Todellisuudessa taustalla voi olla kymmeniä erilaisia syitä. 

Ongelma voi liittyä esimerkiksi: 

* fyysiseen verkkokaapeliin 
* kytkinporttiin 
* väärään VLAN-konfiguraatioon 
* täyttyneeseen verkkoliitäntään 
* DNS-palveluun 
* palvelimen suorituskykyyn 
* virheelliseen reititykseen 
* internet-operaattorin häiriöön 

Mitä suurempi ympäristö on, sitä vaikeampaa järjestelmän kokonaistilan hahmottaminen ilman valvontatyökaluja on. 

 

## Miksi häiriöitä syntyy? 

Vaikka verkko olisi suunniteltu hyvin, häiriöitä syntyy väistämättä. 

Tyypillisiä syitä ovat: 

* Laitteistoviat 

* Laitteiden komponentit kuluvat ajan myötä. 

Esimerkiksi: 

* verkkokortti voi rikkoutua 
* virtalähde voi vioittua 
* levyjärjestelmä voi epäonnistua 
* kuitumoduuli voi lakata toimimasta 

 

## Konfiguraatiovirheet 

Yksi yleisimmistä häiriöiden aiheuttajista on ihmisen tekemä virhe. 

Esimerkiksi: 

* väärä IP-osoite 
* puuttuva reitti 
* virheellinen palomuurisääntö 
* väärä VLAN-määritys 

Pienikin muutos voi aiheuttaa laajoja vaikutuksia koko verkkoon. 

 

## Kapasiteettiongelmat 

Alun perin riittävä verkko voi muuttua kuormituksen kasvaessa hitaaksi. 

Esimerkiksi: 

* käyttäjämäärä kasvaa 
* palveluita lisätään 
* varmuuskopiointi käyttää enemmän kaistaa 
* videoliikenne lisääntyy 

Tällöin palvelu ei välttämättä lakkaa toimimasta kokonaan, mutta sen suorituskyky heikkenee merkittävästi. 

 

## Ohjelmistovirheet 

Verkkolaitteiden käyttöjärjestelmät sisältävät ohjelmistovirheitä samalla tavalla kuin muutkin ohjelmistot. 

Virheet voivat aiheuttaa: 

* yhteyksien katkeamista 
* muistivuotoja 
* suorituskykyongelmia 
* palveluiden kaatumisia 

 

## Ulkoiset tekijät 

Kaikki ongelmat eivät sijaitse organisaation omassa ympäristössä. 

Esimerkiksi: 

* sähkökatkokset 
* internet-operaattorin häiriöt 
* pilvipalveluiden ongelmat 
* palvelunestohyökkäykset 

voivat näkyä käyttäjälle samalla tavalla kuin paikallinen verkkovika. 

 

## Miksi pelkkä käyttäjän vikailmoitus ei riitä? 

Monessa organisaatiossa ensimmäinen merkki ongelmasta on käyttäjän yhteydenotto helpdeskiin. 

Esimerkiksi: 

"Verkkolevy avautuu hitaasti." 

tai 

"Teams pätkii." 

Tällaiset ilmoitukset ovat tärkeitä, mutta niiden perusteella ei vielä tiedetä ongelman syytä. 

Käyttäjä näkee vain oireen. 

Ylläpitäjän tehtävä on selvittää: 

* mikä aiheuttaa oireen 
* missä ongelma sijaitsee 
* kuinka laajalle ongelma vaikuttaa 
* kuinka vakava ongelma on 

Ilman mittausdataa ongelman selvittäminen muuttuu arvailuksi. 


Esimerkkitilanne 

Käyttäjä ilmoittaa: 

"Palvelu toimii erittäin hitaasti." 

Ylläpitäjän on selvitettävä esimerkiksi seuraavat kysymykset: 

**Onko yhteys poikki?**

Jos verkkoyhteys katkeilee, sovellukset voivat vaikuttaa hitailta vaikka varsinainen ongelma olisi verkkokerroksessa. 

**Onko palvelin kuormittunut?**

Jos palvelimen prosessorikuorma on jatkuvasti 100 %, käyttäjä kokee palvelun hitaaksi vaikka verkko toimisi normaalisti. 

**Onko verkkoliitäntä täynnä?**

Jos palvelimen tai reitittimen verkkoliitäntä toimii jatkuvasti lähellä maksimikapasiteettiaan, pakettien määrä kasvaa ja viiveet pitenevät. 

**Onko DNS-palvelussa ongelma?**

Monet sovellukset käyttävät nimipalvelua jatkuvasti. 

Jos DNS-palvelin vastaa hitaasti, käyttäjä voi tulkita ongelman verkkoviaksi tai palvelinviaksi. 

**Vaikuttaako ongelma kaikkiin käyttäjiin?**

Jos ongelma koskee vain yhtä käyttäjää, syynä voi olla paikallinen työasema tai lähiverkkoyhteys. 

Jos ongelma koskee kaikkia käyttäjiä, syy on todennäköisesti keskeisemmässä infrastruktuurissa. 


# Reaktiivinen ja proaktiivinen ylläpito 

Verkon ylläpito voidaan jakaa kahteen toimintamalliin. 

## Reaktiivinen ylläpito 

Reaktiivisessa ylläpidossa toimenpiteisiin ryhdytään vasta, kun ongelma on jo vaikuttanut käyttäjiin. 

Toimintamalli on usein seuraava: 

1. Häiriö tapahtuu. 
2. Käyttäjä ilmoittaa ongelmasta. 
3. Ylläpito aloittaa selvityksen. 
4. Ongelma korjataan. 

Mallin haittapuolena on, että palvelukatko on jo ehtinyt vaikuttaa käyttäjiin. 


## Proaktiivinen ylläpito 

Proaktiivisessa ylläpidossa verkon toimintaa seurataan jatkuvasti mittausten avulla. 

Esimerkiksi: 

* kaistan käyttöaste kasvaa 
* muistin käyttö lisääntyy 
* levytila alkaa loppua 
* verkkovirheet lisääntyvät 

Valvontajärjestelmä voi havaita tilanteen ennen varsinaista häiriötä. 

Tällöin ylläpito voi korjata ongelman jo ennen kuin käyttäjät huomaavat sitä. 

 

Esimerkki 

```text 
Ilman valvontaa: 

     Verkkoliitäntä täyttyy 
             ↓ 
     Yhteydet hidastuvat 
             ↓ 
     Käyttäjät valittavat 
             ↓ 
     Vikaa ryhdytään tutkimaan 
```
Kun tilanne verkonvalvonta työkalun avulla toteutettuna, proaktiivisena mallina: 

```text
Valvonnan avulla: 

     Verkkoliitäntä saavuttaa 80 % käyttöasteen 
             ↓ 
     Valvontajärjestelmä hälyttää 
             ↓ 
     Kapasiteettia lisätään 
             ↓ 
     Käyttäjät eivät huomaa ongelmaa 
```
 

# Miksi mittaaminen on välttämätöntä? 

Verkonhallinnassa tehdyt päätökset tulisi perustaa mitattuun tietoon eikä oletuksiin. 

Mittaamisen avulla voidaan vastata esimerkiksi seuraaviin kysymyksiin: 

* Onko laite käytettävissä? 
* Kuinka paljon verkkoliikennettä kulkee verkossa? 
* Mitkä yhteydet ovat kuormittuneita? 
* Milloin ongelma alkoi? 
* Kuinka vakava ongelma on? 
* Vaikuttaako ongelma yhteen vai useaan käyttäjään? 
* Onko tilanne poikkeuksellinen vai normaali? 

Tämän vuoksi nykyaikaisessa verkonhallinnassa kerätään jatkuvasti tietoa verkkolaitteista, palvelimista ja palveluista. Yksi yleisimmin käytetyistä tiedonkeruumenetelmistä on SNMP (Simple Network Management Protocol), jonka toimintaa tarkastellaan seuraavaksi. 

# Häiriönhallinta (Fault Management) ja Observability

Modernit tietoverkot ja IT-järjestelmät muodostuvat useista palvelimista, verkkolaitteista, pilvipalveluista, sovelluksista ja niiden välisistä riippuvuuksista. Mitä monimutkaisempi ympäristö on, sitä tärkeämpää on kyky havaita häiriöt nopeasti, ymmärtää niiden syyt ja palauttaa palvelut normaalitilaan mahdollisimman vähäisin vaikutuksin.

Häiriönhallinnan tavoitteena on varmistaa järjestelmien käytettävyys, luotettavuus ja suorituskyky. Perinteisesti häiriönhallinta on perustunut erilaisten valvontatyökalujen tuottamiin hälytyksiin, mutta nykyisissä ympäristöissä korostuu myös observability eli järjestelmän havainnoitavuus. Observability auttaa ymmärtämään paitsi sen, että ongelma on olemassa, myös miksi se tapahtuu.

## FCAPS-malli

Tietoliikenne- ja verkkoympäristöjen hallintaa voidaan tarkastella kansainvälisesti tunnetun FCAPS-mallin avulla. Malli jakaa verkonhallinnan viiteen osa-alueeseen:

**Fault (Häiriönhallinta)**

Keskittyy vikojen havaitsemiseen, tunnistamiseen, analysointiin ja korjaamiseen. Tavoitteena on minimoida käyttökatkojen vaikutukset ja palauttaa palvelut mahdollisimman nopeasti.

**Configuration (Konfiguraationhallinta)**

Vastaa laitteiden ja palveluiden asetusten hallinnasta, dokumentoinnista sekä muutosten seurannasta. Konfiguraationhallinnan avulla voidaan esimerkiksi palauttaa toimiva konfiguraatio virheellisen muutoksen jälkeen.

**Accounting (Käytön seuranta)**

Seuraa resurssien käyttöä, käyttäjiä ja mahdollisia kustannuksia. Esimerkkejä ovat verkkoliikenteen mittaaminen tai pilvipalveluiden kustannusseuranta.

**Performance (Suorituskyvyn hallinta)**

Tarkastelee järjestelmien ja verkkojen suorituskykyä. Tavoitteena on havaita mahdolliset pullonkaulat ennen kuin ne aiheuttavat häiriöitä.

**Security (Tietoturvallisuus)**

Keskittyy järjestelmien suojaamiseen, poikkeamien tunnistamiseen sekä tietoturvatapahtumien hallintaan.

Kurssilla keskitytään erityisesti seuraaviin osa-alueisiin:

* Fault Management
* Performance Management
* Configuration Management

Nämä muodostavat käytännössä päivittäisen verkkoylläpidon keskeisimmän osaamisen perustan.

## Häiriönhallinnan prosessi

Häiriönhallinta on järjestelmällinen prosessi, jonka avulla ongelmat ratkaistaan tehokkaasti ja niiden toistuminen pyritään estämään.

1. Häiriön havaitseminen

Ensimmäinen vaihe on poikkeaman tunnistaminen. Häiriö voidaan havaita:

* Valvontajärjestelmän hälytyksenä
* Lokiviestien perusteella
* Suorituskykymittareiden poikkeamina
* Käyttäjän ilmoittamana vikana

Esimerkki:

Palvelin ei vastaa ping-kyselyihin.
CPU-kuorma nousee poikkeuksellisen korkeaksi.
Verkkolaitteen rajapinta menee alas.

Tavoitteena on havaita ongelma mahdollisimman nopeasti ennen kuin käyttäjät kärsivät merkittävistä palvelukatkoista.

2. Häiriön tunnistaminen

Kun häiriö on havaittu, seuraava tehtävä on selvittää mitä on tapahtunut.

Tyypillisiä kysymyksiä ovat:

* Mikä palvelu on häiriintynyt?
* Mitkä järjestelmät ovat vaikutusalueella?
* Milloin ongelma alkoi?
* Onko kyseessä uusi vai aiemmin tunnettu ongelma?

Esimerkiksi verkkopalvelun toimimattomuus voi johtua:

* Verkkoyhteysongelmasta
* DNS-ongelmasta
* Palvelimen kaatumisesta
* Sovellusvirheestä

3. Häiriön analysointi

Analysointivaiheessa etsitään häiriön juurisyy.

Tyypillisiä menetelmiä ovat:

* Lokien tutkiminen
* Mittausdatan analysointi
* Verkkoliikenteen tarkastelu
* Muutoshistorian tarkistaminen

Monissa tapauksissa ongelman syy löytyy äskettäin tehdystä muutoksesta, kuten:

* ohjelmistopäivityksestä
* verkkokonfiguraation muutoksesta
* virheellisestä automaatiosta

Tätä vaihetta kutsutaan usein myös root cause analysis (RCA)-prosessiksi.

4. Korjaaminen

Kun syy on tunnistettu, voidaan toteuttaa tarvittavat korjaavat toimenpiteet.

Esimerkkejä:

* Palvelun uudelleenkäynnistys
* Virheellisen konfiguraation korjaaminen
* Verkkolaitteen vaihto
* Ohjelmistovirheen korjauspäivitys
* Muutoksen peruuttaminen (rollback)

Korjausten jälkeen järjestelmän toiminta tulee varmistaa mittaamalla ja testaamalla palvelun palautuminen normaalitilaan.

5. Jälkianalyysi

Vakavampien häiriöiden jälkeen suoritetaan jälkianalyysi.

Tavoitteena on vastata kysymyksiin:

* Mikä aiheutti häiriön?
* Miksi sitä ei havaittu aikaisemmin?
* Miten vastaava ongelma voidaan estää tulevaisuudessa?
* Tarvitaanko uusia valvontoja tai prosesseja?

Jälkianalyysi on tärkeä osa organisaation oppimista ja jatkuvaa kehittämistä.

6. Dokumentointi

Kaikki häiriöt ja niiden ratkaisut tulee dokumentoida.

Tyypillisesti dokumentaatioon kirjataan:

* Tapahtuman aikajana
* Ongelman kuvaus
* Vaikutukset palveluihin
* Juurisyy (jos selviää)
* Tehdyt korjaustoimenpiteet
* Kehitystoimenpiteet

Hyvä dokumentaatio nopeuttaa tulevien ongelmien ratkaisemista ja tukee organisaation tiedonhallintaa.

## Observability

Perinteinen monitorointi vastaa kysymykseen:

Onko järjestelmä kunnossa?

Observability pyrkii vastaamaan syvällisempään kysymykseen:

Miksi järjestelmä ei toimi odotetulla tavalla?

Observability perustuu kolmeen keskeiseen tietolähteeseen:

### Metrics

Metrikat ovat numeerisia mittauksia järjestelmän toiminnasta.

Esimerkkejä:

* CPU-kuormitus
* Muistin käyttö
* Verkkoliikenteen määrä
* Levyn käyttöaste

Metrikoiden avulla voidaan tunnistaa suorituskykyongelmia ja havaita poikkeamia.

### Logs

Lokit sisältävät yksityiskohtaisia tapahtumatietoja järjestelmästä.

Esimerkkejä:

* Kirjautumiset
* Virheilmoitukset
* Palveluiden käynnistykset
* Konfiguraatiomuutokset

Lokit ovat usein tärkein tietolähde juurisyyn analysoinnissa.

### Traces

Jäljitystiedot kuvaavat yksittäisen palvelupyynnön kulkua useiden järjestelmien läpi.

Niiden avulla voidaan nähdä esimerkiksi:

* Missä vaiheessa sovellus hidastuu
* Mikä palvelukomponentti aiheuttaa virheen
* Kuinka kauan eri käsittelyvaiheet kestävät

Traces ovat erityisen hyödyllisiä hajautetuissa järjestelmissä ja mikropalveluarkkitehtuureissa. Tämän takia kurssilla keskitytään enemmän metriikoiden ja logien käyttämiseen. 




## Miten observability-dataa kerätään? 

Jotta häiriö voidaan havaita, analysoida ja korjata, tarvitaan tietoa siitä, mitä verkossa ja järjestelmissä tapahtuu. Tätä tietoa kutsutaan observability-dataksi. Se koostuu esimerkiksi suorituskykymittauksista, lokeista, hälytyksistä ja verkkoliikenteen tiedoista. Observabilityn tavoitteena on antaa ylläpitäjälle mahdollisuus vastata kysymyksiin: 

* Onko järjestelmä kunnossa?
* Mitä juuri tapahtui? 
* Miksi ongelma syntyi? 
* Miten ongelma voidaan korjata? 


### Tyypillisesti tiedonkeruu muodostaa seuraavan kaltaisen ketjun:

Esimerkiksi kytkin voi havaita verkkorajapinnan menevän alas. Monitorointijärjestelmä saa tiedon, luo hälytyksen ja ilmoittaa asiasta ylläpitäjälle, joka aloittaa häiriönhallintaprosessin. SNMP perustuu manager-agent-malliin, jossa monitorointijärjestelmä kysyy tietoja laitteilta tai vastaanottaa niiden lähettämiä hälytyksiä (traps). [cisco.com], [learningne....cisco.com] 

### Miksi observability-dataa tarvitaan? 

Ilman jatkuvaa tiedonkeruuta ylläpitäjä joutuu odottamaan käyttäjien vikailmoituksia. Tällöin toiminta on reaktiivista. Observability mahdollistaa proaktiivisen ylläpidon, jossa ongelmat havaitaan ennen kuin ne aiheuttavat merkittäviä käyttökatkoja. Observability perustuu tyypillisesti mittareihin (metrics), lokeihin (logs) ja jäljitystietoihin (traces), joiden avulla voidaan ymmärtää järjestelmän toimintaa ja ongelmien juurisyitä. [opentelemetry.io], [opentelemetry.io] 


### Observability-datan tietolähteet 

Nykyaikaisessa ympäristössä monitorointijärjestelmä voi kerätä tietoa useista eri lähteistä. Jokaisella menetelmällä on omat vahvuutensa. 

## SNMP (Simple Network Management Protocol) 

SNMP on verkonhallinnan perinteinen ja edelleen erittäin yleinen tiedonkeruumenetelmä. SNMP:n avulla voidaan lukea verkkolaitteiden ja palvelimien tilatietoja, kuten: 

* CPU-kuorma 
* Muistin käyttö 
* Rajapintojen liikennemäärät 
* Virhelaskurit 
* Laitteiden lämpötilat 

SNMP perustuu agenttiin, joka toimii valvottavassa laitteessa, sekä manageriin, joka kerää tiedot keskitetysti. Lisäksi laite voi lähettää itsenäisesti hälytyksiä eli trap-viestejä merkittävistä tapahtumista. [cisco.com], [learningne....cisco.com] 

Kurssin myöhemmissä harjoituksissa SNMP toimii keskeisenä tekniikkana, jonka avulla mittausdataa kerätään verkkolaitteilta monitorointijärjestelmään. 


## Syslog 

SNMP kertoo yleensä laitteen nykytilan, mutta ei välttämättä selitä miksi jotain tapahtui. 

Tätä varten käytetään Syslogia. 

Syslog on standardoitu lokien siirtoprotokolla, jonka avulla verkkolaitteet, palvelimet ja sovellukset lähettävät tapahtumatietoja keskitetylle lokipalvelimelle. Syslog-viestejä voivat olla esimerkiksi: 

* käyttäjän kirjautuminen 
* palvelun käynnistyminen 
* rajapinnan katkeaminen 
* virheilmoitus 
* tietoturvatapahtuma 

Keskitetty lokien kerääminen mahdollistaa tapahtumien tutkimisen myöhemmin sekä häiriöiden juurisyiden analysoinnin. Syslog on standardoitu RFC 5424 -määrityksessä. [rfc-editor.org], [rfcinfo.com] 

## API 

Monet modernit järjestelmät tarjoavat tietoja ohjelmointirajapintojen (API) kautta. 

Esimerkiksi: 

* Kubernetes 
* VMware vSphere 
* Proxmox VE 
* Pilvipalvelut (Azure, AWS, Google Cloud) 
* Verkkolaitteiden hallintajärjestelmät 

Monitorointijärjestelmä voi hakea tietoja suoraan API-kyselyillä ilman SNMP:tä. API:t mahdollistavat usein huomattavasti laajemman tietomäärän keräämisen kuin perinteiset MIB-pohjaiset SNMP-kyselyt. 

API-pohjainen monitorointi on yhä tärkeämpää erityisesti pilvi- ja virtualisointiympäristöissä. 

## NetFlow 

SNMP kertoo paljonko liikennettä rajapinnalla kulkee, mutta ei sitä, kuka liikennettä aiheuttaa. 

Tätä varten käytetään NetFlow'ta. 

NetFlow kerää verkkoliikenteestä virtoja (flows) ja tuottaa tietoa esimerkiksi: 

* lähdeosoitteesta 
* kohdeosoitteesta 
* käytetystä protokollasta 
* käytetyistä porteista 
* siirrettyjen tavujen määrästä 

NetFlow'n avulla voidaan tunnistaa: 

* suurimmat liikenteen aiheuttajat 
* ruuhkien syyt 
* epätavallinen liikenne 
* tietoturvapoikkeamat 

Tyypillinen NetFlow-ratkaisu koostuu kolmesta osasta: 



NetFlow tarjoaa huomattavasti tarkemman näkymän verkkoliikenteeseen kuin pelkkä SNMP. [en.wikipedia.org], [kentik.com] 

# NetFlow: Verkkoliikenteen virta-analyysi

## Mikä on NetFlow?

NetFlow on verkkoliikenteen analysointimenetelmä, jonka avulla verkkolaitteet muodostavat liikennevirroista (flows) yhteenvetotietoja analysointia varten.

Verkkovirta koostuu paketeista, joilla on yhteisiä ominaisuuksia, kuten:

- Lähde-IP-osoite
- Kohde-IP-osoite
- Lähdeportti
- Kohdeportti
- Käytetty protokolla (TCP, UDP, ICMP jne.)

Toisin kuin paketinkaappausratkaisut (esim. Wireshark), NetFlow ei yleensä tallenna pakettien sisältöä, vaan ainoastaan liikennettä kuvaavia metatietoja. Tämän ansiosta suurten verkkoympäristöjen liikennettä voidaan analysoida tehokkaasti ilman valtavaa tallennustilan tarvetta.

---

## NetFlow-järjestelmän kolme pääosaa

Tyypillinen NetFlow-arkkitehtuuri koostuu kolmesta komponentista:

```text
+-------------------+
|      Exporter     |
| (Verkkolaite)     |
+---------+---------+
          |
          v
+-------------------+
|     Collector     |
|  (Tallennus)      |
+---------+---------+
          |
          v
+-------------------+
|     Analyzer      |
| (Raportointi)     |
+-------------------+
```

---

### 1. Exporter

#### Tehtävä

Exporter on yleensä reititin, kytkin tai palomuuri, jossa NetFlow-toiminto on käytössä.

Sen tehtävänä on:

1. Tarkkailla verkkoliikennettä.
2. Ryhmitellä paketit virroiksi.
3. Laskea virran tunnusluvut.
4. Lähettää tiedot collectorille.

#### Kerättävät tiedot

Tyypillinen virtatietue sisältää:

- Lähde-IP
- Kohde-IP
- Lähdeportti
- Kohdeportti
- Protokolla
- Pakettien määrä
- Tavujen määrä
- Virran aloitus- ja lopetusaika

#### Esimerkki

Käyttäjä avaa selaimella verkkosivun HTTPS-yhteydellä.

Exporter tunnistaa esimerkiksi seuraavan virran:

| Kenttä | Arvo |
|----------|----------|
| Lähde-IP | 192.168.1.50 |
| Kohde-IP | 93.184.216.34 |
| Protokolla | TCP |
| Kohdeportti | 443 |
| Paketteja | 120 |
| Tavuja | 180 000 |

> Exporter ei tallenna varsinaista verkkosisältöä, vaan liikennettä kuvaavan yhteenvedon.

---

### 2. Collector

#### Tehtävä

Collector vastaanottaa exportereiden lähettämät virratiedot.

Sen vastuulla on:

- Datan vastaanotto
- Datan tallennus
- Datan indeksointi
- Historiatietojen ylläpito

Suurissa verkoissa yksi collector voi vastaanottaa tietoja sadoilta tai tuhansilta verkkolaitteilta.

#### Miksi collector tarvitaan?

Jos jokainen verkkolaite säilyttäisi kaiken virratiedon itse, datan analysointi olisi vaikeaa. Collector keskittää tiedot yhteen paikkaan.

#### Esimerkkejä collectoreista

- nProbe
- ElastiFlow
- Akvorado
- Kentik
- SolarWinds NetFlow Traffic Analyzer

---

### 3. Analyzer

#### Tehtävä

Analyzer lukee collectorin tallentamaa dataa ja muuttaa sen helposti ymmärrettävään muotoon.

Analyzer voi tuottaa:

- Raportteja
- Hälytyksiä
- Visualisointeja
- Tilastoja
- Trendejä

#### Tyypillisiä kysymyksiä

Analyzer auttaa vastaamaan esimerkiksi seuraaviin kysymyksiin:

- Mitkä laitteet käyttävät eniten kaistaa?
- Mitä sovelluksia verkossa käytetään?
- Mikä aiheutti verkon ruuhkautumisen?
- Onko verkossa poikkeavaa liikennettä?
- Mihin ulkoisiin palveluihin liikennettä muodostetaan?

#### Esimerkki raportista

| Lähde-IP | Sovellus | Liikenne |
|-----------|-----------|-----------|
| 10.0.0.12 | YouTube | 45 GB |
| 10.0.0.20 | Microsoft Teams | 18 GB |
| 10.0.0.35 | OneDrive | 12 GB |

Raportin perusteella ylläpitäjä voi nopeasti tunnistaa verkon suurimmat kuormittajat.

---

## Käyttökohteet

### Verkon vianmääritys

NetFlow auttaa selvittämään:

- Mikä aiheuttaa ruuhkia
- Mistä liikenne tulee
- Mihin liikenne suuntautuu

### Kapasiteetin suunnittelu

Pitkän aikavälin mittaukset osoittavat:

- Kaistan käytön kasvun
- Kuormituspiikit
- Tarpeen verkkoyhteyksien laajentamiseen

### Tietoturva

NetFlow:lla voidaan havaita:

- DDoS-hyökkäyksiä
- Haittaohjelmien liikennettä
- Epätavallisia yhteyksiä
- Tietovuotoihin viittaavaa suurta ulospäin suuntautuvaa liikennettä

---

## Yhteenveto

NetFlow-järjestelmä koostuu kolmesta pääkomponentista:

### Exporter

- Kerää liikennetiedot verkkolaitteelta.
- Muodostaa virrat (flows).
- Lähettää tiedot collectorille.

### Collector

- Vastaanottaa virratiedot.
- Tallentaa historian.
- Keskittää tiedot analysoitavaksi.

### Analyzer

- Tuottaa raportit ja visualisoinnit.
- Tukee verkonhallintaa.
- Auttaa suorituskyvyn optimoinnissa.
- Tukee tietoturvapoikkeamien tunnistamista.

Näiden kolmen komponentin yhteistyö mahdollistaa tehokkaan verkkoliikenteen seurannan, vianmäärityksen ja tietoturvan valvonnan ilman, että koko verkkoliikenteen sisältöä tarvitsee tallentaa.
---

### Lisälukemista

- [RFC 7011: IP Flow Information Export (IPFIX)](https://datatracker.ietf.org/doc/html/cisco.com/c/en/us/products/ios-nx-os-software/ios-netflow/index.html)
- [Kentik: What is NetFlow?](https://www.kentik.com/kentipedia/what-is-netflow-overview/)
- [Cloudflare Learning Center: Network Flow Monitoring](https://www.cloudflare.com/learning/network-layer/what-is-network-monitoring/)

# Prometheus

Prometheus kerää aikasarjamuotoista mittausdataa palvelimilta ja sovelluksilta.

Sitä käytetään erityisesti:

Linux-palvelimien monitorointiin
Konttiympäristöihin
Pilviympäristöihin

Prometheus mahdollistaa tehokkaat hälytykset ja pitkän aikavälin suorituskykyanalyysin.

# Grafana

Grafana tarjoaa visualisointialustan mittausdatalle.

Sen avulla voidaan rakentaa:

Hallintapaneeleja (dashboards)
Reaaliaikaisia näkymiä
Hälytysjärjestelmiä
Raportteja

Grafanaa käytetään usein yhdessä Prometheuksen kanssa.

# Zabbix

Zabbix on kokonaisvaltainen verkkovalvontaratkaisu.

Se tarjoaa:

Valvonnan
Hälytykset
Raportoinnin
SNMP-tuen
Agenttipohjaisen monitoroinnin

Zabbix soveltuu hyvin organisaatioiden keskitettyyn valvontaan.

Streaming Telemetry 

Verkkojen nopeuksien ja laitemäärien kasvaessa perinteinen SNMP-pollaus ei aina riitä. 

Streaming Telemetry on modernimpi lähestymistapa, jossa laitteet lähettävät tietoa jatkuvana virtana monitorointijärjestelmälle ilman erillisiä kyselyjä. Data voidaan lähettää jopa sekunnin murto-osien tarkkuudella. [blog.paessler.com], [riverbed.com], [cisco.com] 

Perinteinen SNMP toimii näin: 

1     Monitorointi ──► Kysyy tiedon 

2     Laite         ──► Vastaa 

Streaming Telemetry toimii näin: 

1     Laite ──► Lähettää tietoa jatkuvasti 

2             ──► Collector 

3             ──► Analytiikka 

Streaming Telemetryn etuja ovat: 

reaaliaikaisempi näkyvyys 

pienempi viive häiriöiden havaitsemisessa 

tarkempi mittausdata 

parempi skaalautuvuus suuriin ympäristöihin 

Tekniikka on yleistynyt erityisesti datakeskus- ja palveluntarjoajaverkoissa. [blog.paessler.com], [riverbed.com] 

 

# Yhteenveto Observability

Observability perustuu siihen, että järjestelmistä kerätään jatkuvasti tietoa analysointia varten. Tieto voidaan kerätä useilla eri menetelmillä: 

| Menetelmä | Käyttötarkoitus |
|---------------|-------------------|
| SNMP | Laitteiden tila- ja suorituskykytiedot |
| Syslog | Tapahtuma- ja virhelokit |
| API | Modernien järjestelmien hallinta- ja tilatiedot |
| NetFlow | Verkkoliikenteen analysointi |
| Streaming Telemetry | Reaaliaikainen mittausdata |


Kurssin näkökulmasta SNMP muodostaa tärkeän perustan, sillä monet monitorointijärjestelmät hyödyntävät sitä edelleen verkkolaitteiden ja palvelimien valvontaan. Myöhemmissä opinnoissa opiskelija kohtaa myös muita tiedonkeruumenetelmiä, joita käytetään erityisesti moderneissa pilvi-, virtualisointi- ja datakeskusympäristöissä. 

Häiriönhallinnan tavoitteena on havaita ongelmat nopeasti, tunnistaa niiden syyt ja palauttaa palvelut toimintakuntoon mahdollisimman tehokkaasti. FCAPS-mallissa häiriönhallinta muodostaa yhden keskeisistä verkonhallinnan osa-alueista yhdessä suorituskyvyn, konfiguraationhallinnan, käytön seurannan ja tietoturvan kanssa.

Modernissa ympäristössä häiriönhallinta perustuu observability-ajatteluun, jossa metrikat, lokit ja jäljitystiedot muodostavat kokonaiskuvan järjestelmän toiminnasta. Työkalut kuten SNMP, Syslog, Prometheus, Grafana ja Zabbix mahdollistavat poikkeamien havaitsemisen, niiden analysoinnin sekä tehokkaan reagoinnin erilaisiin häiriötilanteisiin. Tämä osaaminen muodostaa perustan nykyaikaiselle verkkopalveluiden ja IT-infrastruktuurin ylläpidolle.

 

## Lisälukemista 

OpenTelemetry Observability Primer 
https://opentelemetry.io/docs/concepts/observability-primer/ [opentelemetry.io] 

Cisco SNMP Overview 
https://www.cisco.com/c/en/us/td/docs/unified_computing/Intersight/IMM_SNMP_Monitoring/b_imm_snmp_monitoring_guide/m_overview_snmp_monitoring.pdf [cisco.com] 

RFC 5424: The Syslog Protocol 
https://www.rfc-editor.org/info/rfc5424/ [rfc-editor.org] 

Kentik: What is NetFlow? 
https://www.kentik.com/kentipedia/what-is-netflow-overview/ [kentik.com] 

Paessler: SNMP vs NetFlow vs Streaming Telemetry 
https://blog.paessler.com/network-streaming-telemetry-monitoring-in-real-time [blog.paessler.com] 


## SNMP Linux-palvelimella 

Linux-palvelimessa SNMP toteutetaan tavallisesti Net-SNMP-ohjelmistolla.

Keskeinen palvelu on:

1     snmpd

Palvelu toimii SNMP-agenttina ja vastaa managerin kyselyihin.

Tyypillinen ympäristö

```text
     SNMP Manager
     srv-monitor
          |
  ---------------------------
  |            |            |
  |            |            |
srv-client1  srv-client2  srv-client3
  |            |            |
 snmpd        snmpd        snmpd
```

Monitorointipalvelin kerää tietoja useilta palvelimilta samanaikaisesti.

### Community

SNMPv1- ja SNMPv2c-ympäristöissä käytetään community string -arvoja.

Esimerkki:

1     public

Community toimii eräänlaisena "salasanana", mutta sitä ei salata verkkoliikenteessä.

Tästä syystä sitä ei suositella tuotantoympäristöihin.

### SNMPv3-käyttäjä

SNMPv3 käyttää käyttäjätunnuksia ja tarvittaessa salausta.

Esimerkiksi:

1     monitor

SNMPv3 mahdollistaa turvallisen monitoroinnin myös verkoissa, joissa liikenteen luottamuksellisuus on tärkeää. [cisco.com], [learningne....cisco.com]

Tämän kurssin Week02-harjoituksessa opiskelija asentaa SNMP-agentin Linux-palvelimelle, määrittää monitorointikäyttäjän ja testaa tiedonkeruuta käytännössä.

## SNMP osana verkonhallinnan kokonaisuutta

SNMP ei ole irrallinen teknologia, vaan osa laajempaa verkonhallinnan kokonaisuutta.

1     Dokumentaatio

2           ↓

3          SNMP

4           ↓

5      Monitorointi

6           ↓

7       Hälytykset

8           ↓

9      Häiriönhallinta

10           ↓

11       Kehittäminen

Verkonhallinta alkaa ympäristön tuntemisesta ja dokumentoinnista. Dokumentoiduista laitteista voidaan kerätä tietoa SNMP:n avulla. Kerätty tieto mahdollistaa monitoroinnin, jonka perusteella syntyy hälytyksiä. Hälytysten avulla havaitaan häiriöt, jotka analysoidaan ja korjataan. Lopuksi kerättyä tietoa käytetään ympäristön kehittämiseen, kapasiteetin suunnitteluun ja automaation rakentamiseen.

# SNMP:n perusteet

SNMP (Simple Network Management Protocol) on verkonhallintaprotokolla, jonka avulla voidaan kerätä tietoa verkkolaitteista, palvelimista ja muista verkkoon liitetyistä järjestelmistä.

SNMP:n avulla voidaan esimerkiksi selvittää:

- laitteen nimi
- käyttöjärjestelmä
- käyttöaika (uptime)
- prosessorin kuormitus
- muistin käyttö
- verkkoliitäntöjen tila
- verkkoliikenteen määrä

SNMP on yksi yleisimmistä verkkovalvonnan tiedonkeruumenetelmistä, ja monet monitorointijärjestelmät hyödyntävät sitä edelleen.

---

# SNMP:n toimintamalli

SNMP perustuu manager-agent-malliin.

```text
             SNMP GET
Manager -----------------> Agent
             Vastaus
Manager <----------------- Agent

                 |
                 v
                MIB
```

## Manager

Manager on järjestelmä, joka kerää tietoa.

Esimerkkejä:

- Zabbix
- LibreNMS
- PRTG
- Observium
- komentorivityökalut (snmpget, snmpwalk)

Manager lähettää kyselyitä valvottaville laitteille.

## Agent

Agentti toimii valvottavassa laitteessa.

Esimerkkejä:

- Linux-palvelin
- reititin
- kytkin
- palomuuri

Linuxissa yleinen SNMP-agentti on:

```bash
snmpd
```

Agentti vastaa managerin lähettämiin kyselyihin.

---

# MIB ja OID

SNMP:n keräämät tiedot sijaitsevat MIB-tietokannassa (Management Information Base).

MIB voidaan ajatella puumaisena tietorakenteena.

```text
iso(1)
└── org(3)
    └── dod(6)
        └── internet(1)
            └── mgmt(2)
                └── mib-2(1)
                    ├── system(1)
                    └── interfaces(2)
```

Jokaisella objektilla on yksilöllinen tunniste, jota kutsutaan OID:ksi (Object Identifier).

Esimerkki:

```text
sysName.0

OID:
1.3.6.1.2.1.1.5.0
```

Sama objekti voidaan kirjoittaa joko nimellä tai numeromuodossa.

```bash
snmpget -v2c -c public web1 sysName.0
```

vastaa käytännössä:

```bash
snmpget -v2c -c public web1 1.3.6.1.2.1.1.5.0
```

Useimmissa tilanteissa nimimuoto on helpompi käyttää.

---

# SNMP-portit

SNMP käyttää UDP-protokollaa.

| Portti | Käyttötarkoitus |
|----------|----------|
| UDP 161 | SNMP-kyselyt |
| UDP 162 | Trap-viestit |

Tyypillisesti monitorointijärjestelmä lähettää kyselyt porttiin 161.

---

# SNMP-kyselyt

SNMP tukee useita kyselytyyppejä.

## GET

Hakee yhden tietyn objektin arvon.

Esimerkki:

```bash
snmpget -v2c -c public web1 sysName.0
```

Palauttaa laitteen nimen.

---

## GETNEXT

Hakee seuraavan objektin MIB-puusta.

Tätä käytetään tiedon selaamiseen ohjelmallisesti.

---

## GETBULK

Hakee useita objekteja yhdellä kyselyllä.

GETBULK vähentää verkkoliikennettä erityisesti suurissa ympäristöissä.

---

# Net-SNMP-komentorivityökalut

Kurssin harjoituksissa käytetään Net-SNMP-työkaluja.

## snmpget

Hakee yhden tietyn OID:n.

Esimerkki:

```bash
snmpget -v2c -c public web1 sysDescr.0
```

---

## snmpwalk

Käy läpi kokonaisen OID-haaran.

Esimerkki:

```bash
snmpwalk -v2c -c public web1 system
```

Palauttaa useita järjestelmätietoja yhdellä komennolla.

---

## snmptranslate

Muuntaa objektin nimen OID-muotoon tai päinvastoin.

Esimerkki:

```bash
snmptranslate sysName.0
```

---

# SNMP-versiot

SNMP:stä on käytössä useita versioita.

| Versio | Turvallisuus |
|----------|----------|
| SNMPv1 | Ei suojausta |
| SNMPv2c | Community String |
| SNMPv3 | Tunnistus ja salaus |

## SNMPv2c

Kurssiharjoituksissa käytetään SNMPv2c-versiota.

Esimerkki:

```bash
snmpget -v2c -c public web1 sysName.0
```

Missä:

```text
-v2c
```

määrittää version.

```text
-c public
```

määrittää community stringin.

Community toimii eräänlaisena tunnisteena, mutta sitä ei salata verkkoliikenteessä.

---

## SNMPv3

SNMPv3 tukee:

- käyttäjätunnistusta
- viestien eheyden tarkistusta
- salausta

SNMPv3 on nykyinen suositeltu vaihtoehto tuotantoympäristöihin.

Kurssilla käytetään SNMPv2c:tä yksinkertaisuuden vuoksi.

---

# Kurssin tärkeimmät OID:t

Seuraavat objektit ovat Week02-harjoituksen kannalta tärkeimpiä.

## Järjestelmätiedot

| OID | Tarkoitus |
|----------|----------|
| sysName | Laitteen nimi |
| sysDescr | Järjestelmän kuvaus |
| sysLocation | Laitteen sijainti |
| sysContact | Yhteyshenkilö |
| sysUpTime | Käyttöaika |

Esimerkki:

```bash
snmpget -v2c -c public web1 sysUpTime.0
```

---

## Verkkorajapinnat

| OID | Tarkoitus |
|----------|----------|
| ifDescr | Rajapinnan nimi |
| ifAdminStatus | Hallinnollinen tila |
| ifOperStatus | Todellinen toimintatila |

Esimerkki:

```bash
snmpwalk -v2c -c public web1 ifDescr
```

Mahdollinen tulos:

```text
lo
eth0
```

---

## Liikennelaskurit

| OID | Tarkoitus |
|----------|----------|
| ifInOctets | Vastaanotetut tavut |
| ifOutOctets | Lähetetyt tavut |

Näitä käytetään verkkoliikenteen mittaamiseen ja grafiikoiden tuottamiseen monitorointijärjestelmissä.

---

# SNMP Linux-palvelimella

Linuxissa SNMP-agentti toteutetaan yleensä Net-SNMP-ohjelmistolla.

Asennus:

```bash
apt update
apt install snmp snmpd -y
```

Palvelun tila:

```bash
service snmpd status
```

Tyypillinen yhteys näyttää seuraavalta:

```text
        SNMP Manager
          ansible

              |
              |
          UDP 161
              |
              |

            web1
           snmpd
```

Manager lähettää kyselyn, ja agentti palauttaa pyydetyn tiedon.

---

# Yhteenveto

SNMP mahdollistaa verkkolaitteiden ja palvelimien tilatietojen keräämisen keskitetysti.

Kurssin harjoituksissa tärkeimmät käsitteet ovat:

- Manager
- Agent
- MIB
- OID
- Community String
- SNMPv2c
- SNMPv3
- snmpget
- snmpwalk

Näiden avulla voidaan kerätä perustiedot verkon laitteista sekä muodostaa pohja myöhemmille monitorointi- ja valvontaratkaisuille.


# Lähteet 

OpenTelemetry Documentation: Observability Primer 
https://opentelemetry.io/docs/concepts/observability-primer/ [opentelemetry.io], [opentelemetry.io] 

Cisco UCS SNMP Monitoring Guide 
https://www.cisco.com/c/en/us/td/docs/unified_computing/Intersight/IMM_SNMP_Monitoring/b_imm_snmp_monitoring_guide/m_overview_snmp_monitoring.pdf [cisco.com] 

Cisco Learning Network: Understanding SNMP 
https://learningnetwork.cisco.com/s/article/Understanding-Simple-Network-Management-Protocol--SNMP [learningne....cisco.com] 

RFC 5424: The Syslog Protocol 
https://www.rfc-editor.org/info/rfc5424/ [rfc-editor.org] 

Kentik: What is NetFlow? 
https://www.kentik.com/kentipedia/what-is-netflow-overview/ [kentik.com] 

Jatkolukemista 

Net-SNMP Project Documentation 
https://www.net-snmp.org/ 

LibreNMS Documentation 
https://docs.librenms.org/ 

Zabbix SNMP Monitoring Documentation 
https://www.zabbix.com/documentation/current/en/manual/config/items/itemtypes/snmp 

RFC 3411: SNMP Framework Architecture 
https://www.rfc-editor.org/rfc/rfc3411 

RFC 3418: Management Information Base (MIB-II) 
https://www.rfc-editor.org/rfc/rfc3418.html 