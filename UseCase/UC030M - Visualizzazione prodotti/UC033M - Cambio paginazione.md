# UC-03.3: CAMBIO DI PAGINAZIONE
---
**Attori coinvolti:**
---
A1: Utente (Ospite o Registrato)

**Descrizione:**
---
L'utente naviga tra le diverse "pagine" del catalogo quando il numero di prodotti totali supera la capacità di visualizzazione di una singola schermata. Può modificare il numero di prodotto visualizzati e la pagina su cui si trova.

**Precondizioni:**
---
Il numero di prodotti trovati è superiore al limite di prodotti per pagina impostato (es. > 24 prodotti).

**Flusso Principale degli Eventi:**

1 - L'utente scorre fino alla fine della lista prodotti.

2 - L'utente cambia il numero di elementi visualizzati.

3 - Il sistema carica i nuovi prodotti e riporta lo scroll dell'utente all'inizio della lista.

4 -Il sistema aggiorna l'URL (es. ?page=2) per permettere la condivisione del link.

**Postcondizioni:**
---
Viene visualizzato il set successivo di prodotti mantenendo i filtri e l'ordinamento precedentemente impostati.

**Varianti / Estensioni:**
---

**Eccezioni / Flussi alternativi:**
---
### E1 Pagina inesistente:

    L'eccezione si verifica al punto 2

    1 - L'utente tenta di modificare i prodotti visualizzati specificando la pagina nell'URL (es. ?page=999).

    E1.1 - Il sistema riceve la richiesta e calcola il numero massimo di pagine disponibili in base ai prodotti totali e al limite per pagina.

    E1.2 - Il sistema rileva che il numero di pagina richiesto è superiore al massimo consentito o è un valore non numerico/negativo.

    E1.3 - Il sistema interrompe il caricamento dei prodotti previsto al punto 3.

    E1.4 - Il sistema visualizza una pagina di errore 404 (Not Found)

### E2 Paginazione non valida: 

    L'eccezione si verifica al punto 2

    1 - L'utente tenta di modificare i prodotti visualizzati specificando il numero di elementi visualizzati nell'URL (es. ?limit=999).

    E1.1 - Il sistema riceve la richiesta e verifica il numero di elementi sia consentito

    E1.2 - Il sistema rileva che il numero non è consentito

    E1.3 - Il sistema interrompe il caricamento dei prodotti previsto al punto 3.

    E1.4 - Il sistema visualizza una pagina di errore 404 (Not Found)


**Note:**
---
