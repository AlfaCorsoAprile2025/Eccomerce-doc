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
V1: Rimozione Articolo: L'utente clicca sull'icona "Rimuovi" (Cestino); il sistema elimina l'articolo e ricalcola il totale.

V2: Carrello vuoto: Se l'utente rimuove tutti i prodotti, il sistema mostra un messaggio "Il tuo carrello è vuoto" e un pulsante "Torna allo shopping".
**Eccezioni / Flussi alternativi:**
---
E1: Quantità non disponibile: L'utente prova a inserire una quantità superiore allo stock; il sistema mostra un avviso e riporta la quantità al valore massimo disponibile.

E2 : Uno dei prodotto del carrello viene rimosso o bloccato da un amministratore, non deve essere visualizzato nel carrello

E3: Prodotto non più disponibile: Un prodotto nel carrello diventa esaurito mentre l'utente naviga; il sistema evidenzia l'articolo come "Non disponibile" e impedisce il checkout finché non viene rimosso.

**Note:**
---
Persistenza: Per gli utenti registrati, il carrello deve essere persistente tra diversi dispositivi (salvato su DB). Per gli ospiti, viene solitamente gestito tramite Cookie o LocalStorage.

Regola di Business: Il calcolo delle spese di spedizione definitive viene solitamente rimandato alla fase di Checkout, poiché dipende dall'indirizzo di consegna.