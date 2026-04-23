---
tipo-artefatto: template
documento: claude-md
descrizione: struttura canonica del CLAUDE.md per un'opera Hodos
fase: trasversale
autorita: operativa
---

# Template — CLAUDE.md

Il file `CLAUDE.md` fornisce all'agente AI il contesto operativo dell'opera.
Viene creato durante l'inizializzazione e aggiornato quando cambia la fase
o lo stato dell'opera.

## Struttura

```markdown
# {Nome Opera}

**protocollo**: Hodos

## Contesto

Questa opera segue il protocollo Hodos. Per sapere come operare consulta
hodos-mcp.

## File di progetto

- `questioni.md` — questioni aperte, indice in intestazione
- `mastro.md` — registro immutabile delle decisioni chiuse (prepend-only)
- `notes.md` — note e memo

## Stato corrente

- Questioni aperte: nessuna

## Arricchimenti abilitati

nessuno
```

## Sezione documento-first per opere con fasi P0-P4

Quando l'opera adotta l'arricchimento fasi P0-P4, si
consiglia di aggiungere nel CLAUDE.md la seguente
sezione:

```markdown
## Direttiva documento-first

Questa opera adotta il flusso P0-P4. Il codice deriva
dai documenti di progetto, non viceversa. Non scrivere
codice senza che i documenti della fase corrente siano
prodotti e approvati.

I documenti di processo (questioni, mastro, note)
governano il ciclo ma non guidano l'implementazione.
I documenti di progetto (documenti/definizione/,
documenti/analisi/, documenti/unita/) guidano
l'implementazione.
```

La sezione serve come presidio diretto: il CLAUDE.md è
letto all'inizio di ogni sessione e l'agente lo ha
sempre in contesto, indipendentemente dal retrieval del
knowledge base.

## Regole

- Il CLAUDE.md non contiene le regole operative: quelle vivono nel protocollo
  e sono accessibili via hodos-mcp.
- Lo stato corrente va aggiornato quando cambiano la fase o le questioni attive.
- Il riferimento a hodos-mcp è sufficiente per l'agente: non replicare le
  istruzioni del protocollo nel CLAUDE.md.
- La sezione `Arricchimenti abilitati` elenca gli arricchimenti attivi
  nell'opera (es. fasi P0-P4, voci di attività). Se la sezione dice
  `nessuno`, l'agente non deve proporre funzionalità degli arricchimenti
  (fasi, voci di attività, iterazioni). Usare solo il protocollo base:
  questioni, note, commenti, mastro, RFC.
