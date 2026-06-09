# Rete

- Cartine macro fatta per ogni hotel
	- Predispozione dispositivi (no dettagli)
		- AP, Router, Switch, PC end point, firewall
	- Vlan IoT,
	- CED
		- Due server (Capiamo costi e decidiamo) (rack / "pc normale")
		- Condizionatore
- Soluzione Wireless, wifi guest (n camera), wifi aziendale (se possibile stessa psw della AD)
- I tablet erogano servizi dell'hotel, se uno vuole internet si connette con il proprio device al wifi dell'hotel
- Smart TV hanno sia i contenuti multimediali che però internet (es. yt)
- Budget possibile
## Firewall
- firewall serio al ced 
- firewall ok / vpn in tutti gli altri
- case gestite tramite vpn into ced
## VPN
-  Che tecnologia, hostata server da noi con protocollo wireguard / Compriamo paloalto / fortinet / cisco 
# Proposta gestione infra mini-case
- VPN al ced
- Cartina di una mini-casa
- Servizi erogati per smartv + wifi
- 1 router tuttofare 

# Architettura software

## Modalità di gestione degli utenti (gruppi, accessi, etc.)
- Windows server DC, AD
## Soluzione per l’archiviazione, protezione, gestione e condivisione dei dati 
- Windows server scegliamo un servizio (es samba)
## Ulteriori soluzioni per la sicurezza informatica (protezione degli endpoint, etc.)
se un PC della reception, un tablet in camera, una Smart TV, un laptop dell’IT o un server viene compromesso, cosa succede e come lo preveniamo/rileviamo? (aggancio sicurezza nelle diapositive)

"password robuste, aggiornamenti automatici, blocco schermo, account non amministratore per gli utenti normali, disco cifrato sui portatili, disabilitazione di servizi inutili, controllo USB dove necessario." - Tutto gestisto tramite AD e DC

**patch management**  - gestisto tramite AD e DC

## Soluzioni multimediali per le sale meeting/eventi e per le stanze degli hotel.
Capire licenze multimediali, possibilità dell'hotel di includere video e o immagini di guida sul territorio / attività / servizi extra. Scelta del software appropriato

## Soluzione hw/sw per gestione dei servizi ai clienti (prenotazioni di servizi, comunicazioni con la reception, etc…)
Lista totale dei software / tecnologie implementate e come interagiscono.
hw come sopra