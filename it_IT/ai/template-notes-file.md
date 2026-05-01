---
tipo-artefatto: template
documento: notes-file
descrizione: struttura canonica del file notes.md vuoto per un'opera Hodos
fase: trasversale
autorita: operativa
---

# Template — File notes.md

Il file `notes.md` raccoglie note e memo informali dell'opera. Viene creato
durante l'inizializzazione e vive nella directory di processo. È opzionale:
non tutte le opere lo usano.

## Struttura

```markdown
# Note — {Nome Opera}

## Indice

- **NOTA-{ID}** — {Descrizione} — {YYYY-MM-DD}

> Ultima nota inserita: —
```

## Regole

- L'indice è un elenco puntato con tre campi: ID in grassetto,
  descrizione, data. Non aggiungere campi extra.
- Le note vengono inserite in cima al file, dopo la sezione Indice e
  il separatore.
- L'indice viene aggiornato ad ogni inserimento.
- Per la struttura di una singola nota, consultare il template `nota`.
