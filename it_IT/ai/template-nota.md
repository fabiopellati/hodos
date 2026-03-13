---
tipo-artefatto: template
documento: nota
descrizione: struttura canonica di una nota in notes.md
fase: trasversale
---

# Template — Nota

Una nota registra un memo, un'osservazione o una decisione informale nel file
`notes.md`. Va inserita in cima al file, prima delle note esistenti.

## Struttura

```markdown
## NOTA-{ID} — {YYYY-MM-DD} — {Descrizione sintetica}

{corpo della nota}

```

## Commento a una nota esistente

Per rettificare o integrare una nota senza modificarne il corpo:

```markdown
**Commenti**

COMMENTO-{NNN} — {YYYY-MM-DD}
{testo del commento}
```

## Aggiornamento indice

Aggiungere in cima alla tabella:

```markdown
| NOTA-{ID} | {Descrizione sintetica} | {YYYY-MM-DD} |
```

Aggiornare la nota a fondo file:

```
> Ultima nota inserita: NOTA-{ID} — {YYYY-MM-DD}.
```

## Regole

- Il formato e' leggero: nessuna sezione strutturata, nessuno stato.
- La descrizione sintetica e' quella che appare nell'indice: deve essere comprensibile senza leggere il corpo.
- Il corpo di una nota e' immutabile dopo la scrittura.
- Per rettifiche o nuove conoscenze sullo stesso argomento, aggiungere un commento (COMMENTO-NNN) alla nota esistente invece di aprirne una nuova.
- I commenti sono additivi e immutabili.
