---
tipo-artefatto: template
documento: notes-file
descrizione: struttura canonica dell'indice note.md, proiezione derivata della cartella note/
fase: trasversale
autorita: operativa
---

# Template — Indice note.md

Il file `note.md` è l'**indice** delle note dell'opera: una proiezione
derivata dei frontmatter dei file presenti nella cartella `note/`.
La sorgente è il singolo file `note/NOTA-{NNN}-slug.md`; l'indice ne offre il
sommario ed è rigenerato dallo strumento dell'opera.
Le note sono opzionali: non tutte le opere le usano.

## Struttura

```markdown
# Note — {Nome Opera}

<!-- FILE GENERATO — proiezione derivata dei frontmatter in note/.
     Non modificare a mano: rigenerare con lo strumento dell'opera. -->

## Indice

- **NOTA-{ID}** — {Descrizione} — {YYYY-MM-DD}

> Ultima nota inserita: —
```

## Regole

- L'indice è un elenco puntato con tre campi derivati dal frontmatter di
  ciascuna nota: ID in grassetto (`id`), titolo/descrizione (`titolo`), data
  (`data`). Non aggiungere campi extra.
- Le voci sono ordinate in senso decrescente per data.
- L'indice non si modifica a mano: si rigenera dai frontmatter ad ogni
  inserimento.
- Per la struttura di una singola nota, consultare il template `nota`.
