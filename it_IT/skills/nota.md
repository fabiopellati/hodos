---
skill: nota
client: Claude Code CLI
invocazione: /hodos-nota
tipo: operativo
locale: it_IT
---

Aggiungi una nuova nota nel file notes.md del progetto corrente.

## 1. Trova notes.md

Cerca `notes.md` nella directory corrente e nelle sottodirectory immediate.

Se non esiste, crealo con questa struttura minima:

```markdown
# Note — [nome progetto]

---

## Indice

| ID | Descrizione | Data |
|---|---|---|

> Ultima nota inserita: —
```

## 2. Determina l'ID

Leggi il file per identificare tutti gli ID esistenti (formato `NOTA-NNN`).
Assegna il prossimo ID disponibile. Ogni ID deve essere univoco.

## 3. Determina il contenuto

Se il messaggio non fornisce il contenuto della nota, chiedi:

- **Descrizione sintetica**: una riga, usata nell'indice
- **Corpo**: testo libero della nota

## 4. Scrivi la nota

Inserisci la nuova nota in cima al file, prima delle note esistenti:

```markdown
## NOTA-{ID} — {YYYY-MM-DD} — {Descrizione sintetica}

{corpo della nota}

```

## 5. Aggiorna l'indice

Aggiungi una riga in cima alla tabella:

```markdown
| NOTA-{ID} | {Descrizione sintetica} | {YYYY-MM-DD} |
```

Aggiorna la nota a fondo file:

```
> Ultima nota inserita: NOTA-{ID} — {YYYY-MM-DD}.
```

## Aggiungere un commento a una nota esistente

Quando occorre rettificare, integrare o contestualizzare una nota senza
modificarne il corpo, aggiungere un commento alla nota esistente.

1. Individua la nota in `notes.md` per ID o titolo.
2. Determina il prossimo numero di commento locale alla nota
   (COMMENTO-001 se e' il primo, altrimenti il successivo disponibile).
3. Aggiungi in fondo alla nota, prima del separatore `---`, la sezione
   `**Commenti**` se non esiste, poi il commento:

```markdown
**Commenti**

COMMENTO-{NNN} — {YYYY-MM-DD}
{testo del commento}
```

4. Non modificare il corpo della nota ne' l'indice.

## Regole

- Il formato e' leggero: nessuna sezione strutturata, nessuno stato
- La descrizione sintetica e' quella che appare nell'indice: deve essere
  comprensibile senza leggere il corpo
- Il corpo di una nota e' immutabile dopo la scrittura
- Per rettifiche o nuove conoscenze sullo stesso argomento, aggiungere un
  commento (COMMENTO-NNN) alla nota esistente invece di aprirne una nuova
- I commenti sono additivi e immutabili: non modificare un commento esistente
