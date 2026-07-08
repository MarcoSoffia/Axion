BK01_NAS: backup appliance, snapshot, repository e copia offsite/cloud

### Ruolo

#### Obiettivo
BK01/NAS è l'appliance di backup e storage dedicata del CED de Il Sogno. Il suo compito è conservare backup, snapshot e copie di ripristino dei servizi centrali del gruppo alberghiero.

BK01/NAS non sostituisce i server ESXi e non ospita direttamente i servizi di produzione. Serve a proteggere VM, configurazioni e dati in caso di guasto hardware, errore umano, aggiornamento fallito o cancellazione accidentale.

#### Posizionamento
BK01/NAS sarà installato fisicamente nel CED de Il Sogno, insieme ai due host ESXi, al firewall centrale e agli apparati di rete principali.

Il NAS deve essere collegato alla rete Server/CED e, dove possibile, anche a una rete o interfaccia dedicata al traffico backup. Deve essere alimentato da UPS e mantenuto nello stesso ambiente climatizzato dei server.

### Indirizzamento

#### Rete Server/CED
BK01/NAS si trova nella rete Server/CED de Il Sogno, secondo il piano di indirizzamento della sede.

- Sede: Il Sogno
- VLAN: 11 - Server_CED
- Rete: `10.30.11.0/27`
- Gateway: `10.30.11.1`

| Server | FQDN | Indirizzo IP | Ruoli principali |
|---|---|---:|---|
| BK01/NAS | `bk01.corp.ilsogno.it` | `10.30.11.14` | Backup, snapshot, repository locale, copia offsite/cloud |

L'indirizzo IP e il record DNS sono statici. BK01/NAS deve essere raggiungibile solo dagli host ESXi, dai server autorizzati e dalle postazioni amministrative IT.

### Requisiti tecnici

#### Hardware consigliato
Il dimensionamento previsto è coerente con l'architettura CED e con la crescita dati stimata su 3-5 anni.

| Componente | Requisito consigliato |
|---|---|
| Capacità utile | 16-24 TB disponibili dopo RAID |
| Dischi | HDD enterprise/NAS, preferibilmente hot-swap |
| RAID | RAID 6, RAIDZ2 o configurazione equivalente con tolleranza a guasto disco |
| Rete | almeno 2 porte 10 GbE o 2,5/10 GbE in base agli switch disponibili |
| Alimentazione | alimentazione protetta da UPS |
| Snapshot | snapshot locali pianificati |
| Offsite | replica verso cloud o sede remota |
| Gestione | accesso amministrativo separato e tracciato |

Il NAS deve avere spazio sufficiente non solo per i backup iniziali, ma anche per retention storica, snapshot, crescita del file server e due eventuali VM future previste nell'architettura CED.

### Strategia backup

#### Principio generale
La strategia segue il modello 3-2-1:
- almeno tre copie dei dati;
- almeno due supporti o repository differenti;
- almeno una copia fuori sede o cloud.

BK01/NAS rappresenta il repository locale principale. La copia offsite/cloud protegge da scenari più gravi: furto, incendio, danneggiamento fisico del CED o compromissione del repository locale.

#### Oggetti protetti
BK01/NAS deve ricevere backup di tutti i servizi centrali.

| Servizio | Contenuto da proteggere | Note |
|---|---|---|
| DC01 | VM backup, System State, configurazione AD DS/DNS/DHCP | necessario per recovery del dominio |
| DC02 | VM backup, System State, configurazione AD DS/DNS/DHCP failover | ridondanza e recovery dominio |
| FS01 | VM backup, dati condivisi, permessi NTFS, snapshot file | servizio con maggiore crescita dati |
| NPS01 | VM backup, export configurazione NPS, policy RADIUS | salvare anche documentazione client RADIUS |
| MEDIA01 | VM backup, configurazione CMS, contenuti pubblicati, mapping dispositivi | utile per ripristino Hospitality TV e signage |
| GESTIONALE01 | VM backup, database applicativo, export dati | critico per reception e operatività hotel |
| ESXi host | export configurazione host e inventario VM | da aggiornare dopo modifiche rilevanti |

### Retention

#### Proposta iniziale
La proposta iniziale è:

| Tipo backup | Retention proposta |
|---|---|
| Giornaliero | 14-30 giorni |
| Settimanale | 8 settimane |
| Mensile | 12 mesi |
| Snapshot pre-aggiornamento | fino a verifica positiva dell'aggiornamento |
| Copia offsite/cloud | almeno backup settimanali e mensili |

FS01 e GESTIONALE01 possono richiedere retention più lunga rispetto agli altri servizi, perché contengono dati operativi e documentali del cliente.

### Snapshot e ripristino

#### Snapshot
Gli snapshot servono per recuperi rapidi da cancellazioni accidentali, errori operativi o aggiornamenti falliti. Non sostituiscono il backup completo.
#### Ripristino

Il ripristino deve essere testato periodicamente. Un backup non verificato non va considerato affidabile.

### Sicurezza e rete

#### Accesso consentito
BK01/NAS deve essere raggiungibile solo da sistemi autorizzati.

Accesso consentito:
- host ESXi;
- server da proteggere;
- postazioni IT autorizzate;
- eventuale software di backup;
- destinazione offsite/cloud configurata.

Accesso non consentito:
- guest Wi-Fi;
- Smart TV;
- tablet camere;
- reti meeting ospiti;
- dispositivi personali ospiti;
- dispositivi non censiti.

Il NAS non deve dipendere esclusivamente da Active Directory per l'accesso amministrativo: in caso di problema al dominio deve essere possibile accedere con account locale di emergenza custodito in modo sicuro.

### Copia offsite/cloud

#### Obiettivo
La copia offsite/cloud riduce il rischio di perdita dati se il CED non è disponibile o se BK01/NAS viene danneggiato.

La copia offsite non deve usare reti guest o traffico non controllato. Deve transitare attraverso connettività aziendale e policy firewall documentate.

### Dipendenze

BK01/NAS dipende da:
- rete Server/CED per raggiungere host e VM;
- DNS interno per risoluzione `bk01.corp.ilsogno.it`;
- spazio disco sufficiente per retention;
