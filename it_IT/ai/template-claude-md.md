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

- Fase: —
- Questioni aperte: nessuna
```

## Regole

- Il CLAUDE.md non contiene le regole operative: quelle vivono nel protocollo
  e sono accessibili via hodos-mcp.
- Lo stato corrente va aggiornato quando cambiano la fase o le questioni attive.
- Il riferimento a hodos-mcp e' sufficiente per l'agente: non replicare le
  istruzioni del protocollo nel CLAUDE.md.
