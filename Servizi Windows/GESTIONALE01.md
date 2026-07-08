GESTIONALE01: server gestionale servizi hotel

### Ruolo

#### Obiettivo
GESTIONALE01 ospita o integra il software gestionale alberghiero usato per prenotazioni, camere, check-in/check-out, anagrafiche clienti, servizi e attività operative della reception.

Il servizio permette al personale autorizzato di lavorare su un sistema centrale, raggiungibile dalle reti aziendali e dalle sedi remote tramite VPN site-to-site. La scelta del software resta flessibile: si può integrare il gestionale già usato dal cliente oppure valutare una soluzione a licenza / open source.

#### Posizionamento
GESTIONALE01 sarà eseguito come macchina virtuale sul primo host ESXi, insieme a DC01, FS01 e NPS01.

Se il cliente usa già un gestionale SaaS, la VM può essere convertita come supporto di servizi oppure per spazio. 

### Indirizzamento

#### Rete Server/CED
GESTIONALE01 si trova nella rete Server/CED de Il Sogno, secondo il piano di indirizzamento della sede.

- Sede: Il Sogno
- VLAN: 11 - Server_CED
- Rete: `10.30.11.0/27`
- Gateway: `10.30.11.1`

| Server | FQDN | Indirizzo IP | Ruoli principali |
|---|---|---:|---|
| GESTIONALE01 | `gestionale01.corp.ilsogno.it` | `10.30.11.16` | Gestionale hotel, prenotazioni, servizi reception |


### Software gestionale

#### Opzione preferibile
Se il cliente usa già un gestionale alberghiero, la scelta più prudente è integrarlo nell'infrastruttura proposta senza forzare una migrazione non necessaria.

Questa opzione riduce il rischio operativo, perché il personale continua a usare strumenti già conosciuti. Axion documenta indirizzi, DNS, regole firewall, gruppi autorizzati, accesso VPN e backup, inserendo il gestionale in un perimetro più ordinato e protetto.

#### Opzione open source
Una possibile alternativa open source è HotelDruid, un PMS web per strutture ricettive rilasciato con licenza AGPL.

Costo licenza:
- software self-hosted: `0 euro` di licenza;
- costi da prevedere: installazione, configurazione, formazione, backup, manutenzione e eventuale import dati;
- eventuale hosting/supporto o moduli aggiuntivi: da quotare separatamente in base a camere, servizi e canali richiesti.

### Accessi

#### Gruppi autorizzati
Gli accessi a GESTIONALE01 saranno gestiti con account personali e gruppi Active Directory, dove supportato dal software scelto.

Gruppi candidati:
- `GG_Reception`
- `GG_Direzione`
- `GG_DirezioneGenerale`
- `GG_Contabilita`
- `GG_IT`

La reception usa il gestionale per le attività operative. Direzione e contabilità accedono alle funzioni e ai report autorizzati. IT mantiene l'accesso amministrativo tecnico.

### Sicurezza e rete

#### Accesso consentito
GESTIONALE01 deve essere raggiungibile solo dalle reti aziendali autorizzate.

Accesso consentito:
- postazioni reception;
- uffici amministrativi e direzione;
- VPN site-to-site dalle sedi remote;
- VPN remota per ruoli autorizzati;
- server interni che necessitano integrazione documentata.

Accesso non consentito:
- guest Wi-Fi;
- Smart TV;
- tablet camere non autorizzati;
- reti meeting ospiti;
- dispositivi personali ospiti;
- dispositivi non censiti.

Se il gestionale è SaaS, le regole firewall dovranno permettere solo il traffico necessario verso il fornitore, mantenendo separati guest, dispositivi camere e reti aziendali.

### Backup e ripristino

#### Obiettivo
Il gestionale contiene dati operativi critici e deve essere incluso nelle procedure di backup del CED.

La strategia prevista include:
- backup completo della VM;
- backup del database applicativo;
- export periodico dei dati principali;
- snapshot prima di aggiornamenti importanti;
- test di ripristino;
- documentazione delle procedure di export.

### Dipendenze

GESTIONALE01 dipende da:
- DNS interno per risoluzione `gestionale01.corp.ilsogno.it`;
- DC01/DC02 se viene usata autenticazione Active Directory;
- firewall e VLAN per raggiungibilità controllata;
- VPN site-to-site per accesso dalle sedi remote;
- BK01/NAS per backup e ripristino;
- eventuale fornitore esterno se il gestionale è SaaS.

### Test di accettazione

- GESTIONALE01 risponde tramite nome DNS `gestionale01.corp.ilsogno.it`.
- Reception, direzione e contabilità accedono secondo i permessi previsti.
- Un client guest non raggiunge il gestionale.
- I dati del gestionale sono inclusi nella procedura di backup o export.
