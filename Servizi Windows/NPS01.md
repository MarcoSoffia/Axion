NPS01: RADIUS/NPS per Wi-Fi aziendale e VPN

### Ruolo

#### Obiettivo
NPS01 ospita il servizio Network Policy Server di Windows Server e fornisce autenticazione RADIUS centralizzata per Wi-Fi aziendale e accessi VPN.

Il servizio permette di usare Active Directory come sorgente unica delle identità: gli utenti autorizzati accedono alla rete aziendale e alla VPN con account personali, gruppi AD e policy controllate dal CED.

#### Posizionamento
NPS01 sarà eseguito come macchina virtuale sul primo host ESXi, insieme a DC01, FS01 e al server gestionale.

NPS01 si integra con:
- DC01/DC02 per autenticazione e gruppi Active Directory;
- firewall pfSense per VPN e accessi remoti;
- controller Wi-Fi o access point aziendali per autenticazione Wi-Fi;
- logging e monitoring del CED.

### Indirizzamento

#### Rete Server/CED
NPS01 si trova nella rete Server/CED de Il Sogno, secondo il piano di indirizzamento della sede.

- Sede: Il Sogno
- VLAN: 11 - Server_CED
- Rete: `10.30.11.0/27`
- Gateway: `10.30.11.1`

| Server | FQDN | Indirizzo IP | Ruoli principali |
|---|---|---:|---|
| NPS01 | `nps01.corp.ilsogno.it` | `10.30.11.13` | RADIUS/NPS, Wi-Fi aziendale, autenticazione VPN |

L'indirizzo IP e il record DNS sono statici. NPS01 deve risolvere correttamente DC01 e DC02, perché l'autenticazione dipende da Active Directory.

### RADIUS

#### Obiettivo
NPS01 riceve richieste RADIUS da apparati autorizzati e verifica le credenziali degli utenti contro Active Directory.

I client RADIUS previsti sono:
- firewall centrale CED;
- firewall pfSense delle sedi;
- controller Wi-Fi o access point aziendali;
- eventuali apparati VPN autorizzati.

Le reti guest, Smart TV, tablet camere e sale meeting non devono usare NPS01 per autenticazione diretta, salvo casi specifici documentati.

#### Client RADIUS
Ogni apparato che interroga NPS01 deve essere registrato come client RADIUS.

Per ogni client devono essere documentati:
- nome apparato;
- indirizzo IP sorgente;
- sede;
- funzione;
- secret RADIUS;
- policy associata.

I secret RADIUS non devono essere inseriti nella documentazione consegnabile o nel repository.

### Wi-Fi aziendale

#### Obiettivo
Il Wi-Fi aziendale usa NPS01 per autenticare utenti e dispositivi autorizzati. Dove possibile, l'accesso Wi-Fi aziendale sarà integrato con Active Directory.

Questa scelta permette di:
- evitare password Wi-Fi condivise tra tutto il personale;
- revocare l'accesso disabilitando l'account AD;
- assegnare accesso in base ai gruppi;
- tracciare gli accessi tramite log;
- separare Wi-Fi aziendale e Wi-Fi guest.

#### Policy proposta
La policy Wi-Fi aziendale autorizza solo utenti appartenenti ai gruppi AD previsti.

Gruppi candidati:
- `GG_Direzione`
- `GG_DirezioneGenerale`
- `GG_Contabilita`
- `GG_Reception`
- `GG_IT`
- `GG_Sicurezza`
- `GG_Eventi`
- `GG_Marketing`

Il Wi-Fi ospiti resta separato e viene gestito tramite firewall/controller Wi-Fi, senza accesso diretto alle risorse interne.

### VPN

#### Obiettivo
NPS01 supporta l'autenticazione VPN per utenti autorizzati. La VPN è prevista per IT, direzione e contabilità, con accesso controllato alle risorse interne.

La VPN non espone direttamente i server su Internet: l'accesso passa attraverso firewall, autenticazione e regole di autorizzazione.

#### Gruppi autorizzati
L'accesso VPN sarà concesso solo ai gruppi AD autorizzati:

| Gruppo | Uso previsto |
|---|---|
| `GG_IT` | Amministrazione tecnica e gestione infrastruttura |
| `GG_Direzione` | Accesso direzionale alle risorse autorizzate |
| `GG_DirezioneGenerale` | Accesso direzionale centrale |
| `GG_Contabilita` | Accesso ai dati contabili e gestionali autorizzati |

Gli altri gruppi non ricevono accesso VPN salvo approvazione esplicita.

#### MFA
La documentazione di rete prevede VPN remota con MFA. NPS01 gestisce l'autenticazione RADIUS, mentre l'eventuale MFA dipende dalla soluzione VPN/firewall scelta.

Nel documento finale va indicato se l'MFA viene gestito direttamente dal firewall, da un plugin RADIUS compatibile o da un provider esterno.

### Policy NPS

#### Network Policies
Le policy NPS saranno separate per funzione.

| Policy | Uso | Gruppi autorizzati |
|---|---|---|
| WiFi_Aziendale | Accesso Wi-Fi staff | gruppi staff autorizzati |
| VPN_IT | Accesso VPN tecnico | `GG_IT` |
| VPN_Direzione | Accesso VPN direzione | `GG_Direzione`, `GG_DirezioneGenerale` |
| VPN_Contabilita | Accesso VPN contabilità | `GG_Contabilita` |

Le policy devono applicare il principio del minimo privilegio: l'autenticazione abilita l'accesso, ma le regole firewall definiscono quali reti e servizi sono raggiungibili.

#### Connection Request Policies
Le richieste saranno accettate solo da client RADIUS registrati. Richieste provenienti da IP non autorizzati devono essere rifiutate.

### Sicurezza e rete

#### Accesso consentito
NPS01 deve essere raggiungibile solo dagli apparati che inviano richieste RADIUS.

Accesso consentito:
- firewall centrale CED;
- firewall pfSense delle sedi;
- controller Wi-Fi o access point aziendali;
- apparati VPN autorizzati.

Accesso non consentito:
- client guest;
- Smart TV;
- tablet camere;
- reti camere;
- sale meeting ospiti;
- dispositivi non gestiti.

#### Dipendenze
NPS01 dipende da:
- DC01/DC02 per autenticazione AD;
- DNS interno per risoluzione del dominio;
- firewall/VPN per ricezione richieste RADIUS;
- gruppi AD per autorizzazione;
- logging e monitoraggio per diagnosi accessi.

### Logging e auditing

#### Obiettivo
NPS01 deve registrare accessi riusciti, accessi negati ed errori di autenticazione. I log sono essenziali per troubleshooting Wi-Fi/VPN e per verificare tentativi di accesso non autorizzati.

Eventi da tracciare:
- autenticazioni Wi-Fi riuscite;
- autenticazioni Wi-Fi negate;
- autenticazioni VPN riuscite;
- autenticazioni VPN negate;
- client RADIUS non riconosciuti;
- errori di comunicazione con DC01/DC02;
- policy non corrispondenti.

I log devono essere consultabili dall'IT e, se previsto dalla soluzione premium, integrati con monitoring centralizzato.

### Backup e ripristino

#### Obiettivo
NPS01 deve essere incluso nelle procedure di backup del CED.

La strategia prevista include:
- backup completo della VM;
- export periodico della configurazione NPS;
- documentazione dei client RADIUS;
- documentazione delle policy NPS;
- ripristino verificato in ambiente di test o durante finestra controllata.

I secret RADIUS devono essere custoditi in modo sicuro e non salvati in chiaro nella documentazione tecnica condivisa.

### Test di accettazione

- Un utente autorizzato accede al Wi-Fi aziendale tramite credenziali AD.
- Un utente non autorizzato non accede al Wi-Fi aziendale.
- Un utente `GG_IT` accede alla VPN.
- Un utente non appartenente ai gruppi VPN autorizzati viene rifiutato.
- Un client RADIUS non registrato viene rifiutato.
- Spegnimento DC01: NPS01 autentica usando DC02.
- I log mostrano accessi riusciti, accessi negati ed eventuali errori.
- Le reti guest, Smart TV e tablet camere non usano NPS01 come autenticazione diretta.
