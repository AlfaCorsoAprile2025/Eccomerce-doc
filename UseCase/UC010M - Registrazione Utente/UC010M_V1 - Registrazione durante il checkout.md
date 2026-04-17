# UC-010_V1: REGISTRAZIONE DURANTE CHECKOUT

**Attori coinvolti**:

A1: Utente Visitatore (Ospite)

**Descrizione:**

L'Utente Visitatore, dopo aver aggiunto prodotti al carrello, decide di procedere all'acquisto. Invece di autenticarsi, sceglie di creare un account contestualmente all'inserimento dei dati di spedizione e pagamento, per non interrompere il flusso d'ordine.

**Precondizioni:**

L'utente ha almeno un prodotto nel carrello.

L'utente ha cliccato su "Procedi al Checkout".

L'utente non è autenticato.

**Flusso Principale degli Eventi:**

Il sistema presenta una schermata di checkout con un'opzione facoltativa "Crea un acccount e completa l'acquisto".

L'utente inserisce nickname, password, comnferma password e mail per il nuovo profilo.

L'utente accetta i termini di servizio e la privacy.

Il sistema valida i dati 

L'account viene creato a sistema

All'account viene associato il carrello precedentemente riempito

Il sistema reindirizza l'utente alla pagina di checkout

**Postcondizioni:**

Il carrello contiene gli oggetti inseriti

Il profilo utente è creato 

L'utente è loggato

**Varianti / Estensioni:**


**Eccezioni / Flussi alternativi:**

E1: Email già registrata: Il sistema avvisa che esiste già un account e chiede all'utente se desidera unire l'acquisto corrente al profilo esistente tramite login.

**Note:**

Nice to have: Se l'utente aveva prodotti nel carrello da ospite e scopre di avere già un account, al login i prodotti del carrello "ospite" devono essere aggiunti a quelli eventualmente già presenti nel carrello "utente".