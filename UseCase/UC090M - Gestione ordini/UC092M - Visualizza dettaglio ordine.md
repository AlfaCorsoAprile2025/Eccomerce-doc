# UC-09.2: VISUALIZZAZIONE DETTAGLIO ORDINE
---
**Attori coinvolti:**
---
A1: Utente (Cliente)

A2: Amministratore (Admin)

**Descrizione:**
---
L'attore consulta la scheda tecnica completa di un singolo acquisto per verificare i prodotti scelti, i costi e lo stato della consegna.

**Precondizioni:**
---
L'ordine selezionato deve esistere nel sistema.

**Flusso Principale degli Eventi:**
---
1 - L'attore clicca sul codice identificativo dell'ordine dalla lista generale.

2 - Il sistema recupera i dati della transazione, i dati di spedizione e l'elenco dei prodotti (snapshot dei prezzi al momento dell'acquisto).

3 - Il sistema mostra la cronologia degli stati (es. "Pagamento ricevuto il 10/01", "Affidato al corriere il 11/01").

4 - Il sistema visualizza il riepilogo finanziario totale.

**Postcondizioni:**
---
L'attore visualizza le informazioni granulari dell'ordine.

**Eccezioni**
---
### E1 Ordine non trovato (Not Found):
    L'eccezione si verifica al punto 2 del flusso principale, quando il sistema tenta di interrogare il database con un identificativo non esistente.

    1 - L'attore tenta di accedere al dettaglio tramite un link diretto o un ID digitato manualmente nell'URL.

    E1.1 - Il sistema riceve la richiesta e cerca l'ID ordine nel database.

    E1.2 - Il sistema rileva che l'ID non corrisponde ad alcun record registrato.

    E1.3 - Il sistema interrompe il caricamento previsto al punto 2.

    E1.4 - Il sistema visualizza una pagina di errore 404 ("Ordine non trovato") con un pulsante per tornare alla lista generale degli ordini.

    Il caso d'uso termina con insuccesso.

### E2 Accesso non autorizzato (Unauthorized):
    L'eccezione si verifica tra il punto 1 e il punto 2 del flusso principale, durante la fase di controllo dei permessi.

    1 - L'attore (A1: Cliente) tenta di visualizzare un ordine specifico.

    E2.1 - Il sistema identifica l'utente loggato e recupera l'ID proprietario associato all'ordine richiesto.

    E2.2 - Il sistema rileva che l'ID dell'utente loggato non coincide con il proprietario dell'ordine E che l'utente non ha il ruolo di Amministratore (A2).

    E2.3 - Il sistema blocca immediatamente il recupero dei dati sensibili previsto al punto 2.

    E2.4 - Il sistema visualizza un messaggio di errore di sicurezza ("Accesso negato: non sei autorizzato a visualizzare i dettagli di questo ordine").

    E2.5 - Il sistema registra il tentativo di accesso non autorizzato nei log di sistema per finalità di auditing.

    Il caso d'uso termina con insuccesso.

**Note:**
---
Privacy: Il Cliente (A1) può accedere a questa vista solo se l'ordine gli appartiene; l'Admin (A2) ha accesso illimitato a tutte le schede ordine.