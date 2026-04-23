---
tipo-artefatto: guida
documento: sviluppo-arricchimenti
descrizione: guida per chi sviluppa arricchimenti Hodos indipendenti
autorita: informativa
---

# Guida allo Sviluppo di Arricchimenti Hodos

Questa guida si rivolge a chi sviluppa un arricchimento
per il protocollo Hodos come progetto indipendente. Un
arricchimento è un'estensione opzionale che aggiunge
funzionalità al protocollo base senza modificarlo.

Ogni arricchimento è un progetto autonomo con il proprio
repository, il proprio ciclo di rilascio e la propria
documentazione. L'integrazione nel knowledge base di
hodos-mcp avviene tramite sincronizzazione multi-root:
il server MCP indicizza gli artefatti da sorgenti
multiple, ciascuna indipendente dalle altre.

---

## Responsabilità dell'arricchimento

L'arricchimento è responsabile della propria visibilità
nel knowledge base. L'agente AI scopre gli arricchimenti
disponibili interrogando hodos-mcp: se l'arricchimento
non produce gli artefatti giusti, l'agente non lo trova
e non lo propone all'operatore.

Gli artefatti che un arricchimento deve produrre sono
di due categorie: quelli per la discovery (farsi trovare)
e quelli per l'operatività (farsi usare).

---

## Artefatti per la discovery

L'agente AI cerca informazioni nel knowledge base
usando diversi tool, ciascuno con il proprio ambito:

- `get_protocol_rules` — cerca artefatti di tipo
  `guida`, `regola`, `ai`. È il tool usato più
  frequentemente dall'agente per rispondere a domande
  generali sul protocollo e sugli arricchimenti
- `get_skill` — restituisce uno skill per nome esatto.
  Richiede che l'agente conosca già il nome
- `search_knowledge` — cerca trasversalmente su tutti
  i tipi di artefatto. È il fallback per query
  esplorative
- `list_skills` — elenca gli skill disponibili. Utile
  per la discovery ma l'agente deve sapere di doverlo
  chiamare

Per essere trovato da un agente che non sa ancora che
l'arricchimento esiste, è necessario produrre almeno
un artefatto di tipo `guida` o `ai` che descriva
l'arricchimento in prosa. Questo artefatto deve:

- Avere un titolo che includa la parola "arricchimento"
  e il nome dell'arricchimento
- Descrivere in linguaggio naturale cos'è
  l'arricchimento, quando è utile e come si abilita
- Contenere le parole chiave che un operatore userebbe
  per cercarlo (es. "operazioni deterministiche",
  "firma utente", "fasi di progetto")

Un arricchimento che pubblica solo uno skill (di tipo
`skill`) non viene trovato da `get_protocol_rules` e
risulta invisibile nelle query semantiche più comuni.

---

## Artefatti per l'operatività

Lo skill è il documento operativo che l'agente
consulta per sapere come usare l'arricchimento. Deve
contenere:

- Le istruzioni di configurazione (prerequisiti,
  variabili d'ambiente, file da creare)
- Il catalogo dei tool o delle funzionalità esposte
- Le regole operative specifiche dell'arricchimento
- I limiti noti

Lo skill è un documento per l'agente esecutore: ogni
passo deve essere eseguibile senza contesto esterno.

---

## Struttura del repository

Gli artefatti devono risiedere in una directory
`artefatti/` nella root del repository, organizzati
per locale:

```
artefatti/
  it_IT/
    guide/
      arricchimento-nome.md    <- discovery
    skills/
      arricchimento-nome.md    <- operatività
```

La directory `artefatti/` è quella che hodos-mcp
indicizza durante la sincronizzazione. Gli artefatti
al di fuori di questa directory non vengono indicizzati.

---

## Frontmatter

Ogni artefatto deve avere un frontmatter YAML con i
campi necessari al sistema di indicizzazione:

```yaml
---
tipo-artefatto: guida    # o skill, regola, ai
documento: nome-documento
descrizione: descrizione breve per l'indicizzazione
autorita: informativa    # o operativa
---
```

Il campo `tipo-artefatto` determina quale tool MCP
trova l'artefatto:

- `guida` e `ai` — trovati da `get_protocol_rules`
- `skill` — trovato da `get_skill` e `list_skills`
- Tutti i tipi — trovati da `search_knowledge`

---

## Sincronizzazione

L'arricchimento deve essere registrato come sorgente
nel server hodos-mcp. La registrazione è a carico del
team hodos-mcp.

Dopo ogni rilascio, la sincronizzazione avviene con
una chiamata HTTP:

```bash
curl -X POST \
  https://vps-350eddbb.vps.ovh.net/hodos/mcp/sync \
  -H "Content-Type: application/json" \
  -d '{"source": "nome-sorgente", "tag": "vX.Y.Z"}'
```

Il campo `source` deve corrispondere al nome della
sorgente registrata. Il campo `tag` deve corrispondere
a un tag git nel repository dell'arricchimento.

---

## Congruenza con il protocollo

L'arricchimento non deve contraddire i vincoli del
protocollo base. In particolare:

- Non deve consentire operazioni che violino
  l'immutabilità del mastro
- Non deve suggerire all'agente di saltare le
  approvazioni esplicite
- Non deve introdurre template che omettano sezioni
  obbligatorie del protocollo
- Non deve definire procedure che contraddicano le
  regole di ingaggio

Il progetto Hodos come gestore del protocollo ha la
responsabilità di verificare la congruenza degli
arricchimenti esterni. La verifica avviene tramite
hodos-mcp, usando `search_knowledge` con filtro
`source` per isolare gli artefatti della sorgente
e confrontarli con la base normativa.

---

## Checklist per un nuovo arricchimento

- [ ] Il repository ha una directory `artefatti/`
  con la struttura per locale
- [ ] Esiste almeno un artefatto di tipo `guida` o
  `ai` per la discovery
- [ ] Esiste almeno uno skill per l'operatività
- [ ] Tutti gli artefatti hanno il frontmatter con
  `tipo-artefatto` e `descrizione`
- [ ] La sorgente è registrata nel server hodos-mcp
- [ ] Il primo sync è stato eseguito e verificato
  con `check_version`
- [ ] Gli artefatti non contraddicono i vincoli del
  protocollo base
