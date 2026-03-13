---
tipo-artefatto: template
documento: questioni-file
descrizione: struttura canonica del file questioni.md vuoto per un'opera Hodos
fase: trasversale
autorita: operativa
---

# Template — File questioni.md

Il file `questioni.md` e' lo strumento di governo delle questioni aperte di
un'opera Hodos. Viene creato durante l'inizializzazione dell'opera e vive
nella directory di processo.

## Struttura

```markdown
# Questioni — {Nome Opera}

## Indice

| ID | Titolo | Stato |
|---|---|---|

> Ultima questione inserita: —
> Ultima questione chiusa: —
```

## Regole

- L'indice contiene tre colonne: ID, Titolo, Stato. Non aggiungere colonne extra.
- Le questioni vengono inserite in cima al file, dopo la sezione Indice e il separatore `---`.
- L'indice viene aggiornato coerentemente ad ogni apertura, cambio di stato e chiusura.
- Per la struttura di una singola questione, consultare il template `questione`.
