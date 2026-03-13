---
tipo-artefatto: template
documento: commento
descrizione: struttura canonica di un commento in una questione o in una nota
fase: trasversale
autorita: operativa
---

# Template — Commento

Un commento e' un'annotazione additiva e immutabile che si aggiunge a una
questione o a una nota per rettificare, integrare o documentare un'evoluzione
senza modificare il corpo originale.

## Struttura

```markdown
**Commenti**

COMMENTO-{NNN} — {YYYY-MM-DD}
{testo del commento}
```

## Prima di scrivere

Non scrivere il commento senza conferma dell'operatore. Proponi il contenuto
e il contenitore di destinazione (quale questione o nota) e attendi
approvazione esplicita.

## Regole

- La numerazione (COMMENTO-NNN) e' locale al contenitore (questione o nota).
- Il primo commento e' COMMENTO-001. Leggere i commenti esistenti per determinare il prossimo numero.
- Il commento e' immutabile dopo la scrittura: non modificarlo mai.
- Il commento e' additivo: si aggiunge in fondo alla sezione Commenti.
- La sezione **Commenti** si trova in fondo al contenitore, prima del separatore `---` finale. Se non esiste, crearla in quella posizione.
- In una questione, la sezione Commenti segue tutti i campi strutturati (Descrizione, Domande aperte, Impatto, Questioni collegate).
- Per rettificare un commento precedente, aggiungere un nuovo commento che lo riferisce esplicitamente (es. "Rettifica del COMMENTO-002").
