# UC-03.3: CAMBIO DI PAGINAZIONE
---
**Attori coinvolti:**
---
A1: Utente (Ospite o Registrato)

**Descrizione:**
---
L'utente naviga tra le diverse "pagine" del catalogo quando il numero di prodotti totali supera la capacità di visualizzazione di una singola schermata.

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
E1: Pagina inesistente: L'utente inserisce manualmente un numero di pagina non consetntito nell'URL; il sistema mostra un errore 404.

**Note:**
---
