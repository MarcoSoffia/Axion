MEDIA01: CMS multimediale, Hospitality TV, sale meeting e digital signage

### Ruolo

#### Obiettivo
MEDIA01 ospita o integra la piattaforma di gestione contenuti multimediali per gli hotel del gruppo. Il servizio centralizza contenuti informativi, welcome page, promozioni, guide, eventi e digital signage, rendendoli distribuibili verso Hospitality TV, display sale meeting e dispositivi multimediali autorizzati.

MEDIA01 non sostituisce FS01: FS01 conserva dati aziendali e cartelle di reparto, mentre MEDIA01 gestisce contenuti destinati agli ospiti e agli spazi pubblici.

#### Posizionamento
MEDIA01 sarà eseguito come macchina virtuale sul secondo host ESXi, insieme a DC02 e a eventuali servizi secondari o di monitoring.

La separazione da FS01 riduce il rischio che un problema sui servizi multimediali impatti il file server aziendale. MEDIA01 resta nel CED de Il Sogno, ma distribuisce contenuti anche verso La Meraviglia, L'Incanto, sale meeting e mini-case.

### Indirizzamento

#### Rete Server/CED
MEDIA01 si trova nella rete Server/CED de Il Sogno, secondo il piano di indirizzamento della sede.

- Sede: Il Sogno
- VLAN: 11 - Server_CED
- Rete: `10.30.11.0/27`
- Gateway: `10.30.11.1`

| Server | FQDN | Indirizzo IP | Ruoli principali |
|---|---|---:|---|
| MEDIA01 | `media01.corp.ilsogno.it` | `10.30.11.15` | CMS multimediale, Hospitality TV, digital signage |

L'indirizzo IP e il record DNS sono statici. MEDIA01 deve risolvere correttamente DC01 e DC02 se la piattaforma scelta prevede autenticazione amministrativa integrata con Active Directory.

### Servizio multimediale

#### Obiettivo
MEDIA01 fornisce un punto unico per pubblicare, aggiornare e controllare i contenuti mostrati ai clienti. La gestione centralizzata evita interventi manuali su ogni TV o display e permette di mantenere uniforme la comunicazione del gruppo alberghiero.

Contenuti previsti:
- welcome page hotel;
- informazioni sui servizi della struttura;
- menu, spa, ristorante ed eventi;
- guide turistiche e territorio;
- promozioni e comunicazioni interne;
- contenuti per sale meeting;
- digital signage fuori sala;
- QR code per prenotazioni o comunicazioni con reception.

#### Ambito
MEDIA01 gestisce contenuti prodotti dall'hotel, contenuti acquistati/licenziati e contenuti compatibili con uso commerciale. Non deve distribuire account streaming condivisi dell'hotel.

Lo streaming personale resta a carico dell'ospite tramite account proprio, usando le funzioni della piattaforma Hospitality TV o Smart TV business scelta.

### Hospitality TV

#### Obiettivo
Le Hospitality TV permettono di offrire servizi digitali in camera senza usare Smart TV consumer non gestite. La piattaforma deve supportare gestione centralizzata, profili per struttura e reset delle credenziali ospite a fine soggiorno.

Funzioni attese:
- welcome page personalizzata;
- guida servizi hotel;
- contenuti per hotel, piano, sala o camera;
- app o casting controllato, dove previsto;
- reset account ospite al check-out;
- blocco delle impostazioni non destinate all'ospite;
- aggiornamento contenuti da pannello centralizzato.

#### Strutture coinvolte
La soluzione multimediale riguarda:
- La Meraviglia: Hospitality TV in camera, contenuti centralizzati e promozioni servizi;
- L'Incanto: Hospitality TV o Smart TV business con contenuti informativi e streaming personale;
- Il Sogno: TV nelle mini-case con guide ai servizi, territorio e comunicazioni con reception;
- sale meeting: display informativi, proiezione, videoconferenza e digital signage.

### Sale meeting e digital signage

#### Obiettivo
MEDIA01 supporta la gestione dei contenuti visibili nelle sale meeting e negli spazi comuni. L'obiettivo è fornire informazioni aggiornate su eventi, orari, indicazioni, brand del cliente e comunicazioni operative.

Uso previsto:
- display fuori sala con nome evento e orari;
- contenuti informativi nelle aree comuni;
- materiale promozionale della struttura;
- contenuti temporanei per eventi;
- supporto a videoproiezione e presentazioni quando integrato con la piattaforma scelta.

Le reti meeting restano separate dalle reti aziendali. Gli ospiti degli eventi non devono avere accesso diretto a MEDIA01 o ad altri server interni.

### Gestione contenuti

#### Modello operativo
La gestione dei contenuti deve essere assegnata a utenti autorizzati. Dove possibile, l'accesso amministrativo al CMS sarà integrato con Active Directory.

Gruppi candidati:
- `GG_IT`
- `GG_Direzione`
- `GG_DirezioneGenerale`
- `GG_Marketing`
- `GG_Eventi`

Il modello consigliato è:
- IT: amministrazione tecnica della piattaforma;
- marketing/eventi: caricamento e aggiornamento contenuti;
- direzione: approvazione contenuti e comunicazioni ufficiali;
- reception: eventuali aggiornamenti operativi limitati, se supportati dalla piattaforma.

#### Organizzazione contenuti
I contenuti devono essere organizzati per ambito:

| Ambito | Esempi |
|---|---|
| Gruppo | comunicazioni comuni a tutti gli hotel |
| Hotel | contenuti specifici per Il Sogno, La Meraviglia, L'Incanto |
| Piano/camera | welcome page, guide, servizi locali |
| Sala meeting | evento, orari, indicazioni, brand |
| Mini-case | informazioni reception, territorio, servizi disponibili |

### Sicurezza e rete

#### Accesso consentito
MEDIA01 deve essere raggiungibile solo dai dispositivi e dalle reti autorizzate.

Accesso consentito:
- Hospitality TV e display autorizzati;
- reti multimediali previste dal piano di rete;
- postazioni amministrative autorizzate;
- VPN remota solo per IT e ruoli autorizzati;
- eventuali integrazioni applicative documentate.

Accesso non consentito:
- client guest generici;
- dispositivi personali ospiti;
- tablet camere non autorizzati;
- reti meeting ospiti;
- dispositivi non censiti.

#### Separazione del traffico
Il traffico multimediale e lo streaming ospite non devono saturare la VPN verso il CED. La navigazione Internet, lo streaming personale e il traffico guest devono usare local breakout dalla sede in cui si trovano i dispositivi.

Verso MEDIA01 deve transitare solo il traffico necessario alla gestione o distribuzione dei contenuti interni. Le regole firewall devono essere documentate e limitate alle porte richieste dalla piattaforma scelta.

### Licenze e contenuti

#### Obiettivo
La documentazione finale deve distinguere contenuti tecnici, contenuti prodotti dall'hotel e contenuti soggetti a licenza.

Regole di base:
- non usare account streaming condivisi dell'hotel;
- non archiviare contenuti senza licenza commerciale valida;
- indicare eventuali contenuti acquistati o forniti da terzi;
- preferire contenuti prodotti internamente o Creative Commons compatibili con uso commerciale;
- documentare responsabilità di caricamento, approvazione e rimozione.

Le licenze della piattaforma Hospitality TV o CMS saranno definite nel budget tecnico, distinguendo soluzione minima e soluzione premium.

### Backup e ripristino

#### Obiettivo
MEDIA01 deve essere incluso nelle procedure di backup del CED, soprattutto per configurazione CMS, template, libreria contenuti e mapping dei dispositivi.

La strategia prevista include:
- backup completo della VM;
- export della configurazione CMS, se supportato;
- backup dei contenuti pubblicati;
- documentazione dei dispositivi associati;
- snapshot prima di aggiornamenti importanti;
- procedura di ripristino della piattaforma e dei contenuti.

I contenuti originali e le licenze devono essere conservati in modo ordinato, così da poter ricostruire rapidamente il servizio in caso di guasto.

### Dipendenze

MEDIA01 dipende da:
- DNS interno per risoluzione `media01.corp.ilsogno.it`;
- firewall e VLAN per raggiungibilità controllata;
- VPN site-to-site per gestione dalle sedi remote;
- eventuale Active Directory per account amministrativi;
- storage e backup BK01/NAS;
- piattaforma Hospitality TV o CMS scelta.

MEDIA01 non deve diventare una dipendenza critica per autenticazione, file server o gestionale: se MEDIA01 è indisponibile, l'impatto deve restare limitato ai servizi multimediali.

### Test di accettazione

- MEDIA01 risponde tramite nome DNS `media01.corp.ilsogno.it`.
- Un amministratore autorizzato accede al pannello CMS.
- Un utente non autorizzato non accede al pannello CMS.
- Una TV o display autorizzato riceve i contenuti previsti.
- Un contenuto può essere pubblicato per singolo hotel.
- Un contenuto può essere pubblicato per sala meeting o area comune.
- Le reti guest non raggiungono direttamente il pannello amministrativo.
- Lo streaming personale dell'ospite usa account personale, non account dell'hotel.
- Il reset credenziali ospite è previsto dalla piattaforma Hospitality TV scelta.
- Il traffico guest e streaming usa local breakout e non attraversa inutilmente la VPN centrale.
- La configurazione CMS e i contenuti possono essere ripristinati da backup.
