ARCHITETTURA_CED: due host ESXi, storage, backup e spazio di crescita

### Ruolo

#### Obiettivo
Il CED de Il Sogno ospita i servizi centrali del gruppo alberghiero: dominio Active Directory, DNS, DHCP, file server, RADIUS/NPS, gestionale, servizi multimediali e backup.

L'obiettivo è centralizzare l'infrastruttura senza distribuire server nelle singole strutture. La Meraviglia e L'Incanto accedono ai servizi aziendali tramite VPN site-to-site verso il CED, mentre traffico guest, Smart TV, tablet camere e sale meeting usano local breakout Internet nelle rispettive sedi.
### Indirizzamento

#### Rete Server/CED
I server centrali si trovano nella rete Server/CED de Il Sogno, secondo il piano di indirizzamento della sede.

- Sede: Il Sogno
- VLAN: 11 - Server_CED
- Rete: `10.30.11.0/27`
- Gateway: `10.30.11.1`

| Server | FQDN | Indirizzo IP | Ruoli principali |
|---|---|---:|---|
| DC01 | `dc01.corp.ilsogno.it` | `10.30.11.10` | AD DS, DNS, DHCP, Global Catalog |
| DC02 | `dc02.corp.ilsogno.it` | `10.30.11.11` | AD DS, DNS, DHCP failover, Global Catalog |
| FS01 | `fs01.corp.ilsogno.it` | `10.30.11.12` | File server SMB, cartelle reparto, permessi NTFS |
| NPS01 | `nps01.corp.ilsogno.it` | `10.30.11.13` | RADIUS/NPS, Wi-Fi aziendale, autenticazione VPN |
| BK01/NAS | `bk01.corp.ilsogno.it` | `10.30.11.14` | Backup, snapshot, repository locale |
| MEDIA01 | `media01.corp.ilsogno.it` | `10.30.11.15` | CMS multimediale, Hospitality TV, digital signage |
| GESTIONALE01 | `gestionale01.corp.ilsogno.it` | `10.30.11.16` | Gestionale hotel, prenotazioni, servizi reception |

Gli indirizzi sono statici e non devono essere inclusi in pool DHCP. La VLAN Management resta separata dalla VLAN Server_CED ed è dedicata ad apparati di rete, firewall, switch, AP, UPS e interfacce di gestione.

### Due server fisici

#### Obiettivo
Il CED userà due server fisici con hypervisor ESXi. La scelta di due host evita che DC01 e DC02 siano sullo stesso hardware e consente di distribuire i carichi principali tra due macchine indipendenti.

La ridondanza applicativa è garantita soprattutto per dominio, DNS e DHCP tramite DC01/DC02. FS01, GESTIONALE01 e MEDIA01 devono invece essere protetti con backup, snapshot e procedure di ripristino, perché non sono descritti come cluster attivo-attivo.

#### Specifiche tecniche minime consigliate

| Componente | Requisito per ogni host |
|---|---|
| Formato | Server rack 1U/2U per CED |
| CPU | 1 CPU server 12-16 core fisici, Intel Xeon Silver/Gold o AMD EPYC equivalente |
| RAM | 128 GB ECC, espandibile almeno a 256 GB |
| Storage sistema | 2 SSD enterprise da 480 GB in RAID 1 per ESXi |
| Storage VM | 4 SSD enterprise da 1,92 TB in RAID 10, circa 3,8 TB utili |
| Rete | almeno 2 porte 10 GbE per traffico VM/NAS e 2 porte 1 GbE per management o failover |
| Alimentazione | doppio alimentatore hot-swap ridondato |
| Gestione | controller out-of-band tipo iDRAC, iLO o IPMI |
| Virtualizzazione | VMware ESXi, con licenza coerente con backup e gestione scelta |

Queste specifiche sono dimensionate per i servizi attuali e lasciano margine per crescita, aggiornamenti software e due nuove VM future.

### Distribuzione VM

#### Host 1 - ESXi 1
Il primo host contiene i servizi più legati all'operatività quotidiana e al dominio primario.

| VM | FQDN | IP | Risorse indicative | Ruolo |
|---|---|---:|---|---|
| DC01 | `dc01.corp.ilsogno.it` | `10.30.11.10` | 2 vCPU, 4-8 GB RAM, 120 GB disco | Domain Controller primario, DNS, DHCP, Global Catalog |
| FS01 | `fs01.corp.ilsogno.it` | `10.30.11.12` | 4 vCPU, 16-32 GB RAM, 120 GB OS + 1,5-2 TB dati | File server SMB, cartelle reparto, quote, versioning |
| NPS01 | `nps01.corp.ilsogno.it` | `10.30.11.13` | 2 vCPU, 4 GB RAM, 80 GB disco | RADIUS/NPS per Wi-Fi aziendale e VPN |
| GESTIONALE01 | `gestionale01.corp.ilsogno.it` | `10.30.11.16` | 4 vCPU, 8-16 GB RAM, 250-500 GB disco | Gestionale hotel o integrazione gestionale esistente |

#### Host 2 - ESXi 2
Il secondo host contiene la ridondanza del dominio e i servizi multimediali. Mantiene più margine libero, così può ospitare servizi futuri o VM temporanee.

| VM | FQDN | IP | Risorse indicative | Ruolo |
|---|---|---:|---|---|
| DC02 | `dc02.corp.ilsogno.it` | `10.30.11.11` | 2 vCPU, 4-8 GB RAM, 120 GB disco | Domain Controller secondario, DNS, DHCP failover, Global Catalog |
| MEDIA01 | `media01.corp.ilsogno.it` | `10.30.11.15` | 4 vCPU, 16-24 GB RAM, 500 GB-1 TB disco | CMS multimediale, Hospitality TV, digital signage |
| Espansione | da definire | da definire | riserva per due VM future | Monitoring, portale ospiti, check-in online o nuovi servizi |

### NAS / backup appliance

#### Obiettivo
BK01/NAS è il repository locale di backup e snapshot del CED. Non sostituisce i server ESXi: protegge VM, configurazioni e dati in caso di guasto, errore umano o necessità di ripristino.

Requisiti consigliati:
- capacità utile: 16-24 TB;
- dischi in RAID 6, RAIDZ2 o configurazione equivalente con tolleranza a guasto disco;
- almeno 2 porte 10 GbE o 2,5/10 GbE in base agli switch disponibili;
- snapshot locali e retention storica;
- copia offsite o cloud per la regola 3-2-1;
- account separati per backup, con accessi amministrativi limitati.

BK01/NAS usa l'indirizzo `10.30.11.14` nella VLAN 11 Server_CED. Deve ricevere backup di DC01, DC02, FS01, NPS01, MEDIA01 e GESTIONALE01, includendo System State dei Domain Controller, dati FS01, configurazioni NPS, contenuti MEDIA01 ed export del gestionale.

Il dettaglio operativo di backup, retention, snapshot e copia offsite/cloud è documentato in [BK01_NAS.md](BK01_NAS.md).

### Condizionatore CED

- Marca proposta: Daikin, split inverter dedicato al CED.
- Potenza: circa 12.000 BTU/h, pari a circa 3,5 kW frigoriferi.
- Target temperatura: 22-24 gradi stabili, con manutenzione periodica filtri e scarico condensa.

### Spazio per VM future

#### Obiettivo
I due host non devono essere dimensionati solo per il carico iniziale. L'hotel deve poter seguire aggiornamenti software, crescita dei dati e nuove esigenze senza sostituire subito l'hardware.

Ad esempio:
- portale interno o check-in online, nuovo;
- integrazione con nuovo gestionale;
