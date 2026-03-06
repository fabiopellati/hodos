Inizializza un nuovo progetto nella directory corrente con il workflow questione-based.

## Procedura

### 1. Raccogli le informazioni del progetto

Chiedi all'utente le seguenti informazioni se non sono gia' presenti nel messaggio:

- **Nome del progetto** — identificatore del progetto
- **Path degli artefatti** — directory dove vivono gli artefatti da verificare
  durante la conformita' delle voci di attivita'. Esempi: `../code`, `./src`, `.`
  (stessa directory). Se il progetto non ha artefatti, rispondere "nessuno".

### 2. Verifica i file esistenti

Controlla file per file se `CLAUDE.md`, `questioni.md` e `mastro.md` esistono gia'
nella directory corrente.

- I file **non esistenti** vengono creati negli step successivi
- I file **esistenti** vengono lasciati intatti senza chiedere conferma
- Se tutti e tre esistono gia', avverti l'utente che il progetto e' gia'
  inizializzato e non fare nulla

Negli step successivi, esegui solo la creazione dei file mancanti.

### 3. Crea `questioni.md`

```markdown
# Questioni — {Nome Progetto}

## Indice

| ID | Titolo | Stato |
|---|---|---|

> Ultima questione inserita: —
> Ultima questione chiusa: —
```

### 4. Crea `mastro.md`

```markdown
# Mastro — {Nome Progetto}
```

### 5. Crea `CLAUDE.md`

```markdown
# {Nome Progetto}

## Contesto

Questo progetto usa il workflow questione-based. Tutti i lavori non banali vengono
tracciati con una questione prima di iniziare e portati a `pending-approval` al
completamento. L'umano approva esplicitamente prima di procedere.

## Percorsi

- Documenti: .
- Artefatti: {path artefatti | "nessuno" se assente}

## Stato Corrente

- Fase: —
- Unita' attiva: —
- Questioni aperte: nessuna

## File di progetto

- `questioni.md` — questioni aperte, ordinate per inserimento, indice in intestazione
- `mastro.md` — registro immutabile delle decisioni chiuse (prepend-only)

## Skill disponibili

| Comando | Quando usarlo |
|---|---|
| `/questione` | Aprire una nuova questione |
| `/aggiorna-questione` | Aggiornare lo stato di una questione esistente |
| `/chiudi-questione` | Chiudere una questione e scrivere l'entry nel mastro |
| `/rfc` | Generare una RFC da una questione in stato pending-rfc |
| `/mastro` | Aggiungere una entry manuale al mastro |
| `/attivita` | Gestire voci di attivita' durante la realizzazione |
| `/nota` | Aggiungere una nota |

## Principi operativi

**Ogni attivita' non banale passa per una questione.** Aprire la questione prima
di iniziare il lavoro. Portarla a `pending-approval` al completamento. Attendere
l'approvazione prima di procedere.

**Gli stati validi di una questione sono**: `open`, `in-progress`, `pending-approval`,
`pending-rfc`, `in-verification`, `deferred`.

**I tipi di questione sono**: `rilievo` (conoscenza nuova), `revisione` (correzione
artefatto esistente), `anomalia` (comportamento difforme da quanto atteso).

**Il mastro e' immutabile.** Le entry vengono aggiunte in cima (prepend-only) e
non vengono mai modificate. Solo i cicli chiusi entrano nel mastro.

**questioni.md e mastro.md vivono nella directory corrente.** Le skill li cercano
qui per default.
```

### 6. Conferma all'utente

Riporta i file creati e lo stato iniziale del progetto. Indica che il progetto
e' pronto: il passo successivo e' aprire la prima questione con `/questione`.
