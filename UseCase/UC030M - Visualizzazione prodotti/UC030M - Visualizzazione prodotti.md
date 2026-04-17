# UC-03: VISUALIZZAZIONE PRODOTTI, RICERCA E FILTRI
---
**Attori coinvolti:**
---
A1: Utente (Ospite o Registrato)

**Descrizione:**
---
L'utente desidera esplorare il catalogo dei prodotti per trovare articoli di suo interesse. Il sistema deve permettere la navigazione tra le categorie, la ricerca testuale libera e l'affinamento dei risultati tramite parametri specifici (filtri), garantendo un'esperienza di reperimento delle informazioni rapida ed efficace.

**Precondizioni:**
---
Il sistema deve avere dei prodotti caricati nel database e pubblicati.

L'utente deve essere connesso alla piattaforma (Home Page o pagina Catalogo).

**Flusso Principale degli Eventi:**
---
1 - L'utente accede alla sezione "Negozio" o "Catalogo".

2 - Il sistema mostra una lista predefinita di prodotti (es. gli ultimi arrivi o i più popolari).

3 - L'utente inserisce una parola chiave nella barra di ricerca e/o seleziona una categoria merceologica.

4 - Il sistema aggiorna la vista mostrando solo i prodotti che corrispondono ai criteri inseriti e che non sono nascosti.

5 - L'utente applica uno o più filtri (es. fascia di prezzo, marca, taglia, colore, disponibilità).

6 - Il sistema filtra dinamicamente i risultati in base alle selezioni effettuate.

7 - L'utente seleziona un criterio di ordinamento (es. "Prezzo: dal più basso", "Novità", "Voto Recensioni").

8 - Il sistema visualizza l'elenco finale dei prodotti con anteprima (immagine, nome, prezzo).

**Postcondizioni:**
---
Il sistema visualizza una lista di prodotti filtrata e ordinata secondo le preferenze dell'utente.

L'utente può cliccare su un prodotto specifico per accedere al UC "Visualizzazione Dettaglio Prodotto".

**Varianti / Estensioni:**
---
V1: Filtri Dinamici: I filtri cambiano in base alla categoria scelta 

**Eccezioni / Flussi alternativi:**
---
### E1 Nessun risultato trovato:

    L'eccezione si verifica ai punti 4 o 6 del flusso principale, a seguito di una ricerca o dell'applicazione di filtri troppo restrittivi.

    3/5 - L'utente inserisce una parola chiave o applica dei filtri.

    E1.1 Il sistema interroga il database e rileva che non esistono prodotti corrispondenti ai criteri inseriti.

    E1.2 Il sistema visualizza un messaggio di avviso ("Nessun prodotto trovato per i criteri selezionati").

    E1.3 Il sistema mostra un pulsante "Resetta filtri" o suggerisce prodotti simili/popolari per non interrompere la navigazione.

    Il flusso torna al punto 3 o 5 del flusso principale.

### E2 Errore di connessione / Timeout Database:
    L'eccezione può verificarsi in qualsiasi punto in cui il sistema deve recuperare dati (punti 2, 4, 6).

    1/3/5 - L'utente tenta di accedere al catalogo o aggiornare la vista.

    E2.1 Il sistema rileva un'interruzione della connessione con il database o un tempo di risposta superiore al limite (timeout).

    E2.2 Il sistema visualizza un messaggio di errore tecnico ("Spiacenti, si è verificato un errore nel caricamento dei prodotti. Riprova tra poco").

    E2.3 Il sistema fornisce un pulsante "Ricarica pagina".

    Il caso d'uso termina con insuccesso o torna al punto iniziale dopo il refresh.

### E3 Stringa di ricerca non valida:
    L'eccezione si verifica al punto 3 del flusso principale.

    3 - L'utente inserisce una stringa composta solo da caratteri speciali o troppo breve (es. meno di 2 caratteri).

    E3.1 Il sistema rileva che la stringa non è idonea per una ricerca efficace.

    E3.2 Il sistema non avvia la query e visualizza un suggerimento sotto la barra di ricerca ("Inserisci almeno 2 caratteri per la ricerca").

    Il flusso torna al punto 3 del flusso principale.

**Note:**
---
