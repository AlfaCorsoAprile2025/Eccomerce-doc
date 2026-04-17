## UC-093M: MODIFICA ORDINE
---
**Attori coinvolti:**
---
A1: Amministratore (Admin)
A2: Utente (Cliente - Limitato)

**Descrizione:**
---
L'attore interviene su un ordine esistente per aggiornare le informazioni di consegna, la composizione del carrello o lo stato logistico. Il sistema deve garantire che ogni modifica sia congruente con le giacenze di magazzino e con le policy di spedizione.

**Precondizioni:**
---
L'ordine non deve essere ancora in stato "Spedito" o "Concluso".
L'attore deve essere autenticato.

**Flusso Principale degli Eventi:**
---
1 - L'attore accede al dettaglio dell'ordine (UC-09.2) e clicca su "Modifica".

2 - Il sistema abilita i campi editabili in base al ruolo:

* Indirizzo di Spedizione: (Nome, Via, CAP, Città, Provincia).

* Quantità Prodotti: Incremento o decremento dei pezzi per riga.

* Rimozione Prodotti: Eliminazione di una riga d'ordine.

* Stato Ordine: (Solo Admin) Aggiornamento della fase gestionale.

3 - L'attore effettua le variazioni desiderate.

4 - L'attore clicca su "Salva Modifiche".

5 - Il sistema esegue la Validazione dei dati:

* Verifica la correttezza formale dell'indirizzo.

* Controlla la disponibilità a magazzino per eventuali aumenti di quantità.

* Ricalcola il totale economico e le tasse.


**Postcondizioni:**
---
I dati dell'ordine sono aggiornati.
Lo stock di magazzino viene riallineato.

**Eccezioni / Flussi alternativi:**
---
### E1 Ordine già spedito:
L'eccezione si verifica al punto 1 del flusso principale.

1 - L'attore tenta di modificare l'ordine.

E1.1 - Il sistema rileva che lo stato dell'ordine è "Spedito" o superiore.

E1.2 - Il sistema disabilita i controlli di modifica e mostra un avviso: "Impossibile modificare un ordine già affidato al corriere".

Il caso d'uso termina con insuccesso.

### E2 Validazione Indirizzo fallita:
L'eccezione si verifica al punto 5 del flusso principale.

5 - Il sistema esegue la validazione dei dati inseriti.

E2.1 - Il sistema rileva un CAP non valido o una combinazione Città/Provincia errata.

E2.2 - Il sistema evidenzia i campi non validi e impedisce il salvataggio.

Il flusso torna al punto 3.

### E3 Mancata disponibilità stock:
L'eccezione si verifica al punto 5 del flusso principale in caso di aumento quantità.

5 - Il sistema controlla le giacenze per i prodotti incrementati.

E3.1 - Il sistema rileva che la quantità richiesta non è disponibile a magazzino.

E3.2 - Il sistema notifica l'errore: "Quantità non disponibile per il prodotto [Nome]".

E3.3 - Il sistema ripristina la quantità precedente nel modulo.

Il flusso torna al punto 3.

### V1 Permessi insufficienti (Restrizioni Cliente):
L'eccezione si verifica al punto 2 del flusso principale.

2 - L'Utente Cliente (A2) accede alla modalità modifica.

E4.1 - Il sistema rileva il ruolo "Cliente".

E4.2 - Il sistema mantiene i campi "Stato Ordine" e "Prezzi unitari" in modalità sola lettura (non modificabili).

Il flusso prosegue regolarmente per i soli campi autorizzati (Indirizzo e Quantità).

**Note:**
---
