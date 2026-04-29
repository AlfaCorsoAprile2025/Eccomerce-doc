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
L'utente è sulla pagina di registrazione.

L'utente non deve essere già autenticato 

**Flusso Principale degli Eventi:**
---
1 - Il sistema mostra un form con campi nome, cognome, email, password, conferma della stessa e un flag con il link ai termini di servizio

2 - L'utente compila il modulo di registrazione inserendo Nome, Cognome, Email, Password e conferma della Password.

3 - Il sistema effettua una prima validazione dei dati 

4 - L'utente accetta i termini di servizio e l'informativa sulla privacy.

5 - L'utente invia i dati cliccando sul pulsante "Registrati".

6 - Il sistema verifica che la mail non sia già presente nel database.

7 - Il sistema valida la robustezza della password 

8 - Il sistema crea un nuovo record utente con stato "In attesa di verifica".

9 - Il sistema invia un otp alla mail indicata

10 - il sistema visualizza un form in cui inserire l'otp invitandolo a controllare la posta

11 - L'utente isnerisce otp

12 - Il sistema aggiorna lo stato utente a "Verificato"

13 - Il sistema reindirizza alla pagina catalogo; vedere UC030M

**Postcondizioni:**
---
Il profilo utente è creato nel database.

Viene generato un log dell'evento di registrazione.

L'utente non può ancora effettuare il login finché non completa la verifica (se previsto dal business).

**Varianti / Estensioni:**
---
V1: Registrazione durante il Checkout: vedere UC084M

**Eccezioni / Flussi alternativi:**
---
### E1 Email già esistente:
    L'eccezione si verifica al punto 4 del flusso principale.

    5 - L'utente invia i dati cliccando sul pulsante "Registrati".

    E1.1 Il sistema rileva che l'email inserita è già presente nel database.

    E1.2 Il sistema blocca la creazione del record.

    E1.3 Il sistema visualizza un messaggio di errore (es: "Email già in uso") e suggerisce il recupero password o il login.

    Il flusso torna al punto 1 del flusso principale.

### E2 Password non conforme:
    L'eccezione si verifica al punto 5 del flusso principale.

    4 - L'utente invia i dati cliccando sul pulsante "Registrati".

    E2.1 Il sistema rileva che la password non soddisfa i requisiti di sicurezza (es. troppo corta o manca di caratteri speciali).

    E2.2 Il sistema evidenzia il campo password con un messaggio di errore specifico sui criteri mancanti.

    Il flusso torna al punto 1 del flusso principale (mantenendo gli altri dati già inseriti).

### E3 Mancata accettazione Privacy:
    L'eccezione si verifica tra il punto 2 e il punto 3 del flusso principale.

    2 - L'utente omette di selezionare le checkbox obbligatorie per i Termini e la Privacy.

    E3.1 L'utente tenta di cliccare sul pulsante "Registrati".

    E3.2 Il sistema mantiene il pulsante disabilitato OPPURE interrompe l'invio mostrando un messaggio di avviso ("È necessario accettare l'informativa sulla privacy per proseguire").

    Il flusso torna al punto 2 del flusso principale.

### E4 Password e Conferma Password non coincidenti:
    L'eccezione si verifica durante la validazione dei dati al punto 3/4.

    4 - L'utente invia i dati cliccando sul pulsante "Registrati".

    E4.1 Il sistema confronta i campi "Password" e "Conferma Password" rilevando una discrepanza.

    E4.2 Il sistema visualizza un messaggio di errore ("Le password non coincidono").

    Il flusso torna al punto 1 del flusso principale.

### E5 OTP errato:
    L'eccezione si verifica al punto 12 del flusso principale, a seguito dell'inserimento del codice da parte dell'utente.

    11 - L'utente inserisce l'OTP nel form di verifica.

    E5.1 - Il sistema riceve il codice e lo confronta con quello generato al punto 9.

    E5.2 - Il sistema rileva che il codice inserito non coincide con quello inviato (errore di battitura o codice non valido).

    E5.3 - Il sistema visualizza un messaggio di errore ("Codice OTP non corretto. Riprova").

    E5.4 - Il sistema incrementa un contatore di tentativi falliti; se superato un limite (es. 3 o 5 tentativi), il sistema inibisce temporaneamente l'inserimento o rigenera un nuovo codice.

    Il flusso torna al punto 10 del flusso principale.

### E6 Tempo scaduto per la verifica (Timeout OTP/Record):
    L'eccezione si verifica al punto 11 o in fase di pulizia automatica del sistema (cron job), basandosi sulla scadenza delle 24 ore citata nelle note.

    11 - L'utente tenta di inserire l'OTP dopo che è trascorso il tempo limite dalla generazione.

    E6.1 - Il sistema verifica il timestamp di creazione del record utente (punto 8) o del codice OTP.

    E6.2 - Il sistema rileva che sono trascorse più di 24 ore (timeout di sicurezza).

    E6.3 - Il sistema invalida il codice e cancella automaticamente il record utente con stato "In attesa di verifica" dal database per liberare l'email.

    E6.4 - Il sistema visualizza un messaggio di errore ("Il tempo per la verifica è scaduto. La tua registrazione è stata annullata, ripeti la procedura").

    Il caso d'uso termina con insuccesso e l'utente viene reindirizzato al punto 1 del flusso principale.

### E7 Mancato arrivo della mail (Richiesta nuovo OTP):
    L'eccezione si verifica al punto 10, su iniziativa dell'utente.

    10 - L'utente visualizza il form ma dichiara di non aver ricevuto la mail.

    E7.1 - L'utente clicca su un link "Non hai ricevuto il codice? Inviamene un altro".

    E7.2 - Il sistema verifica che non sia passato troppo poco tempo dall'ultimo invio (antispam/flooding).

    E7.3 - Il sistema genera un nuovo codice OTP e invalida il precedente.

    Il flusso torna al punto 9 del flusso principale.

**Note:**
---
La password deve essere salvata nel database esclusivamente in forma hashing con salt.

**Dipendenze funzionali**

Dipende da Authentication-Service,Api-Gateway, Storage e Mail-service

