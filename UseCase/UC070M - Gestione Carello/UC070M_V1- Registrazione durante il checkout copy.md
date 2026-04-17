# UC-070_V1: LOGIN DURANTE CHECKOUT
---
**Attori coinvolti**:
---
A1: Utente Visitatore (Ospite)

**Descrizione:**
---
L'Utente Visitatore decide di aggiungere un prodotto al carrello, ma non è autenticato, quindi il sistema glelo suggerisce.

**Precondizioni:**
---

L'utente ha cliccato su "Procedi al Checkout".

L'utente non è autenticato.

**Flusso Principale degli Eventi:**
---
Il sistema presenta una schermata di checkout con un'opzione facoltativa "Accedi o crea un acccount e completa l'acquisto".

Vedere UC020M

**Postcondizioni:**
---
Reindirizzato alla pagina di login

**Varianti / Estensioni:**
---

**Eccezioni / Flussi alternativi:**
---

**Note:**
---
Nice to have: Se l'utente aveva prodotti nel carrello da ospite e scopre di avere già un account, al login i prodotti del carrello "ospite" devono essere aggiunti a quelli eventualmente già presenti nel carrello "utente".