# UC-080: EFFETTUARE CHECKOUT E PAGAMENTO
---
**Attori coinvolti:**
---
A1: Utente (Registrato o Ospite con email)

A2: Gateway di Pagamento Esterno (es. Stripe, PayPal)

**Descrizione:**
---
L'utente, dopo aver revisionato il carrello, decide di finalizzare l'acquisto. Il sistema deve guidare l'utente attraverso l'inserimento dei dati di spedizione, la scelta del metodo di consegna e l'esecuzione del pagamento sicuro, trasformando infine il carrello in un ordine confermato.

**Precondizioni:**
---
Il carrello contiene almeno un prodotto (UC-07).

L'utente è autenticato (UC-02) o ha fornito un indirizzo email valido per il checkout come ospite.

Flusso Principale degli Eventi:
---
1 - L'utente clicca su "Procedi al Checkout" dalla pagina del carrello.

2 - Il sistema richiede o conferma l'indirizzo di spedizione e di fatturazione.

3 - Il sistema calcola le opzioni di spedizione disponibili e i relativi costi.

4 - L'utente seleziona il metodo di spedizione desiderato.

5 - Il sistema calcola il totale finale (Subtotale + Spedizione + Tasse).

6 - L'utente seleziona un metodo di pagamento (es. Carta di Credito, PayPal).

7 - Il sistema reindirizza l'utente al Gateway di Pagamento Esterno (A2) o apre un modulo sicuro.

8 - L'utente inserisce i dati e conferma il pagamento.

9 - Il sistema riceve la conferma dal Gateway (A2).

10 - Il sistema genera l'ordine nel database, svuota il carrello e mostra la pagina di conferma.

**Postcondizioni:**
---
Viene creato un nuovo record "Ordine" con stato "Pagato" o "In lavorazione".

Lo stock dei prodotti acquistati viene decrementato nel database.

Viene inviata un'email di conferma all'utente.

**Varianti / Estensioni:**
---
V1: Utilizzo Coupon/Codice Sconto: L'utente inserisce un codice promozionale; il sistema valida il codice e aggiorna il totale prima del pagamento.

V2: Indirizzi Salvati: Se l'utente è registrato, il sistema propone automaticamente gli indirizzi usati in precedenza.

**Eccezioni / Flussi alternativi:**
---
E1: Pagamento Rifiutato: Il Gateway (A2) comunica che la transazione non è andata a buon fine. Il sistema informa l'utente e permette di riprovare con un altro metodo.

E2: Sessione Scaduta: Se l'utente impiega troppo tempo, il sistema potrebbe richiedere un aggiornamento della pagina per verificare che i prezzi o lo stock non siano cambiati.

E3: Indirizzo non servito: L'utente inserisce un CAP non coperto dai corrieri; il sistema blocca il checkout e richiede un indirizzo diverso.

**Note:**
---
Sicurezza: Il sistema non deve mai memorizzare i dati sensibili delle carte di credito (es. CVV) sui propri server, delegando tutto al Gateway (PCI-DSS compliance).

Regola di Business: L'ordine viene considerato "concluso" solo dopo la ricezione del webhook o della notifica asincrona di successo dal fornitore di pagamento.