---
tipo-artefatto: ai
documento: procedura-arricchimento-esterno
descrizione: procedura per un agente AI che sviluppa un arricchimento Hodos indipendente
autorita: operativa
---

# Procedura — Arricchimento Hodos Esterno

Quando l'agente sviluppa un arricchimento Hodos in un
progetto indipendente (non nel repository artefatti
centrale), deve produrre gli artefatti necessari
affinché hodos-mcp possa indicizzarli e renderli
disponibili nel knowledge base.

## Struttura obbligatoria del repository

Creare la directory `artefatti/` nella root del
repository con la struttura per locale:

```
artefatti/
  it_IT/
    guide/
      arricchimento-{nome}.md
    skills/
      arricchimento-{nome}.md
```

Solo il contenuto di `artefatti/` viene indicizzato
da hodos-mcp. Artefatti fuori da questa directory non
sono visibili nel knowledge base.

## Artefatti da produrre

### 1. Guida (obbligatoria)

File: `artefatti/it_IT/guide/arricchimento-{nome}.md`

Frontmatter:

```yaml
---
tipo-artefatto: guida
documento: arricchimento-{nome}
descrizione: {descrizione breve, una riga}
autorita: informativa
---
```

Contenuto: descrizione in prosa di cos'è
l'arricchimento, quando è utile, quali prerequisiti
richiede e come si abilita. Deve contenere le parole
chiave che un operatore userebbe per cercarlo.

Questo artefatto serve alla discovery: è trovato da
`get_protocol_rules` e da `search_knowledge`. Senza
questo artefatto l'arricchimento è invisibile alle
query semantiche più comuni.

### 2. Skill (obbligatorio)

File: `artefatti/it_IT/skills/arricchimento-{nome}.md`

Frontmatter:

```yaml
---
tipo-artefatto: skill
skill: arricchimento-{nome}
documento: arricchimento-{nome}
descrizione: {descrizione breve, una riga}
autorita: operativa
---
```

Il campo `skill` è obbligatorio: senza di esso i tool
`get_skill` e `list_skills` non trovano l'artefatto.
Il tool `search_knowledge` lo trova comunque perché
usa la ricerca vettoriale senza filtrare per nome
skill, il che rende il problema difficile da
diagnosticare.

Contenuto: istruzioni operative per l'agente. Ogni
passo deve essere eseguibile senza contesto esterno.
Include:
- Configurazione (variabili d'ambiente, file da creare)
- Catalogo dei tool o delle funzionalità esposte
- Regole operative specifiche dell'arricchimento
- Limiti noti

Questo artefatto serve all'operatività: è trovato da
`get_skill` con il nome esatto e da `list_skills`.

## Frontmatter — mapping tipo/tool

Il campo `tipo-artefatto` determina quale tool MCP
trova l'artefatto:

- `guida`, `ai` — trovati da `get_protocol_rules`
- `skill` — trovato da `get_skill` e `list_skills`
- tutti i tipi — trovati da `search_knowledge`

## Vincoli di congruenza

L'arricchimento non deve contraddire il protocollo
base. Verificare prima della pubblicazione:

- Non consente operazioni che violino l'immutabilità
  del mastro
- Non suggerisce di saltare le approvazioni esplicite
- Non introduce template che omettano sezioni
  obbligatorie del protocollo
- Non definisce procedure che contraddicano le regole
  di ingaggio

## Sincronizzazione

Dopo il commit e il tag nel repository
dell'arricchimento:

```bash
curl -X POST \
  https://vps-350eddbb.vps.ovh.net/hodos/mcp/sync \
  -H "Content-Type: application/json" \
  -d '{"source": "{nome-sorgente}", "tag": "vX.Y.Z"}'
```

Verificare con `check_version` che il conteggio
artefatti sia coerente. Verificare con
`search_knowledge` che la guida emerga con query
pertinenti. Verificare con `get_skill` che lo skill
sia raggiungibile per nome.

## Registrazione sorgente

La sorgente deve essere registrata nel server
hodos-mcp prima del primo sync. La registrazione è
a carico del team hodos-mcp.
