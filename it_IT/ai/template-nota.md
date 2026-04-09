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

## Prima di scrivere

Non scrivere la nota senza conferma dell'operatore.

1. Leggi questioni.md per verificare se esistono questioni aperte sullo
   stesso tema o su un tema correlato al prompt dell'operatore.
2. Se esiste una questione correlata, usa il tool AskUserQuestion per
   proporre le opzioni all'operatore:
   - aggiungere un commento alla questione esistente (indicare quale)
   - creare una nota separata
   - non operare
3. Se non esiste una questione correlata, proponi il contenuto della nota
   e attendi approvazione.
4. Non scrivere nulla finché l'operatore non ha scelto.

Usare il tool AskUserQuestion ogni volta che le opzioni sono più di una.
Non proporre opzioni in testo libero.

## Regole

- Il formato è leggero: nessuna sezione strutturata, nessuno stato.
- La descrizione sintetica è quella che appare nell'indice: deve essere comprensibile senza leggere il corpo.
- Il corpo di una nota è immutabile dopo la scrittura.
- Per rettifiche o nuove conoscenze sullo stesso argomento, aggiungere un commento (COMMENTO-NNN) alla nota esistente invece di aprirne una nuova.
- I commenti sono additivi e immutabili.
