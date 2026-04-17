# UC-01: REGISTRAZIONE NUOVO UTENTE
---
**Attori coinvolti:**
---
A1: Utente Visitatore (Ospite)

**Descrizione:**
---
L'Utente Visitatore desidera creare un profilo personale sulla piattaforma ecommerce per poter procedere agli acquisti, salvare i propri dati di spedizione e visualizzare lo storico degli ordini. Il sistema deve validare i dati e creare un'identità digitale univoca.

**Precondizioni:**
---
L'utente deve aver effettuato l'accesso alla pagina di registrazione.

L'utente non deve essere già autenticato nel sistema.

**Flusso Principale degli Eventi:**
---
1 - L'utente compila il modulo di registrazione inserendo Nome, Cognome, Email, Password e conferma della Password.

2 - L'utente accetta i termini di servizio e l'informativa sulla privacy.

3 - L'utente invia i dati cliccando sul pulsante "Registrati".

4 - Il sistema verifica che l'email non sia già presente nel database.

5 - Il sistema valida la robustezza della password e la corrispondenza dei campi.

6 - Il sistema crea un nuovo record utente con stato "In attesa di verifica".

7 - Il sistema invia una comunicazione (A2) all'email fornita contenente un link di attivazione.

8 - Il sistema mostra un messaggio di conferma all'utente invitandolo a controllare la posta.

**Postcondizioni:**
---
Il profilo utente è creato nel database.

Viene generato un log dell'evento di registrazione.

L'utente non può ancora effettuare il login finché non completa la verifica (se previsto dal business).

**Varianti / Estensioni:**
---
V1: Registrazione durante il Checkout: L'utente aggiunge prodotti al carrello e decide di registrarsi solo al momento del pagamento. I dati del carrello devono essere mantenuti e associati al nuovo profilo.

**Eccezioni / Flussi alternativi:**
---
E1: Email già esistente: Se l'email inserita è già associata a un account, il sistema nega la creazione e suggerisce di effettuare il login o il recupero password.

E2: Password non conforme: Se la password non rispetta i criteri di sicurezza (es. lunghezza minima, caratteri speciali), il sistema evidenzia l'errore e richiede una nuova inserimento.

E3: Mancata accettazione Privacy: Se le checkbox obbligatorie non sono selezionate, il pulsante di invio rimane disabilitato o restituisce un errore bloccante.

**Note:**
---
La password deve essere salvata nel database esclusivamente in forma cifrata (hashing con salt).

Regola di Business: Il link di attivazione inviato via email scade dopo 24 ore.