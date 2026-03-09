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

## Costituzione

**Protocollo**: Hodos 1.0
**Inizializzazione**: {YYYY-MM-DD}

**Skill installati**

| Comando | Funzione |
|---|---|
| `/hodos-questione` | Aprire una questione |
| `/hodos-aggiorna-questione` | Aggiornare stato o chiudere |
| `/hodos-rfc` | Generare RFC da questione pending-rfc |
| `/hodos-nota` | Aggiungere una nota |
| `/hodos-attivita` | Gestire attivita' durante la realizzazione |
| `/hodos-inizializza` | Inizializzare o riallineare il progetto |

**Principi**

- Ogni attivita' non banale passa per una questione aperta prima di iniziare
- L'approvazione umana e' esplicita: pending-approval attende risposta prima di procedere
- Il tipo di una questione e' immutabile dopo l'apertura
- Il mastro e' immutabile: entry aggiunte in cima (prepend-only), mai modificate
- Un rilievo con impatto non vuoto richiede una revisione collegata aperta prima della chiusura

---

## {YYYY-MM-DD} — Adozione di Hodos: {Nome Progetto}

Decisione di adottare Hodos come metodologia operativa per questo progetto.
Il workflow questione-based regola tutte le attivita' non banali: apertura
della questione prima di iniziare, esecuzione, approvazione esplicita,
registrazione della decisione nel mastro.

---
```

### 5. Crea `CLAUDE.md`

```markdown
# {Nome Progetto}

**protocollo**: Hodos **versione**: 1.0

## Operazioni di processo

Per qualsiasi operazione sul processo usa lo skill corrispondente.
Non eseguire operazioni di processo direttamente, anche quando il formato e' noto.

| Operazione | Skill |
|---|---|
| Aprire una questione | `/hodos-questione` |
| Aggiornare stato o chiudere | `/hodos-aggiorna-questione` |
| Generare RFC | `/hodos-rfc` |
| Aggiungere nota | `/hodos-nota` |
| Gestire attivita' | `/hodos-attivita` |
| Riallineare il progetto | `/hodos-inizializza` |

## Vincoli

- Il tipo di una questione e' immutabile dopo l'apertura
- Gli stati validi sono: `open`, `in-progress`, `pending-approval`, `pending-rfc`,
  `in-verification`, `deferred`, `closed`
- Un rilievo con campo Impatto non vuoto non puo' essere chiuso senza almeno
  una questione di revisione collegata aperta
- Il commento (COMMENTO-NNN) e' immutabile e passivo: non modifica lo stato

## Contesto

- Artefatti: {path artefatti | "nessuno" se assente}
- Fase: —
- Questioni aperte: nessuna

## File di progetto

- `questioni.md` — questioni aperte, indice in intestazione
- `mastro.md` — registro immutabile delle decisioni chiuse (prepend-only)
- `notes.md` — note e memo (opzionale)
```

### 6. Installa hook SessionStart

Questo passo viene eseguito sempre, anche se i file di progetto esistevano gia'.
L'hook viene sovrascritto ad ogni esecuzione di init per mantenere la versione
aggiornata.

Crea la directory `.claude/hooks/` se non esiste.

Scrivi il file `.claude/hooks/hodos-check-version.sh`:

```bash
#!/bin/bash
# Hook SessionStart Hodos — verifica allineamento versione protocollo
VERSIONE_ATTESA="1.0"
CLAUDE_MD="CLAUDE.md"

if [ ! -f "$CLAUDE_MD" ]; then
  exit 0
fi

VERSIONE=$(grep "versione\*\*:" "$CLAUDE_MD" | sed 's/.*versione\*\*: *//' | tr -d ' \r\n')

if [ -z "$VERSIONE" ]; then
  exit 0
fi

if [ "$VERSIONE" != "$VERSIONE_ATTESA" ]; then
  echo "ATTENZIONE: versione protocollo Hodos non allineata."
  echo "CLAUDE.md dichiara versione $VERSIONE, skill installati versione $VERSIONE_ATTESA."
  echo "Esegui /hodos-inizializza per riallineare il progetto."
fi
```

Aggiorna `.claude/settings.json` aggiungendo la configurazione SessionStart.
Se il file non esiste, crealo. Se esiste, aggiungi la voce senza rimuovere
le configurazioni esistenti:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "bash .claude/hooks/hodos-check-version.sh"
          }
        ]
      }
    ]
  }
}
```

Nota: quando il server MCP Hodos sara' disponibile (Q052), l'hook potra'
sostituire il confronto locale con una chiamata al tool `check_version` del
server, ottenendo la versione canonica corrente invece della versione
hardcoded negli skill installati.

### 7. Conferma all'utente

Riporta i file creati e lo stato iniziale del progetto. Indica che il progetto
e' pronto: il passo successivo e' aprire la prima questione con `/hodos-questione`.
