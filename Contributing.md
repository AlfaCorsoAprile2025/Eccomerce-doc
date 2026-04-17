# Guida al Contributo

Siamo felici che tu voglia contribuire alla documentazione del progetto! Per mantenere la documentazione chiara, coerente e aggiornata, ti chiediamo di seguire le linee guida descritte di seguito.

## Flusso di lavoro (Workflow)

Seguiamo un approccio basato sui branch per garantire l'integrità dei documenti:

1. **Fork della repository**: Crea una copia del progetto sul tuo account.
2. **Crea un branch**: Lavora su un branch dedicato (es: `feat/documentazione-checkout` o `fix/api-user-endpoint`).
3. **Apporta le modifiche**: Segui gli standard di formattazione descritti sotto.
4. **Apri una Pull Request (PR)**: Descrivi chiaramente le modifiche apportate e cita il ticket di riferimento (se presente).

## Standard di Documentazione

### 1. Casi d'Uso e UML
* Utilizza Draw.io per i diagrammi UML.
* Mantieni le descrizioni testuali concise.

### 2. Architettura C4
* Assicurati che ogni modifica all'architettura sia riflessa nei diagrammi C4 corrispondenti.

### 3. OpenAPI
* Le modifiche agli endpoint devono essere validate tramite uno strumento di linting OpenAPI.
* Assicurati che ogni endpoint abbia una breve descrizione, i parametri di input e i possibili codici di risposta (200, 400, 404, 500).

## Best Practices
* **Revisione**: Ogni PR deve essere rivista da almeno un altro membro del team prima di essere mergiata nel branch `main`.
* **Coerenza**: Usa lo stile e la terminologia adottata nei documenti esistenti.
* **Aggiornamento**: Se modifichi il codice, ricordati di aggiornare la documentazione correlata!
