## **Gestione degli utenti e controllo degli accessi**

La gestione delle identità digitali e dei permessi è affidata ad **Active Directory Domain Services (AD DS)**, installato sui Domain Controller della sede centrale. Questa soluzione permette di centralizzare l'amministrazione degli utenti, applicare criteri di sicurezza uniformi e gestire in modo semplice ed efficace tutte le strutture del gruppo alberghiero.

Ad ogni dipendente viene assegnato un **account personale nominativo**, utilizzato per l'accesso ai computer aziendali, alle cartelle condivise, ai servizi di rete e alle applicazioni gestionali. Le credenziali sono individuali e non possono essere condivise, garantendo la tracciabilità delle operazioni eseguite da ciascun utente.

Per semplificare la gestione delle autorizzazioni, gli utenti vengono organizzati in **gruppi di sicurezza** in base alla struttura di appartenenza e al ruolo ricoperto. Sono previsti gruppi dedicati alle Reception, alle Direzioni, al personale di Sicurezza e al reparto IT di ciascun hotel, oltre ai gruppi centrali di Direzione Generale, Segreteria, Contabilità e Marketing.

L'assegnazione dei permessi segue il principio del **Least Privilege (minimo privilegio)**: ogni utente può accedere esclusivamente alle risorse necessarie allo svolgimento delle proprie attività lavorative. Questo approccio riduce il rischio di accessi non autorizzati, limita la possibilità di errori accidentali e migliora la sicurezza complessiva dell'infrastruttura.

Le cartelle condivise sono ospitate sul File Server aziendale e protette mediante autorizzazioni **NTFS** e permessi di condivisione assegnati ai gruppi di Active Directory. In particolare:

* le Reception possono modificare esclusivamente la documentazione relativa alla propria struttura;  
* le Direzioni dei singoli hotel e la Direzione Generale accedono alla documentazione amministrativa e gestionale;  
* il reparto Contabilità dispone dell'accesso ai dati economici e finanziari;  
* il reparto Marketing opera esclusivamente sulle risorse dedicate alla comunicazione aziendale;  
* il personale IT dispone dei privilegi necessari per l'amministrazione dei sistemi e dell'infrastruttura;  
* le cartelle contenenti backup e dati critici sono accessibili esclusivamente agli amministratori di sistema;  
* la cartella **Documenti Comuni** è disponibile in sola lettura a tutto il personale per la consultazione di procedure, modulistica e documentazione condivisa.

L'accesso remoto ai servizi aziendali è consentito esclusivamente al personale autorizzato tramite **VPN** protetta e autenticata. Per il Wi-Fi aziendale viene utilizzata l'autenticazione centralizzata tramite **Active Directory** e **NPS/RADIUS**, consentendo ai dipendenti di utilizzare le stesse credenziali di dominio anche per la connessione alla rete wireless.

La gestione degli account è ulteriormente rafforzata tramite **Group Policy (GPO)**, che permettono di applicare automaticamente criteri di sicurezza comuni a tutti i dispositivi aziendali, come password complesse, blocco automatico della sessione, aggiornamenti di sistema, restrizioni sui dispositivi USB e configurazioni standard degli endpoint.

Questa organizzazione garantisce una gestione centralizzata delle identità, una distribuzione coerente dei permessi, un elevato livello di sicurezza e una struttura facilmente scalabile, in grado di supportare l'espansione futura del gruppo alberghiero mantenendo il pieno controllo degli accessi alle risorse aziendali.

