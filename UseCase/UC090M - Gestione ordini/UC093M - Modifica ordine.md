# UC-09.3: MODIFICA ORDINE
---
**Attori coinvolti:**
---
A1: Amministratore (Admin)

A2: Utente (Cliente - Limitato)

**Descrizione:**
---
L'attore interviene su un ordine già creato per variarne i contenuti (quantità, indirizzo) o lo stato gestionale.

**Precondizioni:**
---
L'ordine non deve essere ancora in stato "Spedito" o "Concluso".

**Flusso Principale degli Eventi:**
---
1 - L'attore accede al dettaglio dell'ordine (UC-09.2).

2 - L'attore seleziona l'opzione "Modifica".

3 - L'attore varia i dati necessari (es. cambia l'indirizzo di consegna o aggiorna lo stato in "In Spedizione").

4 - Il sistema valida le modifiche e aggiorna il record nel database.

5 - Il sistema invia una notifica automatica via email per informare della variazione.

**Postcondizioni:**
---
I dati dell'ordine vengono aggiornati. Se la modifica riguarda i prezzi, il sistema deve gestire il conguaglio.

**Eccezioni / Flussi alternativi:**
---
E1: Ordine già spedito: Il sistema inibisce la modifica se il pacco è già stato affidato al corriere.