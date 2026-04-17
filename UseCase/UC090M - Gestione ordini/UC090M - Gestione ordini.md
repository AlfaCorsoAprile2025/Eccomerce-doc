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
1 - L'attore accede alla sezione "I miei ordini" (Cliente) o "Gestione Ordini" (Admin).

2 - Il sistema interroga il database applicando i filtri di visibilità in base al ruolo dell'attore. 

3 - Il sistema mostra una lista sintetica degli ordini (ID Ordine, Data, Totale, Stato).

**Postcondizioni:**
---
L'attore ha ottenuto le informazioni aggiornate sullo stato degli acquisti.

**Varianti / Estensioni:**
---


**Eccezioni / Flussi alternativi:**
---
### E1 Nessun ordine trovato:
    L'eccezione si verifica al punto 3 del flusso principale, qualora la query non restituisca record.

    3 - Il sistema tenta di mostrare la lista degli ordini.

    E1.1 - Il sistema rileva che il set di dati restituito dal database è vuoto (count = 0).

    E1.2 - Il sistema inibisce la visualizzazione della tabella o della lista ordini.

    E1.3 - Il sistema visualizza un messaggio informativo ("Non hai ancora effettuato ordini" per il Cliente, o "Nessun ordine trovato con questi filtri" per l'Admin).

    E1.4 - Il sistema mostra un pulsante "Inizia lo shopping" (Cliente) o "Reset filtri" (Admin).

### E2 Accesso Negato (Violazione di Sicurezza):
    L'eccezione si verifica al punto 4, solitamente tramite un tentativo di manipolazione dell'URL (IDIDOR).

    4 - L'attore tenta di accedere a un ordine specifico fornendo un ID ordine (es. tramite link diretto).

    E2.1 - Il sistema recupera l'ordine dal database e identifica il proprietario (user_id).

    E2.2 - Il sistema confronta l'ID del proprietario con l'ID dell'attore corrente.

    E2.3 - Il sistema rileva che l'attore non è l'Admin (A2) E l'ID ordine non appartiene all'attore (A1).

    E2.4 - Il sistema blocca il caricamento della scheda previsto al punto 5.

    E2.5 - Il sistema visualizza un messaggio di errore di autorizzazione ("Accesso negato: non sei autorizzato a visualizzare questo ordine").


**Note:**
---
Regola di Visibilità (Multi-tenancy): Questa è la logica cruciale del caso d'uso:

L'Utente Cliente (A1) può visualizzare esclusivamente gli ordini associati al proprio ID utente (clausola WHERE user_id = CURRENT_USER).

L'Amministratore (A2) ha una visuale globale e può visualizzare tutti gli ordini di tutti gli utenti registrati nel sistema, senza restrizioni di appartenenza.