Inizializza un nuovo progetto nella directory corrente con il workflow issue-based.

## Procedura

### 1. Raccogli le informazioni del progetto

Chiedi all'utente le seguenti informazioni se non sono gia' presenti nel messaggio:

- **Nome del progetto** — identificatore del progetto
- **Path degli artefatti** — directory dove vivono gli artefatti da verificare
  durante la compliance dei backlog item. Esempi: `../code`, `./src`, `.`
  (stessa directory). Se il progetto non ha artefatti, rispondere "nessuno".

### 2. Verifica i file esistenti

Controlla file per file se `CLAUDE.md`, `issues.md` e `log.md` esistono gia'
nella directory corrente.

- I file **non esistenti** vengono creati negli step successivi
- I file **esistenti** vengono lasciati intatti senza chiedere conferma
- Se tutti e tre esistono gia', avverti l'utente che il progetto e' gia'
  inizializzato e non fare nulla

Negli step successivi, esegui solo la creazione dei file mancanti.

### 3. Crea `issues.md`

```markdown
# Issues — {Nome Progetto}

## Indice

| ID | Titolo | Stato |
|---|---|---|

> Ultimo issue inserito: —
> Ultimo issue chiuso: —
```

### 4. Crea `log.md`

```markdown
# Log — {Nome Progetto}
```

### 5. Crea `CLAUDE.md`

```markdown
# {Nome Progetto}

## Contesto

Questo progetto usa il workflow issue-based. Tutti i lavori non banali vengono
tracciati con un issue prima di iniziare e portati a `pending-approval` al
completamento. L'umano approva esplicitamente prima di procedere.

## Percorsi

- Documenti: .
- Artefatti: {path artefatti | "nessuno" se assente}

## Stato Corrente

- Fase: —
- Unita' attiva: —
- Issue aperti: nessuno

## File di progetto

- `issues.md` — issue aperti, ordinati per inserimento, indice in intestazione
- `log.md` — registro immutabile delle decisioni chiuse (prepend-only)

## Skills disponibili

| Comando | Quando usarlo |
|---|---|
| `/issue` | Aprire un nuovo issue |
| `/issue-update` | Aggiornare lo stato di un issue esistente |
| `/issue-close` | Chiudere un issue e scrivere l'entry nel log |
| `/rfc` | Generare una RFC da un issue in stato pending-rfc |
| `/log` | Aggiungere una entry manuale al log |
| `/backlog` | Gestire item di backlog durante la realizzazione |

## Principi operativi

**Ogni attivita' non banale passa per un issue.** Aprire l'issue prima di
iniziare il lavoro. Portarlo a `pending-approval` al completamento. Attendere
l'approvazione prima di procedere.

**Gli stati validi di un issue sono**: `open`, `in-progress`, `pending-approval`,
`pending-rfc`, `in-verification`, `deferred`.

**I tipi di issue sono**: `finding` (conoscenza nuova), `revision` (correzione
artefatto esistente), `anomalia` (comportamento difforme da quanto atteso).

**Il log e' immutabile.** Le entry vengono aggiunte in cima (prepend-only) e
non vengono mai modificate. Solo i cicli chiusi entrano nel log.

**issues.md e log.md vivono nella directory corrente.** Le skills li cercano
qui per default.
```

### 6. Conferma all'utente

Riporta i file creati e lo stato iniziale del progetto. Indica che il progetto
e' pronto: il passo successivo e' aprire il primo issue con `/issue`.
