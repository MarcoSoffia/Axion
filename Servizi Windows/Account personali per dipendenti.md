## **Account personali per i dipendenti**

Ogni dipendente del gruppo alberghiero dispone di un **account personale nominativo**, creato e gestito tramite **Active Directory Domain Services (AD DS)**. L'account rappresenta l'identità digitale dell'utente all'interno dell'infrastruttura aziendale e consente l'accesso ai dispositivi, alle applicazioni e alle risorse autorizzate.

Gli account vengono creati seguendo una convenzione di denominazione uniforme e sono associati ai gruppi di sicurezza corrispondenti al ruolo e alla struttura di appartenenza. In questo modo l'assegnazione dei permessi avviene automaticamente tramite l'appartenenza ai gruppi, evitando configurazioni manuali per i singoli utenti e semplificando la gestione dell'infrastruttura.

Le credenziali sono strettamente personali e non possono essere condivise. Ogni accesso è riconducibile al singolo dipendente, garantendo la tracciabilità delle operazioni effettuate e facilitando le attività di auditing e controllo.

Per aumentare il livello di sicurezza vengono applicate specifiche politiche di autenticazione, tra cui:

* password complesse conformi ai criteri aziendali;  
* obbligo di modifica della password al primo accesso;  
* scadenza periodica delle credenziali;  
* blocco temporaneo dell'account dopo un numero definito di tentativi di accesso non riusciti;  
* divieto di riutilizzare le password utilizzate in precedenza.

Gli account vengono gestiti durante tutto il loro ciclo di vita. Alla creazione di un nuovo dipendente vengono automaticamente assegnati i gruppi di appartenenza e le relative autorizzazioni. In caso di cambio di mansione o trasferimento presso un'altra struttura, è sufficiente modificare l'appartenenza ai gruppi di sicurezza per aggiornare i permessi disponibili. Alla cessazione del rapporto di lavoro l'account viene immediatamente disabilitato e successivamente rimosso secondo le procedure aziendali.

Gli stessi account vengono utilizzati anche per l'autenticazione ai servizi aziendali, tra cui il Wi-Fi interno tramite **NPS/RADIUS**, l'accesso remoto tramite **VPN** per il personale autorizzato e le applicazioni gestionali integrate con Active Directory, offrendo così un sistema di autenticazione centralizzato (**Single Sign-On**) che migliora sia la sicurezza sia l'esperienza d'uso.

Questa modalità di gestione consente di amministrare in modo centralizzato tutte le identità digitali del personale, ridurre il rischio di errori nella configurazione dei permessi e garantire un elevato livello di sicurezza e controllo sull'intera infrastruttura informatica del gruppo alberghiero.

