Chiudi un issue: rimuovilo da issues.md e registra la risoluzione in log.md.

## 1. Trova i file

Cerca `issues.md` e `log.md` nella directory corrente e nelle sottodirectory
immediate. Se uno dei due non esiste, interrompi e avvisa l'utente.

## 2. Identifica l'issue da chiudere

Se il messaggio specifica un ID (es. ISSUE-003) o un titolo, individua l'issue
direttamente.

Altrimenti, mostra la lista degli issue nell'indice tramite AskUserQuestion.

## 3. Raccogli le informazioni per il log

Se non presenti nel contesto, chiedi:

- **Decisioni prese**: cosa e' stato risolto e perche' (una o piu' voci)
- **Impatto**: quali artefatti sono stati modificati o lo saranno

## 4. Scrivi l'entry in log.md

Inserisci in cima al file (prepend) la nuova entry:

```markdown
## {YYYY-MM-DD} — Chiusura {ISSUE-ID}: {Titolo}

**Issue**: {ISSUE-ID} — {Titolo}

**Decisioni prese**

- {decisione con motivazione}

**Impatto**

- `{artefatto}` — {descrizione della modifica applicata}

---
```

## 5. Rimuovi l'issue da issues.md

- Rimuovi l'intero blocco dell'issue (dal titolo `## ISSUE-{ID}` fino al `---` finale)
- Rimuovi la riga corrispondente dalla tabella dell'indice
- Aggiorna la nota:

```
> Ultimo issue chiuso: ISSUE-{ID} — {YYYY-MM-DD}.
```

## Regole

- L'entry nel log e' immutabile dopo la scrittura: non modificarla mai
- Rimuovi l'issue da issues.md solo dopo aver scritto con successo l'entry nel log
- Se l'issue ha domande ancora aperte, avvisa l'utente prima di procedere
