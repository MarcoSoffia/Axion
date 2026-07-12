#### Firewall NGFW

Il Next-Generation Firewall (NGFW) rappresenta l'evoluzione del classico firewall di rete. Un firewall tradizionale si occupa di gestire il traffico attraverso l'analisi dell'indirizzo IP sorgente, IP destinazione e porta (Layer 3-4 stack OSI). Un NGFW esamina il contenuto del traffico e capisce quale applicazione lo sta generando (fino al Layer 7).

La progettazione di rete per quanto riguarda i "firewall" si basa sull'ecosistema **pfSense**. Il sistema operativo e motore di questi firewall è **pfSense Plus** (la versione ufficiale, stabile e ottimizzata di pfSense). L'hardware **Netgate** è reso disponibile dalla azienda proprietaria, sviluppatrice e produttrice ufficiale del software pfSense.
#### Hotel Il Sogno: Centro stella / CED 

Il cuore della rete deve gestire i tunnel IPSec delle due filiali e anche 15 tunnel WireGuard simultanei provenienti dalle mini-case, raccogliere tutti i log di sicurezza (logging verso il CED) e smistare il traffico.
**Soluzione proposta**: Cluster in Alta Affidabilità (2x Firewall identici in modalità Active/Passive con CARP).
**Modello consigliato**: Netgate 8200 MAX (Rack 1U).
**Funzionalità**: 
-  Il Centralino delle VPN (IPsec + WireGuard): Grazie al processore Intel a 8 core, riceve i dati criptati da tutti gli hotel e gestisce i 15 micro-tunnel WireGuard stabili e leggeri delle mini-case senza sforzo.
-  Scatola Nera (Log Server): Riceve e memorizza in tempo reale i log di tracciamento inviati dalle filiali (La Meraviglia e L'Incanto) per capire cosa succede sulla rete.
-  Continuità Totale: Se un pezzo si rompe, l'altro subentra in meno di un secondo.
**Stima economica**: Circa € 1.750 + IVA (Totale coppia: ~ € 3.500 + IVA).
#### Focus mini-case dell'Albergo Diffuso "Il Sogno"

Nelle 15 mini-case sparse sul territorio usiamo piccoli router industriali compatibili con WireGuard anziché IPsec, perché è un protocollo moderno, leggerissimo e ideale per dispositivi con risorse hardware limitate.
**Soluzione proposta**: 15x Piccoli Router/Gateway da installare dentro ogni mini-casa.
**Modello consigliato**: Netgate 1100 (o micro-router industriali simili certificati WireGuard).
**Funzionalità**: 
- Micro-Tunnel Blindato: Ogni casetta accende il suo piccolo router che si collega via wireless al territorio e lancia istantaneamente un tunnel WireGuard verso il CED. I tecnici possono così fare manutenzione e i clienti navigano sicuri.
**Stima economica**: Circa € 220 + IVA a dispositivo (Totale per 15 mini-case: ~ € 3.300 + IVA).
#### Hotel La Meraviglia (100 camere)

Viene richiesto la gestione del traffico avanzato (Smart TV/Tablet nelle camere), il supporto opzionale a due linee internet (Dual WAN) e il sistema di rilevamento intrusioni (IDS/IPS come Snort o Suricata), che richiede molta potenza di calcolo.
**Soluzione proposta**: 1x Firewall di fascia media con hardware dedicato all'ispezione dei pacchetti.
**Modello consigliato**: Netgate 6100.
**Funzionalità**: 
-  Cervellone di Controllo (IDS/IPS): Analizza tutto il traffico Internet locale alla ricerca di virus, malware o tentativi di hackeraggio prima che entrino nell'hotel.
-  Doppia Linea (Dual WAN): Permette di collegare due linee internet diverse. Se la principale si guasta, il firewall passa sulla linea di riserva automaticamente.
- Vigile Urbano delle VLAN: Isola e smista i flussi di dati dei clienti, delle Smart TV in camera e dei tablet del personale, mandando i registri (logging) direttamente al CED.
**Stima economica**: Circa € 900 + IVA.
#### Hotel L'Incanto (30 camere)

Struttura basata sulla separazione delle reti, regole di firewall locali e l'invio dei log al centro stella.
**Soluzione proposta**: 1x Firewall compatto ma con porte multi-gigabit per gestire la segmentazione interna.
**Modello consigliato**: Netgate 4200 MAX.
**Funzionalità**: 
- Muri di Separazione (Inter-VLAN): Crea barriere invalicabili tra la rete dello staff, i computer della reception e il Wi-Fi ospiti.
- Postino Sicuro: Spedisce in modo protetto via IPsec i dati aziendali al CED e invia lì i log di sicurezza, mentre fa navigare gli ospiti sul web locale senza appesantire la sede
**Stima economica**: Circa € 600 + IVA.










