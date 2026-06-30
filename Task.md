# Task

## Gruppi

- Networking: [[Regaldo]], [[Moccia]], [[Valenza]], [[Rosso]]
- Infra IT: [[Soffia]], [[Bracco]]
- Documentazione Tecnica: TBD

## Scadenze e stato generale

- [x] Setup team, nome, identita brand e strumenti di lavoro ✅ 2026-06-09
- [x] Prima idea di proposta cliente ✅ 2026-06-09
- [x] Materiale presentazione cliente / slide interattive ✅ 2026-06-22
- [ ] Inizio implementazione e prima demo 📅 2026-07-13 Urgent priority
- [ ] Consegna finale 📅 2026-07-24 Low priority

## Fase attuale - Creazione documentazione tecnica

Obiettivo: produrre una documentazione tecnica coerente, consegnabile e leggibile anche dopo la presentazione commerciale. 
### Struttura del documento tecnico
- low priority 
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
- High priority
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
- High priority
- [ ] Documentare architettura CED [group:: [[Infra CED]]] [assignee:: [[Soffia]]] [assignee:: [[Bracco]]]
	- [ ] Due server fisici con hypervisor ESXi [assignee:: [[Soffia]]]
	- [ ] Distribuzione VM tra host 1 e host 2 [assignee:: [[Soffia]]]
	- [ ] NAS / backup appliance / storage dedicato [assignee:: [[Soffia]]]
	- [ ] Condizionatore CED [assignee:: [[Soffia]]]
	- [ ] Spazio per VM future [assignee:: [[Soffia]]]
- [ ] Documentare servizi Windows [assignee:: [[Soffia]]]
	- [ ] DC01: Active Directory Domain Services, DNS, DHCP centralizzato, Global Catalog [assignee:: [[Soffia]]]
	- [ ] DC02: ridondanza dominio, DNS, Global Catalog, DHCP failover [assignee:: [[Soffia]]]
	- [ ] FS01: file server SMB, permessi NTFS, cartelle reparto, quote, versioning, auditing [assignee:: [[Soffia]]]
	- [ ] BK01 / NAS: backup server, snapshot, repository e copia offsite/cloud [assignee:: [[Soffia]]]
	- [ ] NPS01: RADIUS/NPS per Wi-Fi aziendale e VPN [assignee:: [[Soffia]]]
	- [ ] MEDIA01: contenuti multimediali, se necessario [assignee:: [[Soffia]]]
	- [ ] Server gestionale servizi hotel [assignee:: [[Soffia]]] 
- [ ] Documentare gestione utenti e accessi [assignee:: [[Bracco]]]
	- [ ] Account personali per dipendenti [assignee:: [[Bracco]]]
	- [ ] Reception con login personale su postazioni condivise [assignee:: [[Bracco]]]
	- [ ] Uffici con postazioni legate a persona/ruolo [assignee:: [[Bracco]]]
	- [ ] Gruppi Active Directory per direzione, contabilita, reception, IT, housekeeping e sale/eventi [assignee:: [[Bracco]]]
	- [ ] Accesso ai dati inter-hotel per direzione/contabilita e reception secondo necessita [assignee:: [[Bracco]]]
	- [ ] Smart working per ruoli autorizzati tramite VPN [assignee:: [[Bracco]]]
- [ ] Documentare GPO e hardening endpoint [assignee:: [[Bracco]]]
	- [ ] Policy Password robuste [assignee:: [[Bracco]]]
	- [ ] Blocco schermo automatico [assignee:: [[Bracco]]]
	- [ ] Aggiornamenti Windows forzati e programmati [assignee:: [[Bracco]]]
	- [ ] Account utente non amministratore [assignee:: [[Bracco]]]
	- [ ] Cifratura disco per portatili [assignee:: [[Bracco]]]
	- [ ] Disabilitazione servizi inutili [assignee:: [[Bracco]]]
	- [ ] Controllo USB dove necessario [assignee:: [[Bracco]]]
	- [ ] Patch management gestito centralmente [assignee:: [[Bracco]]]

### Documentazione dati, sicurezza e procedure [group:: [[Infra CED]]] [group:: [[Rete]]]
- low priority
- [ ] Documentare archiviazione, protezione, gestione e condivisione dati [group:: [[Infra CED]]] 
	- [ ] File Server Windows con condivisioni SMB integrate con Active Directory [group:: [[Infra CED]]] 
	- [ ] Cartelle di reparto e permessi NTFS [group:: [[Infra CED]]] 
	- [ ] Cartella condivisa inter-hotel per parte gestionale [group:: [[Infra CED]]] 
	- [ ] Backup, snapshot, restore e copia offsite/cloud[group:: [[Infra CED]]] 
- [ ] Documentare sicurezza informatica security-by-design [group:: [[Infra CED]]] [group:: [[Rete]]]
	- [ ] Segmentazione VLAN e regole firewall [group:: [[Rete]]]
	- [ ] Protezione PC, server, tablet, Smart TV e dispositivi camere [group:: [[Infra CED]]] 
	- [ ] MFA per VPN/accessi remoti [group:: [[Rete]]]
	- [ ] Monitoraggio/alert heartbeat per mini-case (Come lo faremmo) [group:: [[Infra CED]]] 

### Documentazione servizi cliente e multimediale [group:: [[Infra CED]]] [assignee:: [[Soffia]]] [assignee:: [[Bracco]]]
- low priority
- [ ] Documentare CMS multimediale
	- [ ] Gestione contenuti centralizzata
	- [ ] Video, immagini, guide, eventi e promozioni
	- [ ] Gestione per hotel, piano, sala e camera
	- [ ] MEDIA01 come componente possibile
	- [ ] Diffusione dei contenuti all'hospitality TV, sale meeting, camere

### Hardware, software e budget [group:: [[Infra CED]]] [group:: [[Rete]]] 
- low priority
- [ ] Trasformare [[Dispositivi]] in distinta tecnica allegata
	- [ ] Server fisici / host ESXi
	- [ ] NAS / storage
	- [ ] Firewall centrali e di filiale [group:: [[Rete]]]
	- [ ] Switch, PoE, rack, patch panel, prese RJ45 [group:: [[Rete]]]
	- [ ] Access point [group:: [[Rete]]]
	- [ ] Router mini-case [group:: [[Rete]]]
	- [ ] Hospitality TV / Smart TV 
	- [ ] Tablet in camera [group:: [[Rete]]]
	- [ ] PC, telefoni VoIP, telecamere IP [group:: [[Rete]]]
	- [ ] UPS e condizionatore CED [group:: [[Rete]]]
	- [ ] Kit sale meeting e digital signage [group:: [[Rete]]]
- [ ] Documentare software e tecnologie implementate
	- [ ] Windows Server / Active Directory
	- [ ] ESXi
	- [ ] pfSense [group:: [[Rete]]]
	- [ ] WireGuard
	- [ ] IPsec/IKEv2 [group:: [[Rete]]] 
	- [ ] NPS/RADIUS
	- [ ] SMB/NTFS
	- [ ] CMS multimediale / Hospitality TV platform
	- [ ] Software gestionale servizi cliente
- [ ] Preparare sezione budget tecnico [group:: [[Rete]]] 
	- [ ] Budget minimo
	- [ ] Budget premium
	- [ ] Stima specifiche server
	- [ ] Costi Axion: analisi, progettazione, installazione, configurazione, test e documentazione finale

### Allegati e verifica finale [group:: [[Documentazione tecnica]]] 
- low priority
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

