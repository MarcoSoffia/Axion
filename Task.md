# Task

## Gruppi

- Networking: [[Regaldo]], [[Moccia]], [[Valenza]], [[Rosso]]
- Infra IT: [[Soffia]], [[Bracco]]
- Documentazione Tecnica: TBD

## Scadenze e stato generale

- [x] Setup team, nome, identita brand e strumenti di lavoro ✅ 2026-06-09
- [x] Prima idea di proposta cliente ✅ 2026-06-09
- [x] Materiale presentazione cliente / slide interattive ✅ 2026-06-22
- [ ] Inizio implementazione e prima demo 📅 2026-07-13
- [ ] Consegna finale 📅 2026-07-24

## Fase attuale - Creazione documentazione tecnica

Obiettivo: produrre una documentazione tecnica coerente, consegnabile e leggibile anche dopo la presentazione commerciale. 
### Struttura del documento tecnico
Le cose da scrivere nella relazione tecnica
- [ ] Definire indice della documentazione tecnica [group:: [[Documentazione tecnica]]]
	- [ ] Scopo del progetto e perimetro delle tre strutture
	- [ ] Architettura generale Axion per hospitality
	- [ ] Rete e connettivita
	- [ ] CED e infrastruttura Windows
	- [ ] Sicurezza, accessi e gestione utenti
	- [ ] Servizi cliente, multimediale e sale meeting
	- [ ] Hardware, software, licenze e opzioni budget
	- [ ] Procedure operative e manutenzione
	- [ ] Allegati tecnici e diagrammi
- [ ] Documentazione in .pdf
	- [ ] Documento tecnico principale
	- [ ] Allegati tecnici separati per mappe, diagrammi e distinta dispositivi

### Documentazione rete [referee:: [[Regaldo]]]

- [ ] Documentare topologia logica della rete [group:: [[Rete]]] [assignee:: [[Regaldo]]] [assignee:: [[Valenza]]] [assignee:: [[Moccia]]]
	- [ ] Definire le tecnologie usare (Es. Cisco)
	- [ ] Piano di indirizzamento
		- [ ] Hotel il Sogno 
		- [ ] Hotel La meraviglia
		- [ ] Hotel L'incanto
		- [ ] Esempio Mini Casa
	- [ ] VLAN previste per management, staff, ospiti, sicurezza, sale eventi, domotica/IoT e dispositivi multimediali
	- [ ] Separazione traffico guest / staff / camere / Smart TV / tablet
- [ ] Documentare infrastruttura cablata
	- [ ] La Meraviglia: switch principale, switch per piano, PoE, aggregazione, rack e prese RJ45
	- [ ] L'Incanto: cablaggio, eventuali rack secondari e collegamento verso firewall di filiale / CED centrale
	- [ ] Il Sogno: reception, uffici, CED e mini-case
	- [ ] Sale meeting/eventi: Wi-Fi dedicato e postazione PC per proiettore
- [ ] Documentare copertura wireless
	- [ ] Criterio di dimensionamento AP basato sui metri quadri
	- [ ] Wi-Fi guest per ospiti (Nome wifi, tipo psw (WPA3))
	- [ ] Wi-Fi aziendale integrato, dove possibile, con Active Directory / NPS
	- [ ] Rete meeting per ospiti/eventi
- [ ] Documentare firewall e VPN
	- [ ] Firewall centrale CED NGFW
	- [ ] Firewall pfSense di filiale per La Meraviglia
	- [ ] Firewall pfSense di filiale per L'Incanto
	- [ ] Router/VPN WireGuard per mini-case
	- [ ] VPN IPsec site-to-site hotel -> CED con IKEv2
	- [ ] VPN remota per IT, direzione e contabilita con MFA
	- [ ] Local breakout Internet per guest, Smart TV, tablet, camere e sale meeting
	- [ ] Logging verso CED e IDS/IPS opzionale
- [ ] Documentare continuita operativa rete
	- [ ] UPS per apparati critici e connessione Internet
	- [ ] Kit router mini-case preconfigurato per sostituzione rapida

### Documentazione CED e infrastruttura Windows

- [ ] Documentare architettura CED [group:: [[Infra CED]]] [assignee:: [[Soffia]]] [assignee:: [[Bracco]]]
	- [ ] Due server fisici con hypervisor ESXi
	- [ ] Distribuzione VM tra host 1 e host 2
	- [ ] NAS / backup appliance / storage dedicato
	- [ ] Condizionatore CED
	- [ ] Spazio per VM future
- [ ] Documentare servizi Windows
	- [ ] DC01: Active Directory Domain Services, DNS, DHCP centralizzato, Global Catalog
	- [ ] DC02: ridondanza dominio, DNS, Global Catalog, DHCP failover
	- [ ] FS01: file server SMB, permessi NTFS, cartelle reparto, quote, versioning, auditing
	- [ ] BK01 / NAS: backup server, snapshot, repository e copia offsite/cloud
	- [ ] NPS01: RADIUS/NPS per Wi-Fi aziendale e VPN
	- [ ] MEDIA01: contenuti multimediali, se necessario
	- [ ] Server gestionale servizi hotel
- [ ] Documentare gestione utenti e accessi
	- [ ] Account personali per dipendenti
	- [ ] Reception con login personale su postazioni condivise
	- [ ] Uffici con postazioni legate a persona/ruolo
	- [ ] Gruppi Active Directory per direzione, contabilita, reception, IT, housekeeping e sale/eventi
	- [ ] Accesso ai dati inter-hotel per direzione/contabilita e reception secondo necessita
	- [ ] Smart working per ruoli autorizzati tramite VPN
- [ ] Documentare GPO e hardening endpoint
	- [ ] Policy Password robuste
	- [ ] Blocco schermo automatico
	- [ ] Aggiornamenti Windows forzati e programmati
	- [ ] Account utente non amministratore
	- [ ] Cifratura disco per portatili
	- [ ] Disabilitazione servizi inutili
	- [ ] Controllo USB dove necessario
	- [ ] Patch management gestito centralmente

### Documentazione dati, sicurezza e procedure [group:: [[Infra CED]]] [assignee:: [[Soffia]]] [assignee:: [[Bracco]]]

- [ ] Documentare archiviazione, protezione, gestione e condivisione dati
	- [ ] File Server Windows con condivisioni SMB integrate con Active Directory
	- [ ] Cartelle di reparto e permessi NTFS
	- [ ] Cartella condivisa inter-hotel per parte gestionale
	- [ ] Versioning, quote e auditing
	- [ ] Backup, snapshot, restore e copia offsite/cloud
- [ ] Documentare sicurezza informatica security-by-design
	- [ ] Segmentazione VLAN e regole firewall
	- [ ] Protezione PC, server, tablet, Smart TV e dispositivi camere
	- [ ] MFA per VPN/accessi remoti
	- [ ] Logging centralizzato
	- [ ] Tracciamento accesso/modifica documenti sensibili come proposta aggiuntiva
	- [ ] Monitoraggio/alert heartbeat per mini-case
- [ ] Scrivere procedure operative
	- [ ] Onboarding nuovo dipendente
	- [ ] Offboarding dipendente
	- [ ] Cambio ruolo e aggiornamento gruppi AD
	- [ ] Reset password e recupero account
	- [ ] Creazione nuova postazione reception/ufficio
	- [ ] Sostituzione router mini-casa con kit preconfigurato
	- [ ] Verifica tunnel VPN hotel e mini-case
	- [ ] Ripristino file da backup
	- [ ] Gestione incidente endpoint compromesso
	- [ ] Gestione credenziali e consegna al cliente, senza inserire segreti nel documento

### Documentazione servizi cliente e multimediale [group:: [[Infra CED]]] [assignee:: [[Soffia]]] [assignee:: [[Bracco]]]

- [ ] Documentare soluzione Hospitality TV / Smart TV
	- [ ] Piattaforma Hospitality TV LG Pro:Centric
	- [ ] Welcome page
	- [ ] Guida servizi hotel
	- [ ] Promozioni spa/ristorante/eventi
	- [ ] Contenuti locali e territorio
	- [ ] Streaming con account personale ospite
	- [ ] Logout/reset credenziali a fine soggiorno
	- [ ] Nota licenze: l'hotel non fornisce account streaming condivisi
- [ ] Documentare tablet in camera
	- [ ] Richieste reception
	- [ ] Prenotazioni servizi, spa, ristorante, eventi
	- [ ] Comunicazioni in circuito chiuso
	- [ ] Connessione ai servizi CED tramite rete/VPN prevista
- [ ] Documentare sale meeting/eventi Presentazione e comunicazione
	- [ ] Display professionale o videoproiettore
	- [ ] Audio
	- [ ] Videoconferenza Teams/Zoom/Google Meet
	- [ ] Condivisione schermo cablata e wireless
	- [ ] Wi-Fi dedicato ospiti/eventi
	- [ ] Digital signage fuori sala collegato al CMS
- [ ] Documentare CMS multimediale
	- [ ] Gestione contenuti centralizzata
	- [ ] Video, immagini, guide, eventi e promozioni
	- [ ] Gestione per hotel, piano, sala e camera
	- [ ] MEDIA01 come componente possibile

### Hardware, software e budget [group:: [[Infra CED]]] [group:: [[Networking]]] 

- [ ] Trasformare [[Dispositivi]] in distinta tecnica allegata
	- [ ] Server fisici / host ESXi
	- [ ] NAS / storage
	- [ ] Firewall centrali e di filiale
	- [ ] Switch, PoE, rack, patch panel, prese RJ45
	- [ ] Access point
	- [ ] Router mini-case
	- [ ] Hospitality TV / Smart TV
	- [ ] Tablet in camera
	- [ ] PC, telefoni VoIP, telecamere IP
	- [ ] UPS e condizionatore CED
	- [ ] Kit sale meeting e digital signage
- [ ] Documentare software e tecnologie implementate
	- [ ] Windows Server / Active Directory
	- [ ] ESXi
	- [ ] pfSense
	- [ ] WireGuard
	- [ ] IPsec/IKEv2
	- [ ] NPS/RADIUS
	- [ ] SMB/NTFS
	- [ ] CMS multimediale / Hospitality TV platform
	- [ ] Software gestionale servizi cliente
- [ ] Preparare sezione budget tecnico
	- [ ] Budget minimo
	- [ ] Budget premium
	- [ ] Opzioni aggiuntive: firewall ridondante, dual WAN, IDS/IPS, auditing avanzato, monitoraggio
	- [ ] Stima specifiche server
	- [ ] Costi Axion: analisi, progettazione, installazione, configurazione, test e documentazione finale

### Allegati e verifica finale [group:: [[Documentazione tecnica]]] 

- [ ] Inserire allegati grafici
	- [ ] Mappe logiche cablaggio da `img/logical/`
	- [ ] Architettura logica CED
	- [ ] Architettura software CED
	- [ ] Diagramma GPO
	- [ ] Soluzione multimediale
	- [ ] Distinta hardware
- [ ] Verificare coerenza finale
	- [ ] Nomi hotel coerenti: La Meraviglia, L'Incanto, Il Sogno
	- [ ] CED sempre indicato presso Il Sogno
	- [ ] Terminologia uniforme: ospiti, staff, camere, sale meeting, mini-case
	- [ ] Nessuna credenziale reale nel documento
	- [ ] Coerenza tra documentazione, presentazione e `Testo.pdf`
	- [ ] Distinguere chiaramente soluzioni base e opzioni premium

