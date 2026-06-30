#### Firewall NGFW

Il **Next-Generation Firewall (NGFW)** rappresenta l'evoluzione del classico firewall di rete. Un firewall tradizionale si occupa di gestire il traffico attraverso l'analisi dell'indirizzo IP sorgente, IP destinazione e porta (Layer 3-4 stack OSI). Un NGFW esamina il **contenuto** del traffico e capisce **quale applicazione** lo sta generando (fino al Layer 7).

##### Architettura Hardware

Un NGFW per poter analizzare gigabit di traffico al secondo in tempo reale senza rallentare la navigazione degli utenti, sfrutta hardware altamente specializzato. I componenti principali sono:

**Chipset Dedicati (ASIC / SPU):** Questo chip è il cuore dei firewall NGFW enterprise. Invece di far gravare tutto il lavoro sulla CPU principale, i produttori integrano chip custom chiamati **ASIC** (Application-Specific Integrated Circuit). Ad esempio, Fortinet utilizza i _Network Processor (NP)_ per gestire il routing alla velocità del cavo e i _Content Processor (CP)_ per accelerare la decrittografia dei dati e la scansione antivirus a livello hardware.
    
**Interfacce di Rete ad Alta Densità:** I moduli d'interfaccia (SFP+, SFP28, QSFP28) non sono collegati a bus standard, ma sono interconnessi direttamente ai chip di accelerazione per ridurre la latenza a pochi microsecondi.
    
**Componenti di Grado Enterprise:** Alimentatori ridondanti estraibili a caldo (_hot-swap_), ventole ad alta efficienza e storage a stato solido (NVMe) dedicato esclusivamente al logging intensivo degli eventi.
    
##### Funzionamento Software

Il software di un NGFW sfrutta una funzionalità chiamata **DPI (Deep Packet Inspection)**, la quale permette di analizzare il contenuto dei pacchetti oltre alla loro sorgente e destinazione.

**Application Awareness (Riconoscimento delle Applicazioni):** Il software identifica l'applicazione esatta indipendentemente dalla porta utilizzata. Se un utente usa la porta standard dell'HTTPS (443) per avviare una sessione di gioco su Steam o per scaricare file da BitTorrent, il NGFW riconosce la firma del traffico applicativo e può bloccarla, lasciando invece passare l'home banking sulla stessa porta.
    
**Ispezione SSL/TLS (Decrittazione del traffico):** Oggi oltre l'80% del traffico web è cifrato. I malware sfruttano la cifratura per nascondersi. Il software del NGFW effettua una decrittazione "Inbound" o "Outbound" agendo come un proxy trasparente: apre il pacchetto cifrato, lo scansiona con l'antivirus integrato e, se è pulito, lo richiude inviandolo al destinatario.
    
**Sandboxing e Threat Intelligence Centralizzata:** Se il motore IPS (Intrusion Prevention System) del firewall intercetta un file sconosciuto, il software lo isola e lo invia a un'infrastruttura Cloud protetta (la _Sandbox_). Qui il file viene eseguito in un ambiente virtuale per osservarne il comportamento: se si rivela essere un ransomware, il cloud notifica immediatamente il firewall che blocca il download e aggiorna le regole di sicurezza di tutti i dispositivi della stessa marca nel mondo.