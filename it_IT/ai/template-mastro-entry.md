---
tipo-artefatto: template
documento: mastro-entry
descrizione: struttura canonica di un'entry nel mastro.md, scritta alla chiusura di una questione
fase: trasversale
---

# Template — Entry Mastro

Un'entry nel mastro documenta la chiusura di una questione. Va inserita in cima
a `mastro.md` (prepend-only). Il mastro e' immutabile: le entry non vengono mai
modificate dopo la scrittura.

## Struttura

```markdown
## {YYYY-MM-DD} — Chiusura {QUESTIONE-ID}: {Titolo}

**Questione**: {QUESTIONE-ID} — {Titolo}

**Percorso** (opzionale — ometti se la decisione e' stata diretta)

{sintesi del percorso: aperta per X, bloccata per Y, reindirizzata per Z}

**Decisioni prese**

- {decisione con motivazione}

**Impatto**

- `{artefatto}` — {descrizione della modifica applicata}

---
```

## Sezione Percorso

Includere il Percorso quando il ciclo ha avuto qualsiasi complessita': stati
multipli, ripensamenti, alternative esplorate, blocchi. Il bias corretto e'
includere il Percorso. L'omissione e' giustificata solo quando la decisione
e' stata diretta (apertura e chiusura senza stati intermedi significativi).

## Regole

- L'entry va scritta nel mastro prima di rimuovere la questione da questioni.md.
- Il mastro e' prepend-only: ogni nuova entry va inserita in cima al file.
- Le entry sono immutabili: non modificarle mai dopo la scrittura.
- Decisioni prese e Impatto sono obbligatori.
- Il Percorso e' opzionale ma il bias e' includerlo.
