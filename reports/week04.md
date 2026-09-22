1. Johdanto

Infrastructure as Code (IaC) tarkoittaa Palvelimien, verkkojen, ympäristöjen sekä tallennustilan käyttöönottoa ja hallintaa automaattiusesti koodia hyödyntämällä. Tällöin ei tarvitse itse määritellä ja tai kirjoitaa joka kerta itse koodia, vaan esim. Ansiblea käytettäessä valmiit komennot haetaan playbookkeja hyödyntäen.

Automaatio ja IaC muuttavat perinteistä palvelimien ylläpitoa siten, että tavanomaisen ylläpitäjän enään tarvitse manuaalisesti korjata vikaa vaan koodin muokkaamisella ja automaatiolla pystytään ratkaisemaan ongelma nopeammin.

Ansiblen rooli tässä automaatiossa on toimia työkaluna konfiguraationhallinnassa. Ansiblen tärkein rooli on palvelimien ja ohjelmistojen konfigurointi playbookkien avulla.


2. Inventory


Ansible Inventory sisältää harjoitusympäristön laitteet, palvelimet ja monitorointipalvelut. Inventoryssa on kolme reititintä (r1, r2 ja r3), kolme asiakaslaitetta (client1, attacker ja branch-client), kaksi palvelinta (web1 ja db1), monitorointipalvelut Prometheus, Grafana, Zabbix ja cAdvisor sekä Ansible-hallintapalvelin.

Laitteet on jaettu ryhmiin niiden käyttötarkoituksen perusteella. Esimerkiksi "routers" sisältää kaikki reitittimet, "clients" asiakas-laitteet ja "servers" eri palvelimet. Lisäksi inventoryssa on esimerkiksi "monitoring"-ryhmä monitorointipalveluille ja "management"-ryhmä hallintapalvelimelle.

Inventoryssa käytetään myös loogisia ryhmiä, kuten "user_network", "server_network" ja "branch_office". Näiden avulla laitteita voidaan ryhmitellä myös niiden verkon tai sijainnin perusteella.

Ryhmien sisällä voidaan käyttää "children"-rakennetta. Esimerkiksi "linux_hosts" sisältää ryhmät "clients", "servers", "monitoring" ja "management". Tämän ansiosta Ansible-komento voidaan suorittaa kaikille näille laitteille käyttämällä vain yhtä ryhmän nimeä.

Ryhmistä on hyötyä erityisesti Ansible-playbookeissa. Playbook voidaan kohdistaa esimerkiksi kaikkiin reitittimiin käyttämällä hosts: routers tai kaikkiin Linux-koneisiin käyttämällä hosts: linux_hosts. Ryhmille voidaan myös määrittää erilaisia yhteysasetuksia. Reitittimet käyttävät network_cli-yhteyttä, kun taas Linux-koneet käyttävät SSH-yhteyttä.

Ryhmien avulla homma pysyy selkeänä ja laitteita voidaan hallita tehokkaasti ilman, että jokainen laite täytyy määritellä erikseen jokaisessa playbookissa.

3. Ensimmäinen Playbook

Siirryin hakemistoon 

- cd /ansible/playbooks

ja suoritin playbookin

- ansible-playbook -i ../inventory.ini ping.yml


Playbookilla testattiin Ansible-yhteyksiä HAMK laboratorioympäristön eri laitteisiin. Web1, db1, branch-client, client1 ja attacker toimivat onnistuneesti. Prometheus-, Grafana-, Zabbix- ja cAdvisor-konteissa SSH-yhteys ei onnistunut, koska portti 22 ei ollut käytettävissä. Ansible-kontissa ongelmana oli väärä salasana. Reitittimien testaus ei onnistunut, koska Ansiblelta puuttui Paramiko-kirjasto.


4. Playbookkien lukeminen

Molemmissa playbookeissa käytetään useita Ansible-moduuleja eri tehtäviin. SNMP-playbookissa käytetään esimerkiksi apt`
-moduulia pakettien asentamiseen, copy-moduulia SNMP-asetustiedoston luomiseen ja service-moduulia SNMP-palvelun käynnistämiseen ja hallintaan. Lisäksi shell-moduulilla tarkistetaan, että SNMP-prosessi on käynnissä, ja debug-moduulilla näytetään tarkistusviesti. Node Exporter -playbookissa käytetään esimerkiksi apt, file, get_url, unarchive, copy, shell, uri ja debug -moduuleja. Niillä asennetaan tarvittavat paketit, luodaan hakemisto, ladataan ja puretaan Node Exporter sekä käynnistetään ja tarkistetaan se.

Molemmissa playbookeissa käytetään myös vars-muuttujia. SNMP-playbookissa muuttujana on snmp_community, jonka arvoksi on määritetty public. Muuttujaa käytetään SNMP-asetustiedostossa. Node Exporter -playbookissa käytetään node_exporter_version-muuttujaa, jonka avulla määritetään ladattavan Node Exporterin versio. Muuttujien avulla asetuksia on helpompi muuttaa ilman, että koko playbookia tarvitsee muokata.

SNMP-playbookissa käytetään handlers-lohkoa SNMP-palvelun uudelleenkäynnistämiseen. Kun snmpd.conf-asetustiedostoa muutetaan, tehtävässä oleva notify: restart snmpd kutsuu handleria. Handler käynnistää SNMP-palvelun uudelleen, jotta uudet asetukset tulevat käyttöön. Handleria ei suoriteta turhaan, jos asetustiedostossa ei ole tapahtunut muutoksia.

Node Exporter -playbookissa ei käytetä handleria, koska Node Exporter käynnistetään suoraan omassa tehtävässään. Tehtävä pysäyttää mahdollisen vanhan prosessin ja käynnistää Node Exporterin uudelleen. Tässä playbookissa ei myöskään muuteta erillistä palvelun asetustiedostoa, jonka muuttuminen vaatisi handlerin käyttämistä.



5. Oman playbookin asennus

Päätin tehdä vaihtoehdon A, eli Ngix web-palvelimen. Rakensin playbookin rakenteen noudattaen ylemmän tehtävän rakennetta ja hyödyntäen netistä löytyviä valmiita pätkiä koodia.



KOODIN RAKENNE:

---
- name: Install web server
  hosts: web1
  become: true

  tasks:

    - name: Update package cache
      apt:
        update_cache: yes

    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Create index.html
      copy:
        dest: /var/www/html/index.html
        content: |
          <html>
          <head>
            <title>HAMK Web Server</title>
          </head>
          <body>
            <h1>Web server: {{ inventory_hostname }}</h1>
            <p>Server is running with Nginx.</p>
          </body>
          </html>

    - name: Start nginx
      shell: |
        pkill nginx || true
        nginx

    - name: Verify web server
      uri:
        url: http://localhost
        status_code: 200

    - name: Show verification result
      debug:
        msg: "Web server is running on {{ inventory_hostname }}"


Ensimmäinen tuloste kun yritin ajaa playbookkia oli aikaisemmalla versiolla:

TASK [Start and enable nginx] ******************************************************
fatal: [web1]: FAILED! => {"changed": false, "msg": "Service is in unknown state", "status": {}}


Tämä johtui siitä että service-komento piti vaihtaa shell-komentoon.

Nyt Tuloste oli oikea ja web1 web-palvelin lähti toimimaan:

PLAY [Install web server] **********************************************************

TASK [Update package cache] ********************************************************
ok: [web1]

TASK [Install nginx] ***************************************************************
ok: [web1]

TASK [Create index.html] ***********************************************************
ok: [web1]

TASK [Start nginx] *****************************************************************
changed: [web1]

TASK [Verify web server] ***********************************************************
ok: [web1]

TASK [Show verification result] ****************************************************
ok: [web1] => {
    "msg": "Web server is running on web1"
}

PLAY RECAP *************************************************************************
web1                       : ok=6    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0



Testasin vielä web1 kontin sisällä komennolla että web palvelin näkyy oikein:

 curl http://localhost

 ja tuloste oli:

 curl http://localhost
<html>
<head>
  <title>HAMK Web Server</title>
</head>
<body>
  <h1>Web server: web1</h1>
  <p>Server is running with Nginx.</p>
</body>
</html>


Kaikki siis toimii oikein.

6. Ansiblen tietojen dokuentointi taulukkoon

Suoritin komennon ja mukkasin sitä koska inventory on eri paikassa omassa repositoriossa: 

ansible all -i /ansible/inventory.ini -m setup




Taulukko:

käyttöjärjestelmä: 24.04 Ubuntu

IP-osoite: Ei löydy (tyhjä)

prosessorien määrä: 1 prosessori ja 6 ydintä ja 12 säijettä

muistin määrä: 7590mb




7. ANalyysi ja vertaus


Käsintehdyt asennukset ovat huomattavasti hitaampia ja riskialttiimpia virheille kun Ansiblella tehdyt playbookit. Niillä saadaan nopeutettua mnfiguroimista sekä asennusta, ja ne voidaan muokata omaan käyttön sopiviksi. Käsintehdyt asennukset ovat hienotarkempaa, mutta ne sopivat vain pienempiin asennuksiin.

Automaatio mahdollistaa nopeamman käyttöönoton sekä isompien kokonaisuuksien konfiguroinnin. On välttämätöntä että isommat kokonaisuudet, kuten useammat palvelimet ja laitteet konfiguroidaan playbookkeja hyödyntäen. Jos tämän tekisi manuaalilla tavalla, kestäisi konfiguroimisessa huomattavasti pidempää ja virheitä saattaa esiintyä epähuomiossa.

8. Yhteenveto

Opin tässä harjoituksessa Ansiblen käyttöä, playbookkien hyödyntämistä konfiguroinneissa sekä niden luomista. Harjoitus antoi hyvän pohjan ymmärtämiselle, miksi valmiit konfigurointi tiedostot ovat kustannus ja aikatehokkaampia kuin manuaali näpyttely.


