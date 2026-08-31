 Johdanto


Tämän harjoituksen tarkoituksena on selvittää ja dokumentoida virtuaalisen verkkoympäristön rakenne, laitteet, IP-osoitteistus ja reititys. Dokumentointi auttaa hahmottamaan verkon kokonaiskuvaa, mikä on edellytys myöhemmille hallinta-, valvonta- ja vianetsintätehtäville.



TEHTÄVÄ 1.1
Laite	Tarkoitus
r1	    R1toimii linkkinä clientile ja attackerille r2 välilä.
r2	    Keskitinreititin joka yhdistää palvelin-, hallinta- ja etäverkot toisiinsa.
r3	    Etätoimipisteen (branch) reititin.
client1	   Normaali asiakaskone/työasema pääverkossa.
attacker	Hyökkäys-/testauskone turvallisuusharjoituksia varten.
web1	    Web-palvelin palvelinverkossa (srv-br).
db1	        Tietokantapalvelin palvelinverkossa (srv-br).
branch-client	Etätoimipisteen asiakaskone/työasema
ansible	         Automatio- ja konfiguraationhallintapalvelin hallintaverkossa (mgmt-br)
prometheus	      Metriikan keruu- ja valvontapalvelin hallintaverkossa (mgmt-br)
grafana	          Visualisointi- ja raportointityökalu valvontadatalle hallintaverkossa (mgmt-br)
zabbix	          Verkon ja laitteiston valvontajärjestelmä hallintaverkossa (mgmt-br)





TEHTÄVÄ 1.3

Verkko         Tarkoitus   Yhdyskäytävä
10.10.10.0/24  User LAN    10.10.10.1 (tai r1 liitäntä)
10.10.20.0/24  Server LAN  10.10.20.1 (tai r2 liitäntä)
10.10.30.0/24  Branch Office  10.10.30.1 (tai r3 liitäntä)
10.10.99.0/24  Management LAN  10.10.99.1 (tai r2 liitäntä)
10.255.12.0/30 Reitittimien r1 ja r2 välinen runkoverkko  r1 - r2 osoite tältä väliltä
10.255.23.0/30  Reitittimien r2 ja r3 välinen runkoverkko  r2 - r3 osoite tältä väliltä


 Laitteet, yhdyskäytävät ja tarkoitukset seuraavasti:


**10.10.10.0/24**

* Laitteet: client1, attacker
* Yhdyskäytävä: r1
* Tarkoitus: User LAN (käyttäjäverkko)

**10.10.20.0/24**

* Laitteet: web1, db1
* Yhdyskäytävä: r2
* Tarkoitus: Server LAN (palvelinverkko)

**10.10.30.0/24**

* Laitteet: branch-client
* Yhdyskäytävä: r3
* Tarkoitus: Branch Office (etätoimipisteen verkko)

**10.10.99.0/24**

* Laitteet: ansible, grafana, prometheus, zabbix
* Yhdyskäytävä: r2
* Tarkoitus: Management LAN (ylläpito- ja valvontaverkko)

**10.255.12.0/30**

* Laitteet: r1, r2
* Yhdyskäytävä: r1 ja r2
* Tarkoitus: Reitittimien r1 ja r2 välinen runkoyhteys

**10.255.23.0/30**

* Laitteet: r2, r3
* Yhdyskäytävä: r2 ja r3
* Tarkoitus: Reitittimien r2 ja r3 välinen runkoyhteys


TEHTÄVÄ 1.4


**Yhteydet:**
Yhteys löytyy kaikkiin verkkoihin. Ping-testit osoitteisiin 10.10.20.101 (Server LAN) ja 10.10.30.101 (Branch Office) menivät läpi ilman pakettihävikkiä (0% packet loss).

**Liikenteen kulkureitti ja reitittimet:**
Traceroute-komennon tulosteen perusteella liikenne kulkee client1-laitteelta branch-clientille seuraavasti:

1. 10.10.10.1 (Reititin r1 – oletusyhdyskäytävä)
2. 10.255.12.2 (Reititin r2 – runkoverkko)
3. 10.255.23.2 (Reititin r3 – etätoimipisteen reititin)
4. 10.10.30.101 (Kohdelaite branch-client)

---

**Komentojen tulosteet:**

```text
root@client1:/# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0@if14: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 72:aa:f1:ca:10:59 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.20.20.6/24 brd 172.20.20.255 scope global eth0
       valid_lft forever preferred_lft forever
19: eth1@if20: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9500 qdisc noqueue state UP group default
    link/ether aa:c1:ab:82:8a:e0 brd ff:ff:ff:ff:ff:ff link-netnsid 1
    altname clab-o-05031180f95d8850
    inet 10.10.10.101/24 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a8c1:abff:fe82:8ae0/64 scope link
       valid_lft forever preferred_lft forever

root@client1:/# ip route
default via 10.10.10.1 dev eth1
10.10.10.0/24 dev eth1 proto kernel scope link src 10.10.10.101
172.20.20.0/24 dev eth0 proto kernel scope link src 172.20.20.6

root@client1:/# ping -c 4 10.10.20.101
PING 10.10.20.101 (10.10.20.101) 56(84) bytes of data.
64 bytes from 10.10.20.101: icmp_seq=1 ttl=62 time=1.56 ms
64 bytes from 10.10.20.101: icmp_seq=2 ttl=62 time=0.202 ms
64 bytes from 10.10.20.101: icmp_seq=3 ttl=62 time=0.214 ms
64 bytes from 10.10.20.101: icmp_seq=4 ttl=62 time=0.200 ms

--- 10.10.20.101 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3048ms
rtt min/avg/max/mdev = 0.200/0.542/1.555/0.584 ms

root@client1:/# ping -c 4 10.10.30.101
PING 10.10.30.101 (10.10.30.101) 56(84) bytes of data.
64 bytes from 10.10.30.101: icmp_seq=1 ttl=61 time=2.20 ms
64 bytes from 10.10.30.101: icmp_seq=2 ttl=61 time=0.201 ms
64 bytes from 10.10.30.101: icmp_seq=3 ttl=61 time=0.214 ms
64 bytes from 10.10.30.101: icmp_seq=4 ttl=61 time=0.190 ms

--- 10.10.30.101 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3035ms
rtt min/avg/max/mdev = 0.190/0.701/2.200/0.865 ms

root@client1:/# traceroute 10.10.30.101
traceroute to 10.10.30.101 (10.10.30.101), 30 hops max, 60 byte packets
 1  10.10.10.1 (10.10.10.1)  0.531 ms  0.024 ms  0.055 ms
 2  10.255.12.2 (10.255.12.2)  0.241 ms  0.031 ms  0.021 ms
 3  10.255.23.2 (10.255.23.2)  0.262 ms  0.037 ms  0.030 ms
 4  10.10.30.101 (10.10.30.101)  0.141 ms  0.200 ms  0.047 ms

lOPPUTEKSTI

Eniten aikaa verkon dokumentointivaiheessa kului IP-osoitteiden ja laitteiden välisen topologian hahmottamiseen sekä reitityksen varmistamiseen traceroute- ja reitti-analyyseilla. Eri verkkoalueiden (LAN, Server, Management, Branch) ja runkoverkkojen sarjoittaminen vaati huolellisuutta, jotta jokainen laite sijoittui oikean yhdyskäytävän alle.

Laadukas ja ajantasainen verkkodokumentaatio on IT-asiantuntijalle kriittinen työkalu. Se nopeuttaa vianetsintää ongelmatilanteissa, kun reitit ja laiteosoitteet ovat nopeasti tarkistettavissa ilman verkon uudelleenkartoitusta. Lisäksi dokumentaatio helpottaa turvallisuus- ja kapasiteettisuunnittelua sekä uusien järjestelmämuutosten hallittua toteuttamista.
