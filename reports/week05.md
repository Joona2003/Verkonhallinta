0. Johdanto




1. Wireshark analysi


Porttiskannauksen katsotaan tulleen IP-osoitteesta 172.20.20.10, joka toimi hyökkäävänä osapuolena. Skannauksen kohteena oli web1 palvelin osoitteessa 10.10.20.101. Hyökkääjä käytti kiinteää lähdeporttia 58514 ja lähetti sen kautta jatkuvaa SYN-pakettien virtaa. Testattuja TCP-kohdeportteja olivat muun muassa:
 
56737
2492
1149
3878
49176
12174
5631
2046
6346
5678
12345 
9003
5633 
3052
    
    
Esitetyssä pakettinäkymässä palvelimen lähettämiä vastauksia ei näy lainkaan. Paketin yksityiskohtien tila "Incomplete, SYN_SENT (1)" vahvistaa, että yhteyspyynnöt jäivät ilman vastauksia. Palvelimen mahdolliset RST- tai SYN-ACK-vastaukset voidaan selvittää suodattamalla liikennettä ehdolla ip.src == 10.10.20.101.  

Images kansioon on liitetty kuvakaappaus "Wireshark", joka todentaa skannauksen lähteen, käytetyt kohdeportit ja keskustelun keskeneräisen tilan.


2. DNS ja HTTP liikenne


Loin DNS ja HTTP liikennettä web1 suuntaan



DNS-kyselyt:
Asiakaskone (172.20.20.10) tekee A- ja AAAA-kyselyitä verkkotunnuksille.
- Esimerkki 1: Paketti 13 (Standard query A zalando.com)
- Esimerkki 2: Paketti 23 (Standard query AAAA cars.com)

DNS-vastaukset:
DNS-palvelin palauttaa kysytyt IP-osoitteet tai nimipalvelutiedot.
- Esimerkki 1: Paketti 14 (Standard query response A zalando.com -> 108.156.22.118)
- Esimerkki 2: Paketti 22 (Standard query response A cars.com -> 3.93.126.98)

Käytetyt palvelimet:
- DNS-palvelin: 10.255.255.254
- Asiakaslaite (Client): 172.20.20.10


Tehtävä 5.5 – HTTP-liikenne

HTTP-pyynnöt:
Ei havaittu. Suodattimella 'http' näkymä on tyhjä, sillä HTTP-tason pyyntöjä ei ole lähetetty.

HTTP-vastaukset:
Ei havaittu.

Palvelimet ja havainnot:
Asiakaskone (172.20.20.10) yrittää avata TCP-yhteyttä HTTP-porttiin 80 palvelimelle 10.10.20.101 (Paketti 25). Yhteys epäonnistuu palvelimen vastaamattomuuden vuoksi (Paketit 26-27: TCP Retransmission), minkä seurauksena HTTP-liikennettä ei synny.


3. Loki analyysi


Tarkastelin lokeja:

Lokit näyttävät kaikki kirjautumiset, eri palveluiden kännistymiset sekä virheilmoitukset kuin myös uloskirjautumiset ja ympäristön sulkemisen.

Lokit ovat tallentaneet kaiken ihan alusta asti ja tietoa on huima määrä.


4. Turvallisuus

Miten porttiskannaus näkyi liikenteessä?

Liikenteessä näkyi tiheä sarja yhtäaikaisia TCP SYN -paketteja, jotka lähetettiin yhdestä samasta lähde-IP-osoitteesta (172.20.20.10) ja lähdeportista (58514) useisiin eri kohdeportteihin palvelimelle (10.10.20.101). Yhteyspyynnöt jäivät keskeneräisiksi (SYN_SENT), sillä kolmiteikädenpuristusta ei viety loppuun.   

Miten se näkyi lokeissa?

Verkkoliikennekaappauksessa ja palomuurilokeissa skannaus näkyy poikkeuksellisena määränä lyhyessä ajassa tulleita saapuvia TCP-yhteyspyyntöjä samaan kohde-IP-osoitteeseen eri portteihin. Mikäli palomuuri tai kohdejärjestelmä pudottaa tai hylkää pyynnöt, lokit tallentavat suuren määrän hylättyjä (DROP / REJECT) tai vastattuja (RST-ACK) paketteja.

Mitä hyötyä verkkoliikenteen analysoinnista on?

Verkkoliikenteen analysointi auttaa havaitsemaan poikkeavaa toimintaa (kuten skannauksia tai haittaohjelmaliikennettä), selvittämään tietoturvaloukkauksia, todentamaan verkon ja palvelinten todellisen tilan sekä varmistamaan palomuurisääntöjen toimivuuden.

Miten monitorointia voisi hyödyntää hyökkäysten tunnistamisessa?

Asettamalla automaattisia hälytysrajoja SIEM-järjestelmään tai IDS/IPS-tunkeutumisenhavaitsemisjärjestelmään (esim. hälytys, jos sama IP pyytää yli 10 eri porttia sekunnissa). Realiaikaisen monitoroinnin avulla skannaajan IP-osoite voidaan estää automaattisesti palomuurissa jo ennen kuin mahdollista haavoittuvuutta päästään hyödyntämään.
