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





