Apri un nuovo issue nel file issues.md del progetto corrente.

## 1. Trova issues.md

Cerca `issues.md` nella directory corrente e nelle sottodirectory immediate
(es. `docs/`, `process/`).

Se non esiste, chiedi all'utente dove crearlo prima di procedere.

## 2. Determina i parametri

Se il contesto del messaggio non fornisce tutte le informazioni necessarie,
usa AskUserQuestion per raccogliere:

- **Tipo**: `finding` (conoscenza nuova emersa) o `revision` (correzione artefatto esistente)
- **Titolo**: breve e descrittivo
- **Fase**: fase di appartenenza (es. P0, P1, P2, step 1, step 3...)
- **Descrizione**: il problema, il finding o la revisione necessaria

## 3. Determina l'ID

Leggi il file per identificare tutti gli ID esistenti (formato `ISSUE-NNN`).
Assegna il prossimo ID disponibile. La numerazione non deve essere progressiva
senza buchi, ma ogni ID deve essere univoco.

## 4. Scrivi l'issue

Inserisci il nuovo issue in cima al file, dopo la sezione Indice, usando
questo formato:

```markdown
## ISSUE-{ID} — {Titolo}

**Tipo**: {finding | revision}
**Stato**: open
**Fase**: {fase}

**Storia**
- {YYYY-MM-DD} open — {motivazione apertura, una riga}

**Descrizione**

{descrizione del problema, finding o revisione}

**Domande aperte**
- [ ] {prima domanda, se presente}

**Impatto**
- {artefatto o fase} — {descrizione dell'impatto}

---
```

## 5. Aggiorna l'indice

Aggiungi una riga in cima alla tabella dell'indice:

```markdown
| ISSUE-{ID} | {Titolo} | open |
```

Aggiorna la nota:

```
> Ultimo issue inserito: ISSUE-{ID} — {YYYY-MM-DD}.
```

## Regole

- Un issue aperto non contiene mai la soluzione, solo il problema
- La motivazione nella Storia deve rispondere al "perche'" non al "cosa"
- Se le domande aperte non sono ancora note, ometti la sezione o lasciala vuota
