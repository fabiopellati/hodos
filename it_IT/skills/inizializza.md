---
skill: inizializza
client: Claude Code CLI
invocazione: /hodos-inizializza
tipo: operativo
locale: it_IT
---

Inizializza un nuovo progetto nella directory corrente con il workflow questione-based.

## Procedura

### 1. Raccogli le informazioni del progetto

Chiedi all'utente le seguenti informazioni se non sono già presenti nel messaggio:

- **Nome del progetto** — identificatore del progetto
- **Path degli artefatti** — directory dove vivono gli artefatti da verificare
  durante la conformità delle voci di attività. Esempi: `../code`, `./src`, `.`
  (stessa directory). Se il progetto non ha artefatti, rispondere "nessuno".

### 2. Verifica i file esistenti

Controlla file per file se `CLAUDE.md`, `questioni.md` e `mastro.md` esistono già
nella directory corrente.

- I file **non esistenti** vengono creati negli step successivi
- I file **esistenti** vengono lasciati intatti senza chiedere conferma
- Se tutti e tre esistono già, avverti l'utente che il progetto è già
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
| `/hodos-attivita` | Gestire attività durante la realizzazione |
| `/hodos-inizializza` | Inizializzare o riallineare il progetto |

**Principi**

- Ogni attività non banale passa per una questione aperta prima di iniziare
- L'approvazione umana è esplicita: pending-approval attende risposta prima di procedere
- Il tipo di una questione è immutabile dopo l'apertura
- Il mastro è immutabile: entry aggiunte in cima (prepend-only), mai modificate
- Un rilievo con impatto non vuoto richiede una revisione collegata aperta prima della chiusura

---

## {YYYY-MM-DD} — Adozione di Hodos: {Nome Progetto}

Decisione di adottare Hodos come metodologia operativa per questo progetto.
Il workflow questione-based regola tutte le attività non banali: apertura
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
Non eseguire operazioni di processo direttamente, anche quando il formato è noto.

| Operazione | Skill |
|---|---|
| Aprire una questione | `/hodos-questione` |
| Aggiornare stato o chiudere | `/hodos-aggiorna-questione` |
| Generare RFC | `/hodos-rfc` |
| Aggiungere nota | `/hodos-nota` |
| Gestire attività | `/hodos-attivita` |
| Riallineare il progetto | `/hodos-inizializza` |

## Vincoli

- Il tipo di una questione è immutabile dopo l'apertura
- Gli stati validi sono: `open`, `in-progress`, `pending-approval`, `pending-rfc`,
  `in-verification`, `deferred`, `closed`
- Un rilievo con campo Impatto non vuoto non può essere chiuso senza almeno
  una questione di revisione collegata aperta
- Il commento (COMMENTO-NNN) è immutabile e passivo: non modifica lo stato

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

Questo passo viene eseguito sempre, anche se i file di progetto esistevano già.
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

Nota: quando il server MCP Hodos è configurato (step 7), l'hook potrà
sostituire il confronto locale con una chiamata al tool `check_version` del
server, ottenendo la versione canonica corrente invece della versione
hardcoded negli skill installati.

### 7. Configura client MCP Hodos

Questo passo viene eseguito sempre, anche se i file di progetto esistevano già.
La configurazione viene sovrascritta ad ogni esecuzione di init per mantenere
l'URL aggiornato.

Leggi `.mcp.json` nella directory corrente se esiste; altrimenti parti da
`{ "mcpServers": {} }`.

Aggiungi (o aggiorna) la chiave `hodos` dentro `mcpServers` con questa
configurazione, senza modificare le altre chiavi presenti:

```json
{
  "mcpServers": {
    "hodos": {
      "type": "http",
      "url": "http://vps-350eddbb.vps.ovh.net/hodos/mcp/sse"
    }
  }
}
```

Scrivi il file aggiornato.

Al termine di questo step, avvisa l'operatore:

> Server MCP Hodos configurato in `.mcp.json`.
> Per attivarlo, esci e rientra nella sessione.

### 8. Conferma all'utente

Riporta i file creati e lo stato iniziale del progetto. Indica che il progetto
è pronto: il passo successivo è aprire la prima questione con `/hodos-questione`.

Se lo step 7 ha configurato il server MCP, ricorda all'operatore che deve
riavviare la sessione per rendere disponibili i tool MCP Hodos.
