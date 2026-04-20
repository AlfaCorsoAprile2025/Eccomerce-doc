# UC-080: EFFETTUARE CHECKOUT E PAGAMENTO
---
**Attori coinvolti:**
---
A1: Utente (Registrato o Ospite con email)

A2: Gateway di Pagamento Esterno (es. Stripe, PayPal)

**Descrizione:**
---
L'utente, dopo aver revisionato il carrello, decide di finalizzare l'acquisto. Il sistema deve guidare l'utente attraverso l'inserimento dei dati di spedizione e l'esecuzione del pagamento sicuro, trasformando infine il carrello in un ordine confermato.

**Precondizioni:**
---
Il carrello contiene almeno un prodotto (UC-070).

L'utente è autenticato (UC-020) o ha fornito un indirizzo email valido per il checkout come ospite.

Flusso Principale degli Eventi:
---
1 - L'utente clicca su "Procedi al Checkout" dalla pagina del carrello.

2 - Il sistema richiede o conferma l'indirizzo di spedizione.

3 - L'utente inserisce l'indirizzo

4 - Il sistema valida l'indirizzo

5 - Il sistema calcola il totale finale (Subtotale + Spedizione + Tasse).

6 - L'utente seleziona un metodo di pagamento (es. Carta di Credito, PayPal).

7 - Il sistema reindirizza l'utente al Gateway di Pagamento Esterno (A2) o apre un modulo sicuro.

8 - L'utente inserisce i dati e conferma il pagamento.

9 - Il sistema riceve la conferma dal Gateway (A2).

10 - Il sistema genera l'ordine nel database

11 - Il sistema svuota il carrello

**Postcondizioni:**
---
Viene creato un nuovo record "Ordine" con stato "Pagato" .

Lo stock dei prodotti acquistati viene decrementato nel database.

Viene inviata un'email di conferma all'utente.

**Varianti / Estensioni:**
---

### V1 Indirizzi Salvati:
    Questa variante interviene al punto 2 del flusso principale per semplificare l'esperienza degli utenti autenticati.

    2 - Il sistema deve acquisire l'indirizzo di spedizione.

    V1.1 - Il sistema rileva che l'utente è registrato e possiede indirizzi salvati nel profilo.

    V1.2 - Il sistema mostra una lista di indirizzi predefiniti (es. "Casa", "Ufficio") con i relativi dettagli.

    V1.3 - L'utente seleziona l'indirizzo desiderato con un click.

    V1.4 - Il sistema compila automaticamente tutti i campi del modulo di spedizione.

    Il flusso prosegue regolarmente al punto 4.
**Eccezioni / Flussi alternativi:**
---
### E1 Pagamento Rifiutato:
    L'eccezione si verifica tra il punto 8 e il punto 9 del flusso principale, a seguito di un problema comunicato dal Gateway finanziario.

    8 - L'utente inserisce i dati e conferma il pagamento sul Gateway (A2).

    E1.1 - Il Gateway (A2) restituisce un esito negativo (es. fondi insufficienti, carta scaduta, errore 3D Secure).

    E1.2 - Il sistema intercetta l'errore e interrompe la generazione dell'ordine prevista al punto 10.

    E1.3 - Il sistema reindirizza l'utente alla pagina di selezione del metodo di pagamento (punto 6).

    E1.4 - Il sistema visualizza un messaggio di errore descrittivo (es: "Il pagamento è stato rifiutato dall'istituto di credito. Verifica i dati o usa un altro metodo").

    Il flusso torna al punto 6 del flusso principale.

### E2 Indirizzo non servito:
    L'eccezione si verifica al punto 3 del flusso principale, durante il calcolo della logistica.

    2 - L'utente inserisce o conferma l'indirizzo di spedizione.

    E2.1 - Il sistema invia i dati (CAP e Nazione) al modulo di calcolo delle spedizioni.

    E2.2 - Il sistema rileva che l'area geografica indicata non è coperta da alcun corriere configurato.

    E2.3 - Il sistema blocca il passaggio al punto 4 (selezione metodo di spedizione).

    E2.4 - Il sistema visualizza un messaggio di errore bloccante (es: "Spiacenti, non effettuiamo spedizioni verso il CAP inserito").

    Il flusso torna al punto 2 del flusso principale per permettere la modifica dell'indirizzo.

**Note:**
---
Sicurezza: Il sistema non deve mai memorizzare i dati sensibili delle carte di credito (es. CVV) sui propri server, delegando tutto al Gateway (PCI-DSS compliance).

Regola di Business: L'ordine viene considerato "concluso" solo dopo la ricezione del webhook o della notifica asincrona di successo dal fornitore di pagamento.