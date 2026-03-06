Aggiungi una entry al mastro.md per documentare una decisione o un ciclo chiuso.

Questa skill e' per entry manuali. Per chiudere una questione usa /chiudi-questione,
che scrive nel mastro automaticamente.

## 1. Trova mastro.md

Cerca `mastro.md` nella directory corrente e nelle sottodirectory immediate.
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

- Il mastro contiene solo cicli chiusi: non usare questa skill per decisioni
  ancora in discussione o soggette a revisione
- Una entry nel mastro non viene mai modificata dopo la scrittura
- Se la decisione riguarda la chiusura di una questione, usa /chiudi-questione
  invece di questa skill
