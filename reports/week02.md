# Week 2 – SNMP

## 1. Johdanto

SNMP (Simple Network Management Protocol) on protokolla, jota käytetään verkkolaitteiden ja palvelimien valvontaan. Sen avulla voidaan kerätä tietoa esimerkiksi laitteen nimestä, käyttöjärjestelmästä, käyttöajasta ja verkkorajapinnoista.

## 2. Asennus

SNMP-agentti asennettiin `web1`, `db1` ja `branch-client` -laitteille:

```bash
apt update
apt install snmp snmpd -y
```

SNMP konfiguroitiin tiedostossa `/etc/snmp/snmpd.conf` lisäämällä:

```text
rocommunity public
```

Palvelu käynnistettiin uudelleen:

```bash
service snmpd restart
```

Palvelun tila tarkistettiin komennolla:

```bash
service snmpd status
```

Tuloksena oli:

```text
* snmpd is running
```

## 3. Kerätyt tiedot

`web1`:n järjestelmän nimi:

```bash
snmpget -v2c -c public web1 sysName.0
```

```text
SNMPv2-MIB::sysName.0 = STRING: web1
```

Järjestelmän kuvaus:

```bash
snmpget -v2c -c public web1 sysDescr.0
```

```text
SNMPv2-MIB::sysDescr.0 = STRING:
Linux web1 6.18.33.2-microsoft-standard-WSL2
#1 SMP PREEMPT_DYNAMIC Thu Jun 18 21:54:43 UTC 2026 x86_64
```

Käyttöaika:

```bash
snmpget -v2c -c public web1 sysUpTime.0
```

```text
DISMAN-EVENT-MIB::sysUpTimeInstance =
Timeticks: (218399) 0:36:23.99
```

Myös `db1` ja `branch-client` vastasivat SNMP-kyselyihin.

| Laite         | Nimi          | Käyttöjärjestelmä | Uptime     |
| ------------- | ------------- | ----------------- | ---------- |
| web1          | web1          | Linux / WSL2      | 0:36:23.99 |
| db1           | db1           | Linux / WSL2      | 0:00:43.30 |
| branch-client | branch-client | Linux / WSL2      | 0:03:56.25 |

## 4. Verkkorajapinnat

`web1`:n verkkorajapinnat selvitettiin komennolla:

```bash
snmpwalk -v2c -c public web1 ifDescr
```

Tulokset:

```text
IF-MIB::ifDescr.1 = STRING: lo
IF-MIB::ifDescr.2 = STRING: eth0
```

Rajapintoja löytyi yhteensä kaksi:

* `lo` – loopback-rajapinta
* `eth0` – verkkorajapinta, joka yhdistää laitteen verkkoon

## 5. OID-analyysi

| OID-objekti    | Tarkoitus                                         |
| -------------- | ------------------------------------------------- |
| `sysName.0`    | Laitteen nimi                                     |
| `sysDescr.0`   | Järjestelmän kuvaus ja käyttöjärjestelmän tietoja |
| `sysUpTime.0`  | Kertoo SNMP-agentin käyttöajan                    |
| `ifDescr`      | Kertoo verkkorajapintojen nimet                   |
| `ifOperStatus` | Kertoo verkkorajapinnan toimintatilan             |

OID-objektien avulla SNMP-manageri voi pyytää laitteelta tiettyä tietoa.

## 6. Pohdinta

1. **Mitä hyötyä SNMP:stä on verkonhallinnassa?**
   SNMP:n avulla voidaan valvoa useita laitteita keskitetysti ja kerätä niistä tietoa automaattisesti.

2. **Mitä tietoa SNMP:n avulla voidaan kerätä?**
   Esimerkiksi laitteen nimi, käyttöjärjestelmän tietoja, käyttöaika, verkkorajapinnat ja rajapintojen toimintatila.

3. **Mitä ongelmia yhteisöpohjaisessa SNMPv2:ssa on?**
   SNMPv2c käyttää community string -tunnistetta, joka ei ole salattu. Tässä työssä käytetty `public` ei siksi ole turvallinen tuotantoympäristössä.

4. **Missä tilanteissa käyttäisit mieluummin SNMPv3:a?**
   SNMPv3:a käyttäisin tuotantoverkossa tai tilanteissa, joissa valvontaliikenteen turvallisuus on tärkeää. Se tarjoaa paremman tunnistautumisen ja liikenteen suojauksen.
