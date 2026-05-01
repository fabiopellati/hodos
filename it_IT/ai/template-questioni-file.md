---
tipo-artefatto: template
documento: questioni-file
descrizione: struttura canonica del file questioni.md vuoto per un'opera Hodos
fase: trasversale
autorita: operativa
---

# Template — File questioni.md

Il file `questioni.md` è lo strumento di governo delle questioni aperte di
un'opera Hodos. Viene creato durante l'inizializzazione dell'opera e vive
nella directory di processo.

## Struttura

```markdown
# Questioni — {Nome Opera}

## Indice

- **QUESTIONE-{ID}** — {Titolo} — {stato}

> Ultima questione inserita: —
> Ultima questione chiusa: —
```

## Regole

- L'indice è un elenco puntato con tre campi: ID in grassetto, titolo,
  stato. Non aggiungere campi extra.
- Le questioni vengono inserite in cima al file, dopo la sezione Indice
  e il separatore `---`.
- L'indice viene aggiornato coerentemente ad ogni apertura, cambio di
  stato e chiusura.
- Per la struttura di una singola questione, consultare il template
  `questione`.
