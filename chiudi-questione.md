Chiudi una questione: rimuovila da questioni.md e registra la risoluzione in mastro.md.

## 1. Trova i file

Cerca `questioni.md` e `mastro.md` nella directory corrente e nelle sottodirectory
immediate. Se uno dei due non esiste, interrompi e avvisa l'utente.

## 2. Identifica la questione da chiudere

Se il messaggio specifica un ID (es. QUESTIONE-003) o un titolo, individua la
questione direttamente.

Altrimenti, mostra la lista delle questioni nell'indice tramite AskUserQuestion.

## 3. Raccogli le informazioni per il mastro

Se non presenti nel contesto, chiedi:

- **Decisioni prese**: cosa e' stato risolto e perche' (una o piu' voci)
- **Impatto**: quali artefatti sono stati modificati o lo saranno

## 4. Scrivi l'entry in mastro.md

Inserisci in cima al file (prepend) la nuova entry:

```markdown
## {YYYY-MM-DD} — Chiusura {QUESTIONE-ID}: {Titolo}

**Questione**: {QUESTIONE-ID} — {Titolo}

**Decisioni prese**

- {decisione con motivazione}

**Impatto**

- `{artefatto}` — {descrizione della modifica applicata}

---
```

## 5. Rimuovi la questione da questioni.md

- Rimuovi l'intero blocco della questione (dal titolo `## QUESTIONE-{ID}` fino al `---` finale)
- Rimuovi la riga corrispondente dalla tabella dell'indice
- Aggiorna la nota:

```
> Ultima questione chiusa: QUESTIONE-{ID} — {YYYY-MM-DD}.
```

## Regole

- L'entry nel mastro e' immutabile dopo la scrittura: non modificarla mai
- Rimuovi la questione da questioni.md solo dopo aver scritto con successo l'entry nel mastro
- Se la questione ha domande ancora aperte, avvisa l'utente prima di procedere
