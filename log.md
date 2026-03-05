Aggiungi una entry al log.md per documentare una decisione o un ciclo chiuso.

Questa skill e' per entry manuali. Per chiudere un issue usa /issue-close,
che scrive nel log automaticamente.

## 1. Trova log.md

Cerca `log.md` nella directory corrente e nelle sottodirectory immediate.
Se non esiste, chiedi all'utente dove crearlo prima di procedere.

## 2. Raccogli le informazioni

Se non presenti nel contesto del messaggio, chiedi:

- **Titolo**: cosa viene documentato (es. "Decisione architetturale su X")
- **Decisioni prese**: le scelte fatte con motivazione
- **Impatto**: artefatti modificati o da modificare (opzionale)

## 3. Scrivi l'entry in cima al file (prepend)

```markdown
## {YYYY-MM-DD} — {Titolo}

**Decisioni prese**

- {decisione con motivazione}

**Impatto**

- `{artefatto}` — {descrizione}

---
```

Ometti la sezione **Impatto** se non ci sono artefatti coinvolti.

## Regole

- Il log contiene solo cicli chiusi: non usare questa skill per decisioni
  ancora in discussione o soggette a revisione
- Una entry nel log non viene mai modificata dopo la scrittura
- Se la decisione riguarda la chiusura di un issue, usa /issue-close
  invece di questa skill
