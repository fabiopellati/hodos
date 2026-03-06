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

## Regole

- Il formato e' leggero: nessuna sezione strutturata, nessuno stato
- La descrizione sintetica e' quella che appare nell'indice: deve essere
  comprensibile senza leggere il corpo
- Le note non hanno ciclo di vita: non cambiare mai il contenuto di una
  nota esistente; se serve un aggiornamento, apri una nuova nota
