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
L'utente si trova nella pagina "Carrello" (UC-070).

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

Il totale del carrello è aggiornato

**Varianti / Estensioni:**
---
**Eccezioni / Flussi alternativi:**
---
### E1 Rimozione ultimo prodotto:
    L'eccezione si verifica al termine del punto 4 del flusso principale, quando il sistema rileva che non vi sono più articoli associati al carrello.

    4 - Il sistema elimina l'associazione tra l'articolo e la sessione/profilo dell'utente.

    E1.1 - Il sistema esegue un controllo sul numero di articoli residui nel carrello.

    E1.2 - Il sistema rileva che il conteggio degli articoli è pari a zero.

    Il caso d'uso termina con il reindirizzamento a UC070V2

**Note:**
---