# Rete 
 [group:: [[Rete]]] [assignee:: [[Regaldo]]] [assignee:: [[Rosso]]] [assignee:: [[Moccia]]] [assignee:: [[Valenza]]] 
[referente:: [[Regaldo]]]
- Cartine macro fatta per ogni hotel
	- Predispozione dispositivi (no dettagli)
		- AP, Router, Switch, PC end point, firewall
	- Vlan IoT,
	- CED
		- Due server (Capiamo costi e decidiamo) (rack / "pc normale")
		- Condizionatore
- Soluzione Wireless, wifi guest (n camera), wifi aziendale (se possibile stessa psw della AD)
- I tablet erogano servizi dell'hotel, se uno vuole internet si connette con il proprio device al wifi dell'hotel
- Smart TV hanno sia i contenuti multimediali che però internet (es. yt)
- Budget possibile
## Firewall
Firewall NGFW di filiale basato su pfSense, con VPN IPsec site-to-site verso il CED, routing inter-VLAN, NAT, filtraggio del traffico e local breakout Internet per ospiti e dispositivi multimediali.

La Meraviglia Firewall  ── VPN site-to-site ┐
                                            │
L'Incanto Firewall      ── VPN site-to-site ├── Firewall centrale CED ── Server / NAS / Gestionale
                                            │
Il Sogno / mini-case    ── LAN locale ──────┘
                                            │
Lavoratori remoti       ── VPN SSL/IPsec/WireGuard + MFA

Firewall centrale: **Next Generation Firewall**

Possibilità di un secondo firewall ridondante, chiaramente aumento di costi
Perché se il firewall centrale cade, perdete:
- VPN degli hotel;
- accesso remoto;
- accesso ai servizi centralizzati;
- gestione delle mini-case;
- parte del gestionale.


- DHCP Relay sui firewall
- firewall ok / vpn in tutti gli altri
- case gestite tramite vpn into ced

### Hotel La Meraviglia - 100 Camere
Firewall pfSense di filiale - fascia media
- VPN IPsec site-to-site verso CED
- routing tra VLAN
- NAT verso Internet locale
- firewall rules tra VLAN
- gestione traffico guest / camere / Smart TV / tablet
- supporto dual WAN opzionale
- logging verso CED
- IDS/IPS opzionale
### Hotel L'incanto - 30 Camere
Firewall pfSense di filiale - fascia small/medium
- VPN IPsec site-to-site verso CED
- routing inter-VLAN
- NAT Internet locale
- separazione rete ospiti / staff / camere
- logging verso CED
- regole firewall locali
### Hotel il Sogno - Mini case
Il router della mini-casa fa partire una **VPN client site-to-site** verso il CED
Data la forma piccola delle mini case utlizziamo WireGuard che è leggero, stabile e adatto a tanti tunnel piccoli, invece che *IpSec*.
## VPN
Per le VPN tra hotel e CED usiamo **IPsec site-to-site con IKEv2**

pfSense supporta IPsec come soluzione standard per VPN site-to-site e accessi remoti. Una VPN IPsec site-to-site collega due reti come se fossero direttamente connesse, lasciando comunque la possibilità di filtrare il traffico con regole firewall.

Negli hotel il firewall locale deve fa uscire direttamente su Internet:
Guest Wi-Fi,Smart TV,tablet, camere, streaming, sale meeting, dispositivi clienti

Verso il CED deve andare solo il traffico aziendale.

Questa scelta evita di saturare la VPN centrale con traffico inutile, per esempio streaming delle Smart TV o traffico degli ospiti.

## Proposta gestione infra mini-case
Router che apre con Wireguard vpn automatica al CED
Smart TV
Guest wifi

# Architettura software 
[group:: [[Infra CED]]]  [assignee:: [[Soffia]]] [assignee:: [[Bracco]]]
## Modalità di gestione degli utenti (gruppi, accessi, etc.)
Ambiente soluzione: Windows 
### Struttura
DC01: identità e servizi di dominio
DC02: ridondanza dominio
FS01: dati aziendali
BK01/NAS: backup e ripristino
MEDIA01: contenuti multimediali, se necessari

DC01
- Active Directory Domain Services
- DNS interno
- Forest root
- Global Catalog
- DHCP centralizzato

DC02
- Active Directory Domain Services
- DNS interno
- Global Catalog
- Ridondanza dominio
- DHCP failover,

FS01
- File Server Windows
- Condivisioni SMB
- Permessi NTFS
- Cartelle di reparto
- Quote, versioning, auditing

BK01 / NAS
- Backup dei server
- Snapshot
- Copia offline/offsite
- Replica verso altra sede o cloud

NPS01
- RADIUS / NPS
- Autenticazione Wi-Fi aziendale
- Autenticazione VPN

Server fisico 1 / Hypervisor 1**ESXi** » Vendi il fatto che tiri su facilmente vm
> Lasciamo spazio per extra VM per servizi
- DC01
- FS01
- NPS01
- server gestionale 

Server fisico 2 / Hypervisor 2 **ESXi**
- DC02 - Separato da DC01 per ridondanza
- MEDIA01 - Seperato da FS01 per sicurezza 
- eventuale monitoring / servizi secondari

NAS / Backup appliance / Storage dedicato
- BK01
- repository backup
- snapshot
- copia offsite/cloud

### Da fare
- [x] Topologia Infra windows [assignee:: [[Soffia + Bracco]]] ✅ 2026-06-16
- [x] Una infografica / immagine che mostra la gestione utenti tramite AD ✅ 2026-06-16
- [x] Soluzione per l’archiviazione, protezione, gestione e condivisione dei dati ✅ 2026-06-16
- [x] Mostrare come con le GPO di windows possiamo granularmente agire sugli end-point ✅ 2026-06-16
- [x] Mostrare possibilità di accesso remoto da qualsiasi luogo + ✅ 2026-06-16
- [x] Soluzione multimediale ✅ 2026-06-16
- [x] VPN ✅ 2026-06-16
- [x] Firewall ✅ 2026-06-16
- [x] Subappaltare Climatizzatore ✅ 2026-06-16


https://lucid.app/lucidchart/592c2f3c-7dfa-4cb7-b8c7-71d9c38a5e32/edit?invitationId=inv_6141ee99-ac11-48ab-b3dc-96332b6d8281

## Soluzione per l’archiviazione, protezione, gestione e condivisione dei dati 
- File Server Windows con condivisioni SMB integrate con Active Directory
## Ulteriori soluzioni per la sicurezza informatica (protezione degli endpoint, etc.)
Security By Design

se un PC della reception, un tablet in camera, una Smart TV, un laptop dell’IT o un server viene compromesso, cosa succede e come lo preveniamo/rileviamo? (aggancio sicurezza nelle diapositive)

"password robuste, aggiornamenti automatici, blocco schermo, account non amministratore per gli utenti normali, disco cifrato sui portatili, disabilitazione di servizi inutili, controllo USB dove necessario." - Tutto gestisto tramite AD e DC

**patch management**  - gestisto tramite AD e DC

## Soluzioni multimediali per le sale meeting/eventi e per le stanze degli hotel.
1. Stanze hotel
   - Smart TV / Hospitality TV
   - contenuti informativi dell’hotel
   - streaming personale dell’ospite
   - eventuale richiesta servizi / info territorio

2. Sale meeting/eventi
   - schermo/proiettore
   - audio
   - videoconferenza
   - condivisione schermo
   - digital signage fuori sala

3. Gestione contenuti
   - CMS multimediale centralizzato
   - video, immagini, guide, eventi, promozioni
   - gestione per hotel / piano / sala / camera

4. Licenze
   - contenuti prodotti dall’hotel
   - contenuti acquistati/licenziati
   - contenuti Creative Commons compatibili con uso commerciale
   - musica/video soggetti a diritti
   - streaming usato dagli ospiti con account personale
> L’hotel non fornisce account streaming condivisi.
L’ospite può accedere con il proprio account personale.
A fine soggiorno il sistema deve consentire logout automatico o reset credenziali.

La soluzione più professionale è usare **Hospitality TV** con piattaforma dedicata, per esempio LG Pro:Centric o Samsung LYNK Cloud.

LG Pro:Centric Direct è pensato proprio per hotel: permette gestione centralizzata dei contenuti sulle TV in camera, welcome page, informazioni su eventi, servizi e guide dell’hotel; LG lo descrive come una soluzione on-premise gestita da server interno dedicato.


La Meraviglia:
- Hospitality TV in ogni camera
- piattaforma centralizzata hotel TV
- welcome page personalizzata
- guida servizi
- promozioni spa/ristorante/eventi
- streaming con account personale ospite
- reset credenziali a fine soggiorno
L’Incanto:
- Hospitality TV o Smart TV business
- contenuti informativi centralizzati
- streaming personale ospite
- eventuale casting sicuro
Il Sogno:
- Smart TV / Hospitality TV nelle mini-case
- contenuti locali sul territorio enogastronomico
- guida ai servizi della reception
- QR code per prenotazioni e comunicazioni
- casting o app streaming con account ospite

**CMS multimediale**

Le sale meeting saranno dotate di display professionale o videoproiettore, sistema audio, apparati per videoconferenza, condivisione schermo cablata e wireless, e accesso Wi-Fi dedicato per ospiti/eventi. All’esterno delle sale potrà essere installato un display informativo collegato al CMS multimediale per mostrare nome evento, orari e indicazioni.
## Soluzione hw/sw per gestione dei servizi ai clienti (prenotazioni di servizi, comunicazioni con la reception, etc…)
Lista totale dei software / tecnologie implementate e come interagiscono.
hw come sopra