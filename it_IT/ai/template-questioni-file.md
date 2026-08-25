---
tipo-artefatto: template
documento: questioni-file
descrizione: struttura canonica dell'indice questioni.md, proiezione derivata della cartella questioni/
fase: trasversale
autorita: operativa
---

# Template — Indice questioni.md

Il file `questioni.md` è l'**indice** delle questioni di un'opera Hodos: una proiezione derivata dei frontmatter dei file presenti nella cartella `questioni/`.
La proiezione è integrale, come dispone l'Art. 7 comma 3 del protocollo, che vi fa riportare identificativo, titolo e stato corrente di ogni questione presente nella collezione.
Le questioni chiuse non vi compaiono perché l'Art. 7 comma 1 le rimuove dalla collezione spostandole in `mastro/`, e non perché l'indice filtri sullo stato: il campo `stato` della voce serve appunto a distinguere gli stati che nella collezione convivono, da `open` a `in-progress`, `pending-approval` e `deferred`.
Non è la sorgente delle questioni — la sorgente è il singolo file `questioni/Q{NNN}-slug.md` — ma un sommario committato per comodità di lettura e navigazione, rigenerato dallo strumento dell'opera.

## Struttura

```markdown
# Questioni — {Nome Opera}

<!-- FILE GENERATO — proiezione derivata dei frontmatter in questioni/.
     Non modificare a mano: rigenerare con lo strumento dell'opera. -->

## Indice

- **QUESTIONE-{ID}** — {Titolo} — {stato}

> Ultima questione inserita: —
> Ultima questione chiusa: —
```

## Regole

- L'indice è un elenco puntato con tre campi, derivati dal frontmatter di
  ciascuna questione: ID in grassetto (`id`), titolo (`titolo`), stato
  (`stato`). Non aggiungere campi extra.
- Le questioni sono ordinate in senso decrescente per identificativo:
  l'ordinamento è una proprietà dell'indice, non dei file.
- L'indice non si modifica a mano: si rigenera dai frontmatter ad ogni
  apertura, cambio di stato e chiusura.
- Per la struttura di una singola questione, consultare il template
  `questione`.
