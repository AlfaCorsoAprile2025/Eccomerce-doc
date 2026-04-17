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

4 - Il sistema aggiorna la vista mostrando solo i prodotti che corrispondono ai criteri inseriti.

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
E1: Nessun risultato trovato: Se la ricerca o i filtri non producono corrispondenze, il sistema mostra un messaggio "Nessun prodotto trovato" e suggerisce di modificare i criteri o mostra prodotti alternativi.

E2: Errore di connessione: Se il sistema non riesce a recuperare i dati dal database, mostra un messaggio di errore tecnico e invita a ricaricare la pagina.

**Note:**
---

Regola di Business: I prodotti "Esauriti" possono essere mostrati o nascosti 