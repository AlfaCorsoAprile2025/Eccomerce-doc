# UC-07: GESTIONE CARRELLO
---
**Attori coinvolti:**
---
A1: Utente (Ospite o Registrato)

**Descrizione:**
---
L'utente desidera gestire l'elenco dei prodotti selezionati prima di procedere all'acquisto definitivo. Il sistema deve permettere di visualizzare il riepilogo degli articoli, modificare le quantità, rimuovere prodotti e calcolare in tempo reale il subtotale della spesa.

**Precondizioni:**
---
L'utente ha aggiunto almeno un prodotto al carrello (tramite UC-04).

Il sistema ha una sessione attiva (per utenti Ospiti) o un profilo collegato (per utenti Registrati).

**Flusso Principale degli Eventi:**
---
1 - L'utente accede alla pagina "Carrello" tramite l'icona dedicata nell'header.

2 - Il sistema recupera gli articoli salvati nella sessione o nel database.

3 - Il sistema visualizza per ogni articolo: immagine, nome, prezzo unitario, quantità e prezzo totale per riga.

4 - L'utente modifica la quantità di un prodotto tramite selettore numerico.

5 - Il sistema valida la disponibilità a magazzino per la nuova quantità richiesta.

6 - Il sistema ricalcola istantaneamente il subtotale del carrello.

7 - L'utente visualizza un riepilogo dei costi (Subtotale, tasse stimate).

8 - L'utente clicca su "Procedi al Checkout" per avviare la fase d'acquisto.

**Postcondizioni:**
---
Il carrello viene aggiornato nel database o nella sessione.

L'utente viene indirizzato al processo di Checkout (UC-08).

**Varianti / Estensioni:**
---
### V1 Rimozione Articolo:
    La variante può verificarsi in qualsiasi momento dopo la visualizzazione della lista (punto 3).

    1 - L'utente individua l'articolo da eliminare e clicca sull'icona "Rimuovi" (Cestino).

    V1.1 - Il sistema riceve la richiesta di eliminazione per lo specifico ID prodotto.

    V1.2 - Il sistema rimuove il record dell'articolo dalla sessione o dal database.

    V1.3 - Il sistema aggiorna la vista rimuovendo la riga corrispondente.

    V1.4 - Il sistema ricalcola istantaneamente il subtotale (punto 6).

    Il flusso torna al punto 3 o attiva la variante V2 se il carrello risulta vuoto.

### V2 Carrello vuoto:
    La variante si verifica se il sistema non trova articoli al punto 2 o dopo una rimozione totale (V1).

    2 - Il sistema tenta di recuperare gli articoli.

    V2.1 - Il sistema rileva che non sono presenti prodotti nel carrello.

    V2.2 - Il sistema inibisce la visualizzazione della tabella prodotti e del riepilogo costi (punti 3, 6, 7).

    V2.3 - Il sistema visualizza un messaggio informativo ("Il tuo carrello è vuoto").

    V2.4 - Il sistema mostra un pulsante "Torna allo shopping" che reindirizza al catalogo (UC-03).

    Vedere UC030M

**Eccezioni / Flussi alternativi:**
---
### E1 Quantità non disponibile:
    L'eccezione si verifica al punto 5 del flusso principale, a seguito di un tentativo di modifica manuale.

    4 - L'utente aumenta la quantità tramite selettore numerico.

    E1.1 - Il sistema confronta con la disponibilità residua e rileva che la quantità inserita è superiore alle giacenze fisiche di magazzino.

    E1.2 - Il sistema blocca l'inserimento del valore non valido.

    E1.3 - Il sistema mostra un avviso a video (es: "Spiacenti, disponibilità limitata: solo [n] pezzi disponibili").

    E1.4 - Il sistema riporta automaticamente la quantità nel selettore al valore massimo disponibile.

    Il flusso riprende dal punto 6 per aggiornare i calcoli economici.

### E2 Prodotto rimosso o bloccato dall'amministratore:
    L'eccezione si verifica al punto 2 durante il recupero dei dati.

    2 - Il sistema interroga il database/sessione per caricare i prodotti salvati.

    E2.1 - Il sistema identifica un prodotto che è stato eliminato dal catalogo o disattivato centralmente (stato "Hidden" ).

    E2.2 - Il sistema cancella  l'associazione tra quel prodotto e il carrello dell'utente.

    E2.3 - Il sistema visualizza una notifica di aggiornamento (es: "Un articolo nel tuo carrello non è più disponibile ed è stato rimosso").

    Il flusso prosegue al punto 3 con gli articoli rimanenti.

**Note:**
---
Persistenza: Per gli utenti registrati, il carrello deve essere persistente tra diversi dispositivi (salvato su DB). Per gli ospiti, viene solitamente gestito tramite Cookie o LocalStorage.

Regola di Business: Il calcolo delle spese di spedizione definitive viene solitamente rimandato alla fase di Checkout, poiché dipende dall'indirizzo di consegna.