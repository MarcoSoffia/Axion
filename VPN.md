Basandoci sulla topologia e sui requisiti definiti nella progettazione dei firewall (Cluster HA al CED con Netgate 8200 MAX, Netgate 6100, Netgate 4200 e Netgate 1100), la soluzione scelta per i tre hotel è la tecnologia VPN con protocollo IPSec con IKEv2e il protocollo WireGuard per le mini-case.

#### Connessioni VPN Site-to-Site (IPsec IKEv2)

Le connessioni **Site-to-Site** collegano in modo permanente le reti LAN locali dei due hotel periferici con il CED centrale presso l'hotel _Il Sogno_.

Vengono instaurati due tunnel IPsec principali:
- _La Meraviglia_ $\leftrightarrow$ _CED (Il Sogno)
-  _L'Incanto_ $\leftrightarrow$ _CED (Il Sogno)_

**Puntamento all'IP Virtuale (Alta Affidabilità):** I firewall di filiale (_La Meraviglia_ e _L'Incanto_) non punteranno all'indirizzo IP pubblico del singolo firewall del CED, ma all'**IP Virtuale CARP WAN** del cluster. In questo modo, se il firewall Master del CED fallisce, il tunnel si ricollega automaticamente al firewall di Backup in una frazione di secondo.
**Local Breakout (Navigazione Ospiti):** Le regole di routing sui firewall periferici instraderanno attraverso il tunnel IPsec solo il traffico aziendale e gestionale (es. verso la VLAN 20 Amministrazione o verso i server/NAS del CED). Il traffico internet degli ospiti (VLAN 50, sale meeting) e delle Smart TV uscirà direttamente tramite la connessione internet locale di ciascun hotel (_local breakout_), evitando di sovraccaricare la VPN e la banda del CED.

Per garantire massima sicurezza e sfruttare l'accelerazione hardware dei processori Intel/Netgate, utilizzeremo lo standard **IKEv2** con i seguenti parametri:

**Fase 1 (Autenticazione e Scambio Chiavi):**
-  _Algoritmo di Crittografia:_ AES-GCM con chiave a 256 bit (estremamente sicuro e ottimizzato hardware).
-  _Funzione di Hash:_ SHA256 o SHA384.
-  _Gruppo Diffie-Hellman (DH):_ Gruppo 14 (2048-bit) o superiore (es. Gruppo 19 - Curve Ellittiche).
**Fase 2 (Protezione dei Dati - IPsec):**
-  _Protocollo:_ ESP (Encapsulating Security Payload).
-  _Algoritmo:_ AES-GCM (256 bit).
-  _PFS (Perfect Forward Secrecy):_ Abilitato (Gruppo 14 o 19) per garantire che la compromissione di una chiave non comprometta le sessioni passate.
#### Connessioni VPN Client-to-Site (Lavoratori Remoti / Direzione)

Per permettere al personale autorizzato, alla direzione generale o ai tecnici di lavorare da remoto (es. da casa o durante i viaggi), configuriamo l'accesso **Client-to-Site** sul Cluster pfSense del CED.

Le tecnologie proposte hanno una doppia scelta per una questione di flessibilità:
-  **IPsec IKEv2 EAP-MSCHAPv2:** Ideale perché nativamente supportato da quasi tutti i sistemi operativi moderni (Windows, macOS, iOS) senza dover installare software o client aggiuntivi sul computer dell'utente.
-  **OpenVPN / WireGuard Road Warrior:** Ottima alternativa tramite app dedicata per una gestione granulare degli accessi.

I requisiti di sicurezza integrati (MFA) seguiranno le seguenti configurazioni:

-  **Autenticazione a Due Fattori (MFA / 2FA):** l'accesso non avverrà solo tramite password bensì con l'implementazione di un secondo livello di sicurezza. Configureremo pfSense per interfacciarsi con un server di autenticazione (es. RADIUS) per richiedere nome utente e password aziendale e un codice OTP generato sul proprio smartphone tramite servizi web (es. Google Authenticator).
-  **Controllo degli Accessi (Firewall ACL):** Una volta connesso, l'utente remoto verrà inserito in una specifica subnet VPN. Regole rigide sul pfSense del CED stabiliranno cosa può vedere.
#### Connessioni Mini-Case (WireGuard Site-to-Site)

Per l'infrastruttura di rete delle 15 mini-case dislocate sul territorio dell'Albergo Diffuso "Il Sogno" utilizziamo il protocollo **WireGuard** anzichè IPSec. La scelta è stata fatta sulla base dello scenario proposto:

-  **Leggerezza e Velocità:** WireGuard ha un codice estremamente snello ed è incredibilmente efficiente su hardware compatti (come i piccoli router).
-  **Resilienza alle Disconnessioni:** Le mini-case sono collegate tramite una rete wireless distribuita sul territorio. WireGuard gestisce i cambi di IP o i micro-blackout della rete wireless in modo nativo e trasparente, senza dover "ricostruire" il tunnel da zero come fa IPsec, garantendo una connessione stabile.
-  **Configurazione Hub-and-Spoke:** Il Cluster pfSense del CED agirà da "Hub" (Server centrale sempre in ascolto). Ogni mini-casa agirà da "Spoke" (Client peer).
-  **Isolamento e Gestione:** Ogni mini-casa avrà una micro-subnet dedicata (es. `/30` o `/29`). Tramite il tunnel WireGuard, i tecnici informatici dal CED (VLAN 10) o dallo staff operativo (VLAN 30) potranno raggiungere direttamente l'interfaccia di gestione interna della singola mini-casa per attività di manutenzione o per monitorare la domotica.













