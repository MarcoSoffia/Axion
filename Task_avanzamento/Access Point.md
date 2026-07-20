#### Rete Wireless — Cisco Catalyst (Wi-Fi 6 / Wi-Fi 6E)

Per il Wi-Fi abbiamo scelto di usare dispositivi **Cisco Catalyst**. Invece di avere un unico "cervello" che controlla tutti gli access point da lontano, abbiamo preferito mettere un **WLC (Wireless LAN Controller)** in ogni sede: uno nella sala informatica de La Meraviglia, uno nella sala informatica de L'Incanto e uno nel CED de Il Sogno. Il WLC è in pratica il dispositivo che tiene sotto controllo tutti gli access point del suo hotel: decide su che canale devono trasmettere, quanto devono "spingere" il segnale e fa in modo che non si disturbino a vicenda. Il WLC del CED, in più, controlla anche gli access point delle 15 mini-case, collegandosi a loro attraverso i tunnel VPN che abbiamo già previsto nel progetto Firewall/VPN. Tutti gli access point sono **Wi-Fi 6** e vengono alimentati direttamente dagli switch di piano (PoE+), senza bisogno di prese elettriche dedicate.

**Standard, bande e canali:**
-  Tutti gli access point standard (camere, corridoi, aree comuni) usano **Wi-Fi 6**, lo standard più recente e diffuso, più veloce e più stabile con tanti dispositivi connessi insieme rispetto ai vecchi Wi-Fi 4/5.
-  Nelle sale Meeting usiamo access point **Wi-Fi 6E**, che sfruttano anche la banda dei 6 GHz: è una "corsia" di frequenza nuova, quasi vuota, perfetta per videochiamate e presentazioni senza interferenze.
-  Banda **2,4 GHz**: la teniamo attiva solo per i dispositivi più vecchi (qualche sensore domotico datato), sui soli canali 1-6-11 che non si sovrappongono tra loro.
-  Banda **5 GHz**: è la banda principale usata da Staff, Ospiti e Camere. Il canale e la potenza di ogni access point vengono scelti automaticamente dal WLC (funzione chiamata **RRM**), così non serve regolarli a mano uno per uno.
-  Banda **6 GHz** (solo sale Meeting): canali larghi (80-160 MHz) per garantire più velocità dove serve davvero.

**Obiettivi di copertura, capacità e segnale:**
-  Il segnale Wi-Fi non deve mai scendere troppo: puntiamo ad almeno **-65 dBm** nei corridoi e nelle aree comuni, e **-67 dBm** al massimo nel punto più lontano di ogni camera (più il numero è vicino allo 0, più il segnale è forte).
-  Tra un access point e l'altro lasciamo una piccola zona di sovrapposizione (15-20%), così quando un ospite cammina per l'hotel il telefono passa da un access point all'altro senza che internet si stacchi un attimo.
-  Ogni access point è pensato per reggere comodamente **25-30 dispositivi collegati** insieme, calcolando 3 dispositivi Wi-Fi a camera/mini-casa più quelli dello staff.
-  Come regola generale mettiamo **1 access point ogni 150-200 m²** nelle zone normali, e molti di più nelle sale Meeting, dove ci sono tante persone sedute vicine (1 access point ogni 15-20 persone).
-  Grazie al RRM, il WLC evita da solo che due access point vicini usino lo stesso canale disturbandosi, quindi non servono i piccoli "ripetitori" (extender) usati nelle soluzioni più semplici.
#### CED Hotel Il Sogno: WLC centrale + copertura reception + mini-case

Il WLC del CED gestisce il Wi-Fi della reception e delle aree comuni de Il Sogno, e in più gestisce da remoto gli access point delle 15 mini-case (modalità che si chiama **FlexConnect/OfficeExtend**), collegandosi tramite il tunnel WireGuard già previsto per le mini-case.
**Soluzione proposta**: 1 WLC nel CED + 2 access point per reception e aree comuni + 16 access point "mesh" da esterno robusti (1 punto centrale sul tetto della reception + 1 per ogni mini-casa), che fanno sia da ponte radio che da Wi-Fi locale.
**Modello consigliato**: Cisco Catalyst 9800-L (WLC) + 2x Cisco Catalyst 9120AXI (reception) + 16x Cisco Catalyst IW9165E Heavy Duty (i nodi mesh da esterno).
**Funzionalità**:
-  Un Solo Dispositivo per Casa: ogni mini-casa ha un solo apparecchio (IW9165E) che riceve il segnale dalla reception e allo stesso tempo fa da Wi-Fi per il tablet e la Smart TV di casa, senza bisogno di due apparecchi separati.
-  Gestione da Remoto: dal CED i tecnici vedono tutti gli access point delle mini-case come se fossero collegati in locale, con segnale, dispositivi connessi e stato di ognuno visibili da un'unica schermata.
-  Rete che si Auto-Ripara: se il collegamento con una mini-casa peggiora, la rete mesh trova da sola un percorso alternativo passando dai nodi vicini.
**Stima economica**: Circa € 36.400 + IVA (WLC + 2 access point reception + 16 access point mesh da esterno).
#### Sala Informatica — Hotel La Meraviglia (100 camere)

Nella sala informatica installiamo il WLC che gestisce tutti gli access point dei 5 livelli dell'hotel (piano terra + 4 piani, circa 650 m² a livello) e delle 3 sale Meeting.
**Soluzione proposta**: 1 WLC locale + access point standard per camere e corridoi su ogni livello + access point più potenti per le sale Meeting + 1 access point dedicato agli ospiti degli uffici.
**Modello consigliato**: Cisco Catalyst 9800-L (WLC) + 30x Cisco Catalyst 9120AXI (6 per livello, piano terra + P1-P4) + 3x Cisco Catalyst 9136I Wi-Fi 6E (uno per sala Meeting) + 1x Cisco Catalyst 9105AXI (ospiti uffici).
**Funzionalità**:
-  Un Access Point, Più Reti: ogni access point trasmette allo stesso tempo la rete delle camere del suo piano e quella degli ospiti, tenendole ben separate anche se viaggiano sullo stesso apparecchio.
-  Sale Meeting Pronte per le Videochiamate: i 3 access point Wi-Fi 6E, uno per sala, usano la banda 6 GHz per reggere tante persone in videoconferenza senza rallentamenti.
-  Wi-Fi che ti Segue: spostandosi dalla camera alla hall, il telefono dell'ospite passa da un access point all'altro senza che la connessione si interrompa, perché il WLC regola tutto in automatico.
**Stima economica**: Circa € 35.350 + IVA.
#### Sala Informatica — Hotel L'Incanto (30 camere)

Nella sala informatica installiamo il WLC che gestisce gli access point dei 3 livelli (piano rialzato + 2 piani, circa 400 m² a livello) e della sala Meeting.
**Soluzione proposta**: 1 WLC locale + access point standard sui 3 livelli + 1 access point più potente per la sala Meeting + 1 access point per gli ospiti degli uffici.
**Modello consigliato**: Cisco Catalyst 9800-L (WLC) + 12x Cisco Catalyst 9120AXI (4 per livello) + 1x Cisco Catalyst 9136I Wi-Fi 6E (sala Meeting) + 1x Cisco Catalyst 9105AXI (ospiti uffici).
**Funzionalità**:
-  Piccolo ma Ben Diviso: ogni livello ha la sua rete camere separata, così un ospite di un piano non riesce a vedere i dispositivi di un altro piano.
-  Sala Meeting Pronta: un solo access point Wi-Fi 6E basta a coprire tutta la sala eventi, anche quando è piena di gente collegata.
-  Rete Regolata in Automatico: il WLC locale gestisce da solo il canale e la potenza dei 14 access point della struttura.
**Stima economica**: Circa € 17.750 + IVA.
#### Come dividiamo il Wi-Fi: reti (SSID), VLAN e regole del firewall

In ogni struttura creiamo 4 reti Wi-Fi (SSID) diverse. Ognuna finisce in una VLAN diversa (cioè una "stanza" di rete separata dalle altre) e ha le sue regole sul firewall, seguendo la stessa logica già usata per il progetto Firewall/VPN:

| Rete Wi-Fi (SSID) | Chi si collega | VLAN | Banda e Login | Cosa può fare (Firewall) |
|------|-------------|------|------------------------|------------------|
| **AX-Staff** | PC e laptop del personale | VLAN 30 Staff_Operations | 5/6 GHz — login con utente e password aziendale + certificato (**WPA2/3-Enterprise + 802.1X**, verificati dal server Active Directory) | Può raggiungere i server del CED (file, gestionale) e navigare su Internet (filtrato); non vede Ospiti né Camere. |
| **AX-Ospiti** | Smartphone e laptop personali dei clienti | VLAN 50 Ospiti_Wi-Fi | 2,4/5 GHz — password semplice + pagina di benvenuto (es. numero di camera) | Solo Internet, niente accesso alle reti interne dell'hotel; gli ospiti non si vedono nemmeno tra loro. |
| **AX-Camere** | Smart TV e Tablet dati in dotazione in camera/mini-casa | VLAN del piano (52-55 a La Meraviglia, 51-53 a L'Incanto, 51 nelle mini-case) | 5 GHz — password dedicata, ogni dispositivo ha un indirizzo IP fisso | Può usare i servizi dell'hotel (es. film, room service) e Internet filtrato; non vede le altre camere né lo Staff. |
| **AX-Tech** | Gli access point stessi, telecamere di sicurezza, sensori domotici | VLAN 10 Management / VLAN 60 Security | 5 GHz — login con certificato digitale (**WPA2/3-Enterprise con EAP-TLS**), più sicuro della semplice password | Raggiungibile solo dai tecnici IT tramite la rete di gestione; Ospiti e Camere non possono vederla; i log vanno al CED. |


