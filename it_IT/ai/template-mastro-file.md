---
tipo-artefatto: template
documento: mastro-file
descrizione: struttura canonica dell'indice mastro.md, proiezione derivata della cartella mastro/
fase: trasversale
autorita: operativa
---

# Template — Indice mastro.md

Il file `mastro.md` è l'**indice** del registro delle decisioni prese: una
proiezione derivata dei frontmatter dei file presenti nella cartella
`mastro/`.
La sorgente è il singolo file `mastro/Q{NNN}-slug.md`; l'indice ne offre il
sommario cronologico decrescente ed è rigenerato dallo strumento dell'opera.

## Struttura

```markdown
# Mastro — {Nome Opera}

<!-- FILE GENERATO — proiezione derivata dei frontmatter in mastro/.
     Non modificare a mano: rigenerare con lo strumento dell'opera. -->

## Indice

- **{QUESTIONE-ID}** — {Titolo} — chiusa {YYYY-MM-DD}
```

## Regole

- L'indice è un elenco puntato derivato dal frontmatter di ciascuna voce:
  ID (`id`), titolo (`titolo`), data di chiusura (`chiusa`).
- Le voci sono ordinate in senso cronologico decrescente per data di
  chiusura.
- L'indice non si modifica a mano: si rigenera dai frontmatter ad ogni
  chiusura di questione.
- Per la struttura di una singola voce, consultare il template `mastro-entry`.
