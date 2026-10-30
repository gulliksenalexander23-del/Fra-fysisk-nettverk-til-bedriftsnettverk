# Fra-fysisk-nettverk-til-bedriftsnettverk
# Kravspesifikasjon

<img width="595" height="578" alt="image" src="https://github.com/user-attachments/assets/72bd9121-f7f5-4c93-bdaf-5cc6df078063" />

Endret ipv4 fra 198.168.1.11 til 198.168.0.11 på klient pc-en for å kobling til ruten 
For at ruteren var på et annet nettverk.
Startet med å endret WAN , fra statisk til dynamisk på tplinkwifi.net
Endret Ip-en på ruteren via tplinkwifi.net 198.168.0.11 til 198.168.1.1 for å ha det det lokale nettverket. 
Endret statisk ipv4 på klient pc-en tilbake til 192.168.0.11

Endring av brannmur regler for å kunne sende ping fra sever-pc til klient-pc 
Hvor ping har feilet fra fra sever-pc til klient-pc og hvor ping har funket etter endingene i brannmur 

<img width="945" height="74" alt="image" src="https://github.com/user-attachments/assets/8dd1aeeb-ac7b-49b3-85d2-540f0ed88070" />

<img width="516" height="447" alt="image" src="https://github.com/user-attachments/assets/6881fd7b-c554-4062-bff7-2ecff738b240" />


Port 2 til switch til port 1 ruteren
Port 3 til switch til serveren 
Får internett fra vegg til ruteren på internett porten 

# Steg 2 – adresseplan og gateway
Nett: 192.168.1.1
R1: 192.168.1.1
SERVER01: 192.168.1.10
CLIENT01: 192.168.1.100

# Steg 3 – grunnleggende testing

Ping fra klienten til serveren
<img width="829" height="373" alt="image" src="https://github.com/user-attachments/assets/2eff0638-ac9c-44c0-a02d-985b10d9ddae" />

Ping fra serveren til klienten
<img width="845" height="384" alt="image" src="https://github.com/user-attachments/assets/19a79bf1-93e5-4b3c-89c2-3fb5a9940a26" />

# Steg 4 – DHCP til klienten
Først Setter vi CLIENT01 til automatisk IP-adresse på ethernet.
Så skriver vi inn ipconfig /release for å fjerne nåværende IP-adress som den har fra DHCP-serveren. Deretter kjører vi ipconfig /renew for å tvinge maskinen til å be om ny IP-adresse fra DHCP-serveren på det nettet den nå faktisk er plugget i. Med ipconfig /all er det bare vanlig ipconfig bare mer informasjon. 
I mitt tilfelle blir ikke den endret fordi den tar den nærmeste IP-adressen som er tilgjengelig. Siden den er allerede satt 192.168.1.100 vil den bare ta den IP-adressen siden det er bare en person på serveren. 
<img width="789" height="169" alt="image" src="https://github.com/user-attachments/assets/84665f46-48e8-4972-b477-42b8b87f7b6f" />
<img width="945" height="398" alt="image" src="https://github.com/user-attachments/assets/5275e1f2-a2fd-4fca-bdfc-cc1c28f1d873" /> 

# Steg 5 – bruk SERVER01 som server

Laget en ny fells mappe for dette projektet på server-pc med å lag ny mappe med navn. Så inn på advanced shering og La til alle med full kontroll. Legg til nettverksplassering i filutforsker, og skriver derved navnet til serveren og logger på admin for å godkjenne mappen. Deretter åpner man den nye fells mappen på klient-pc for å kunne dele en ny mappe med sever-pc-en og klient-pc-en.

<img width="240" height="312" alt="image" src="https://github.com/user-attachments/assets/48e2327a-9fda-44a7-90ca-9c83940e2c4d" /> <img width="237" height="312" alt="image" src="https://github.com/user-attachments/assets/0c6dfdaa-1bb5-424a-aa8a-2ca1f76e8602" /> <img width="251" height="313" alt="image" src="https://github.com/user-attachments/assets/f7330831-eaeb-4338-855a-3e356d92cf04" /> <img width="315" height="90" alt="image" src="https://github.com/user-attachments/assets/11a6840d-da75-4646-bb89-699b8c9d3c39" />

<img width="250" height="277" alt="image" src="https://github.com/user-attachments/assets/f98c54cf-4baa-417a-9f30-29c3c6520c58" />

Med denne løsningen blir dette en «quick fix» for kunne sette opp mappen lettere som en snarvei. Det er mulig å sette begrensinger sånn det er bare users på serveren som har tilgang til spesifikke mapper, mens admin har styring hvem som har tilgang til hva. Ved denne «quick fix» løsningen kan det være fare for om klient pc-en blir utsatt for virus. kan det forutsake fri tilgang til å kryptere og slette alt på serveren gjennom den delte mappen.
# Steg 6 – porter og Nmap
Port : 443 State : open Service : https

Port : 445 State : open Service : Microsoft-ds

<img width="430" height="373" alt="image" src="https://github.com/user-attachments/assets/b67da8dc-73fa-45b4-a862-7fff55c4a73a" /> <img width="427" height="374" alt="image" src="https://github.com/user-attachments/assets/82c4c761-2b70-4851-ad74-e919f4f57d2f" /> <img width="432" height="314" alt="image" src="https://github.com/user-attachments/assets/e9f4a362-e40f-43cc-89e0-f87ddaf23890" />

en port (State: open) er åpen betyr at den kjører en tjeneste eller et program på serveren som aktivt lytter på denne porten, og som er klar til å motta tilkoblinger fra andre enheter på nettverket. Om porten hadde været (State: closed) så ville port vært lukket, som er at det er ingen tjeneste som lytter der og trafikken blir avvist. 

# Steg 7 – Wireshark
Åpner Wireshark med å starte fangsten ved å sende ping 192.168.1.10 på klient pc-en. Deretter filtrer vi i søkefeltet etter ICMP for å finne requst og replay og kilder og mål. 
Her ser vi at klienten sendere request og så får serveren replay. Kilden blir 192.168.1.100 og mål blir 192.168.1.10

<img width="945" height="113" alt="image" src="https://github.com/user-attachments/assets/c7ef8122-898b-423d-9fc4-e47c29d9dc06" />

Gjennom å sjekke i wireshark på den delte felles mappen så får jeg opp ipv6 i resultatet mitt. Dette skylles at nettverket på server pc-en ikke har blitt endret til ipv4 sånn at wireshark klarer ikke å lese av ipv4 på søket TCP. Om dette skulle blitt endret til ipv4 så måtte man starte serveren på nytt via å ta av ipv6 på serveren.

<img width="945" height="243" alt="image" src="https://github.com/user-attachments/assets/99d2892d-95eb-4edf-afac-e62d8081d1df" />
Nmap sender forespørsler til en rekke port er for å kartlegge hva som finnes på maskinen. Svaret viser klienten hvilke port er og tjenester som er åpne og klare til bruker. Dette sier noe om systemets tilgjengelige tjenester på et gitt tidspunkt.

Port 53 ( domain / DNS): Navneoppslagstjeneste som oversetter domenenavn (f.eks. domene.local) til IP-adresser, og hjelper klienter med å finne servere i nettverket.

Port 80 ( http ): Ukryptert web-trafikk, brukes til å betjene vanlige nettsider eller webbaserte administrasjonsgrensesnitt.

Port 88 ( kerberos-sec ): Sikker autentiseringsprotokoll i Windows Active Directory. Håndterer billettbasert innlogging og identitetsverifisering for brukere og maskiner.

Port 135 ( msrpc ): Microsoft RPC (Remote Procedure Call) Endpoint Mapper. Hjelper klienter med å oppdage hvilke dynamiske porter andre Windows-tjenester lytter på.

Port 139 ( netbios-ssn ): NetBIOS Session Service, en eldre Windows-protokoll for fildeling, skriveutskrift og nettverkskommunikasjon.

Port 389 ( ldap ): Lightweight Directory Access Protocol. Brukes til å søke i og oppdatere oppføringer i Active Directory-databasen (som brukerkontoer, grupper og tilganger).

Port 443 ( https ): Kryptert web-trafikk (TLS/SSL) for sikker kommunikasjon mot nettsider eller web-tjenester.

Port 445 ( microsoft-ds / SMB): Server Message Block over IP. Brukes til direkte fildeling, tilgang til nettverksskrivere og overføring av Group Policy (GPO) til Windows-klienter.

Port 3389 ( ms-wbt-server / RDP): Remote Desktop Protocol. Gjør det mulig for administratorer å koble seg til maskinen via et grafisk fjernskrivebord.

Wireshark viser trafikken som flyter i øyeblikket. (ping fra pakker eller flyten mellom delte mapper når man åpner de) dette gjelder også for kommunikasjonen mellom enhetene.

# Del 2 - Krav til Packet Tracer-løsningen

## Steg 1 – bygg og test LAN-ene
### Plassering av enheter 
Startet med å ta 2 stykk 2911-rutere for ruter 8 og ruter 9. 4 stykk 2960-24-switcher for salg,support,admin og server. tre-klient-PC-er for (PC salg, PC support og PC admin) og en sentral server (server). På ruter 8 kobler vi til salg-switchen og support-switchen med Copper Straight-Through kabler mot port gig0/0 og gig0/1. på ruter 9 kobler vi til admin-switchen og server-switchen med Copper Straight-Through kabler mot port gig0/0 og gig0/1. Deretter kobler vi sammen ruter 8 og ruter 9 forbindelesen med å kable en Copper Cross-Over kabel direkte fra en ledig port på ruter 8 til en ledig port på ruter 9 (gig0/2).

### Konfigurasjon av Ruter-grensesnitt (CLI)
For å etablere Default Gateway for hvert subnett og aktivere portene, ble følgende gjennomført i CLI.

**Ruter 8**

**Salg-LAN (192.168.40.0)**

Router> enable 

Router# configure terminal 

Router(config)# interface GigabitEthernet0/0

Router(config-if)# ip address 192.168.40.1 255.255.255.0 

Router(config-if)# no shutdown 

Router(config-if)# exit

**Support-LAN (192.168.20.0)**

Router> enable 

Router# configure terminal 

Router(config)# interface GigabitEthernet0/1

Router(config-if)# ip address 192.168.20.1 255.255.255.0

Router(config-if)# no shutdown 

Router(config-if)# exit

**Linje mot Ruter 9 (10.0.0.0/30)**

Router> enable 

Router# configure terminal 

Router(config)# interface GigabitEthernet0/0/2 

Router(config-if)# ip address 10.0.0.1 255.255.255.252 

Router(config-if)# no shutdown

<img width="917" height="150" alt="image" src="https://github.com/user-attachments/assets/bc6b326c-bfc9-4dec-aad8-b78520e50c61" />

**Ruter 9**

**Admin-LAN (192.168.10.0)**

Router> enable 

Router# configure terminal

Router(config)# interface GigabitEthernet0/0

Router(config-if)# ip address 192.168.10.1 255.255.255.0

Router(config-if)# no shutdown 

Router(config-if)# exit 

**Server-LAN (192.168.30.0)**

Router> enable 

Router# configure terminal

Router(config)# interface GigabitEthernet0/1 

Router(config-if)# ip address 192.168.30.1 255.255.255.0 

Router(config-if)# no shutdown 

Router(config-if)# exit

**Linje mot Router 8 (10.0.0.0/30)**

Router> enable 

Router# configure terminal

Router(config)# interface GigabitEthernet0/2 

Router(config-if)# ip address 10.0.0.2 255.255.255.252 

Router(config-if)# no shutdown

<img width="945" height="132" alt="image" src="https://github.com/user-attachments/assets/3c53ba0b-5b20-492d-b6c1-1ab11ad688f3" />

## Steg 2 – routing mellom nettene 

For at trafikk skal flyte på tvers av ruter 8 og ruter 9, må ruterne få vite hvor pakkene skal sendes. 

**Statisk Ruting**

**På ruter 8 i CLI**

Router> enable

Router# configure terminal 

Router(config)# ip route 192.168.10.0 255.255.255.0 10.0.0.2 

Router(config)# ip route 192.168.30.0 255.255.255.0 10.0.0.2

Router# end

<img width="945" height="528" alt="image" src="https://github.com/user-attachments/assets/7ce63ee0-b10c-413c-8756-f9a70e5b0e82" />

**På Ruter 9 i CLI**

Router> enable

Router# configure terminal 

Router(config)# ip route 192.168.20.0 255.255.255.0 10.0.0.1

Router(config)# ip route 192.168.40.0 255.255.255.0 10.0.0.1

Router# end

<img width="719" height="366" alt="image" src="https://github.com/user-attachments/assets/5ff3c062-ee5a-49e0-bad5-db2936801aeb" />

For å sjekke om den statiske IP-adressen er satt velger jeg å sende tracert mellom admin og salg. Først må vi vite hva ip-adressen til salg er før vi sender ut trafikken. I desktop på PC salg går vi innpå command promt og skriver ipconfig, da finner vi ut av at  IP-en på PC salg er 192.168.40.21.

<img width="739" height="449" alt="image" src="https://github.com/user-attachments/assets/febf4ae6-2eae-4d5a-a7b1-b0e5190a2b73" />

Detter åpner vi command promt på desktop for PC admin og skriver inn tracert 192.168.40.21.

<img width="928" height="280" alt="image" src="https://github.com/user-attachments/assets/b29bf43f-90a4-45c9-9574-5af0eab3dd5c" />

##Steg 3 – DHCP, DNS og http
Fast IP-adresse på Server0
Går inn på Server0 til Desktop så på IP Configuration og velg Static:
•	IP Address: 192.168.30.10
•	Subnet Mask: 255.255.255.0
•	Default Gateway: 192.168.30.1
•	DNS Server: 192.168.30.10 (Serveren peker på seg selv for sine egne navneoppslag)

 <img width="945" height="336" alt="image" src="https://github.com/user-attachments/assets/3891e27f-c08c-4af1-8f18-b9f398dfcb1d" />

2. Aktiver og konfigurer HTTP (Webserver)
1.	Klikk på Server0 og går til Services også HTTP.
2.	Sørg for at både HTTP og HTTPS står satt til On.
3.	(Valgfritt) Klikk på edit ved siden av index.html for å tilpasse nettsiden (f.eks. endre overskriften til <h1>Velkommen til Fjordtek Intranett!</h1>). Trykk Save.
 
<img width="945" height="540" alt="image" src="https://github.com/user-attachments/assets/b04021a8-1a0b-460b-91cb-1915caa3dfec" />

3. Aktiver og konfigurer DNS (Navnetjeneste)
1.	Klikk på Server0 så til Services også DNS.
2.	Sett DNS Service til On.
3.	Opprett A Record under Resource Records:
o	Name: intranett.fjordtek.local
o	Type: A Record
o	Address: 192.168.30.10
4.	Klikk Add.

<img width="945" height="479" alt="image" src="https://github.com/user-attachments/assets/104c0de5-9b0d-4569-ae2b-24f63e08c342" />

4. Konfigurer DHCP for klientnettene
Siden vi bruker en ruter (Router) som DHCP-server:
Åpne CLI på ruterene og kjør kommandoer
Opprett DHCP-pooler på Server0:
•	Salg-Pool (192.168.40.0)

<img width="575" height="498" alt="image" src="https://github.com/user-attachments/assets/b652d848-2714-4eb0-97fe-d8818f283c9a" />
Her har det blitt feil skrevet. Ip dhcp pool slag skal hete (salg)

•	Support-Pool (192.168.20.0)
<img width="945" height="1302" alt="image" src="https://github.com/user-attachments/assets/d30130ed-4f7d-4bea-a052-98d1908c901c" />

•	Admin-Pool (192.168.10.0)
<img width="945" height="189" alt="image" src="https://github.com/user-attachments/assets/2c62ef7c-5241-456c-b389-6d73ab39becf" />

Etter at vi lagt til dette, kan vi sjekke via command promt på en av klient-pcene med kommandoen ipconfig /all for å se at klientens side er bekreftet og at den har mottatt alt fra DHCP-serveren.

<img width="945" height="556" alt="image" src="https://github.com/user-attachments/assets/0909d000-380c-460d-8ebd-0724a7005efd" />






