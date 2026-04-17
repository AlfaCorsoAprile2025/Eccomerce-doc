# UC-09: VISUALIZZAZIONE ORDINI
---
**Attori coinvolti:**
---
A1: Utente Autenticato (Cliente)

A2: Amministratore (Admin)

**Descrizione:**
---
L'attore desidera consultare lo storico o il dettaglio degli acquisti effettuati sulla piattaforma. Il sistema deve mostrare una lista di ordini con i relativi stati (es. In lavorazione, Spedito, Consegnato)

**Precondizioni:**
---
L'attore deve aver effettuato il login con successo (UC-02).

Devono esistere ordini registrati nel database del sistema.

**Flusso Principale degli Eventi:**
---
L'attore accede alla sezione "I miei ordini" (Cliente) o "Gestione Ordini" (Admin).

Il sistema interroga il database applicando i filtri di visibilità in base al ruolo dell'attore.

Il sistema mostra una lista sintetica degli ordini (ID Ordine, Data, Totale, Stato).

L'attore seleziona un ordine specifico per vederne i dettagli.

Il sistema visualizza la scheda completa dell'ordine inclusi i prodotti acquistati, l'indirizzo di spedizione e il metodo di pagamento utilizzato.

**Postcondizioni:**
---
L'attore ha ottenuto le informazioni aggiornate sullo stato degli acquisti.

**Varianti / Estensioni:**
---
V1: Filtro per Stato: L'attore filtra gli ordini per visualizzare solo quelli "Spediti" o "In attesa di pagamento".

V2: Download Fattura: Se l'ordine è in stato "Completato", l'attore può scaricare il documento fiscale in formato PDF.

V3: Ricerca Avanzata (Admin): L'amministratore cerca un ordine specifico tramite ID, nome cliente o intervallo di date.

**Eccezioni / Flussi alternativi:**
---
E1: Nessun ordine trovato: Se l'utente non ha mai effettuato acquisti, il sistema mostra il messaggio "Non hai ancora effettuato ordini" con un link al catalogo.

E2: Accesso Negato: Un utente prova ad accedere tramite URL diretto all'ordine di un altro utente; il sistema blocca l'operazione e mostra un errore di autorizzazione.

**Note:**
---
Regola di Visibilità (Multi-tenancy): Questa è la logica cruciale del caso d'uso:

L'Utente Cliente (A1) può visualizzare esclusivamente gli ordini associati al proprio ID utente (clausola WHERE user_id = CURRENT_USER).

L'Amministratore (A2) ha una visuale globale e può visualizzare tutti gli ordini di tutti gli utenti registrati nel sistema, senza restrizioni di appartenenza.