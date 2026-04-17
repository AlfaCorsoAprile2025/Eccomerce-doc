# UC-07.1: RIMOZIONE DI UN PRODOTTO
---
**Attori coinvolti:**
---
A1: Utente (Ospite o Registrato)

**Descrizione:**
---
L'utente desidera eliminare un articolo precedentemente inserito nel carrello perché non più intenzionato ad acquistarlo. Il sistema deve rimuovere l'istanza del prodotto e aggiornare immediatamente i calcoli economici della sessione.

**Precondizioni:**
---
L'utente si trova nella pagina "Carrello" (UC-07).

È presente almeno un prodotto nel carrello.

**Flusso Principale degli Eventi:**
---
1 - L'utente individua il prodotto da rimuovere nella lista del riepilogo.

2 - L'utente clicca sull'icona di rimozione (es. "Cestino" o pulsante "Rimuovi").

3 - Il sistema richiede una conferma dell'azione (opzionale, per evitare click accidentali).

4 - Il sistema elimina l'associazione tra l'articolo e la sessione/profilo dell'utente.

5 - Il sistema aggiorna dinamicamente la vista del carrello 

6 - Il sistema ricalcola il subtotale.

**Postcondizioni:**
---
Il prodotto non è più visibile nel carrello.

Il database o la sessione vengono aggiornati con la rimozione permanente del record.

**Varianti / Estensioni:**
---
V1: Annulla Rimozione: Immediatamente dopo l'eliminazione, il sistema mostra un messaggio "Prodotto rimosso" con un tasto "Annulla" per ripristinare l'articolo.

**Eccezioni / Flussi alternativi:**
---
E1: Rimozione ultimo prodotto: Se l'utente rimuove l'ultimo articolo presente, il sistema attiva automaticamente la variante V2 del caso d'uso principale (UC-070V2: Carrello vuoto).

**Note:**
---
Se il prodotto rimosso aveva delle varianti specifiche (es. Taglia L), solo quella specifica combinazione viene rimossa, lasciando invariate eventuali altre varianti dello stesso prodotto presenti nel carrello.