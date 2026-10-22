# Fra-fysisk-nettverk-til-bedriftsnettverk
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

Laget en ny fells mappe for dette projektet på server-pc med å lag ny mappe med navn. Så inn på advanced shering og La til alle med full kontroll. Legg til nettverksplassering i filutforsker, og skriver derved navnet til serveren og logger på admin for å godkjenne mappen. Deretter åpner man den nye fells mappen på klient-pc for å kunne dele en ny mappe med sever-pc-en og klient-pc-en.

<img width="240" height="312" alt="image" src="https://github.com/user-attachments/assets/48e2327a-9fda-44a7-90ca-9c83940e2c4d" /> <img width="237" height="312" alt="image" src="https://github.com/user-attachments/assets/0c6dfdaa-1bb5-424a-aa8a-2ca1f76e8602" /> <img width="251" height="313" alt="image" src="https://github.com/user-attachments/assets/f7330831-eaeb-4338-855a-3e356d92cf04" /> <img width="315" height="90" alt="image" src="https://github.com/user-attachments/assets/11a6840d-da75-4646-bb89-699b8c9d3c39" />

<img width="250" height="277" alt="image" src="https://github.com/user-attachments/assets/f98c54cf-4baa-417a-9f30-29c3c6520c58" />

Med denne løsningen blir dette en «quick fix» for kunne sette opp mappen lettere som en snarvei. Det er mulig å sette begrensinger sånn det er bare users på serveren som har tilgang til spesifikke mapper, mens admin har styring hvem som har tilgang til hva. Ved denne «quick fix» løsningen kan det være fare for om klient pc-en blir utsatt for virus. kan det forutsake fri tilgang til å kryptere og slette alt på serveren gjennom den delte mappen. Jeg skal kommer mer inn på dette med active directory i neste oppgave. 



