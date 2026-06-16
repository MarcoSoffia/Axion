# Gestione utenti e accessi
  1. Alcuni uffici devono vedere dati di tutti gli hotel, oppure solo la direzione/contabilità centrale?
  Si
  2. La reception di un hotel deve poter accedere alle prenotazioni/servizi degli altri hotel?
Si
  3. L’IT deve essere centralizzato al CED de Il Sogno o ogni sede deve avere autonomia minima?  (Noi la pensiamo centralizzata)
Centralizzato, valutiamo criticità di ridondanza
  4. Gli account devono essere personali per ogni dipendente o esistono postazioni condivise, per esempio reception?
Solo personali, reception si AD, ma gli uffici sono personali
  5. Serve tracciare chi accede/modifica documenti sensibili?
Proposta aggiuntiva al cliente (Es. grafana)
#  Archiviazione e dati
  6. Serve una cartella condivisa unica tra tutti gli hotel?
Si - parte gestionale 
# Sicurezza
  8. Serve proteggere solo PC e server o anche tablet, Smart TV e dispositivi delle camere?
Security by design
  9. Gli accessi da remoto devono essere permessi solo all’IT o anche a direzione/contabilità?
Si per direzione, contabilità e IT
  10. Serve autenticazione forte per VPN/accessi remoti? (MFA, 2FA)
Gestiamo noi
#  Mini-case de Il Sogno
  11. Le mini-case devono essere gestite come piccole reti autonome o come estensione controllata della rete aziendale? (Accedono al media server tramite api pubbliche dietro Autenticazione oppure sono nella vpn?)
VPN + internet
  12. In caso di guasto della connessione, quali servizi devono continuare a funzionare?
Certo tipo di ridondanza e facilità di sostituzione, heartbeat che ci notifica rapidamente

# Multimediale e servizi cliente
  14. Il cliente vuole Smart TV normali o Hospitality TV con gestione centralizzata?
Hospitality TV, non possono configurare i propri account sulla smart tv
  15. I tablet in camera servono solo per informazioni o anche per richieste alla reception, prenotazioni spa/ristorante/eventi?
Strettamente servizi hotel, circuito chiuso. 
  16. Per le sale meeting serve solo proiezione/condivisione schermo o anche videoconferenza completa?
Rete a parte per meeting, la gestiamo noi bassa frizione
