---
tipo-artefatto: guida
documento: sviluppo-arricchimenti
descrizione: guida per chi sviluppa arricchimenti Hodos indipendenti
autorita: normativa
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
autorita: normativa    # o operativa, informativa
---
```

Il campo `tipo-artefatto` determina quale tool MCP
trova l'artefatto:

- `guida` e `ai` — trovati da `get_protocol_rules`
- `skill` — trovato da `get_skill` e `list_skills`
- Tutti i tipi — trovati da `search_knowledge`

### Il campo `autorita`

Il campo `autorita` dichiara quale rapporto l'artefatto intrattiene con le norme che tratta, ed è obbligatorio per ogni artefatto.
La ragione è che più artefatti trattano la medesima materia, uno perché ne è la sede e gli altri perché la applicano o la spiegano, e chi legge un testo isolato dal suo contesto deve poter sapere se ha davanti la norma o un suo derivato.
Il campo è dunque un'asserzione sul contenuto, che vale per qualunque lettore e non per un solo strumento.

Il canale MCP è uno di quei lettori, e ne trae due effetti.
Il primo è l'ordine: fra risultati di similarità comparabile serve per primo l'artefatto di autorità più alta, e un artefatto che non dichiara il campo vale quanto il più debole.
Il secondo è ciò che la sessione legge: sotto ogni risultato servito il canale dichiara se il testo enuncia la norma nella propria sede oppure la applica o la commenta, e per un artefatto che non dichiara il campo dichiara di non poterlo dire.
Chi assegna il valore decide quindi anche come il testo sarà qualificato a chi lo riceve.
Un valore diverso dai tre ammessi, anche per un refuso, non è segnalato da nessuno ed equivale al silenzio, non a una dichiarazione.
Che il canale legga il campo su un tipo di artefatto o su un altro dipende dal canale e può mutare: la dichiarazione resta dovuta su ogni artefatto, perché asserisce un fatto del contenuto e non un effetto atteso.

I valori sono tre, e si assegnano rispondendo alla domanda se la norma che il testo enuncia viva anche altrove.

- `normativa` — l'artefatto è la sede propria di almeno una norma, cioè la enuncia senza che essa derivi da un'altra sede. Sono normativi il protocollo, i principi, la skill di un arricchimento rispetto alle norme di quell'arricchimento, e ogni guida che stabilisce una regola o una convenzione che non è scritta altrove.
- `operativa` — l'artefatto applica norme stabilite altrove, portandone la forma o la procedura: i template, le procedure, gli strumenti di classificazione delle richieste dell'operatore.
- `informativa` — l'artefatto spiega, commenta o riassume norme stabilite altrove, senza aggiungervi né forma né regola: le FAQ, i glossari, le guide introduttive, i diagrammi.

Il campo si dichiara per file, e un file che sia sede propria di una norma e insieme ripeta norme altrui non può qualificare in modo diverso le due parti.
In quel caso il file dichiara `normativa`, e le parti che ripetono una norma stabilita altrove si riducono a un rinvio alla sede propria invece di riscriverla: una ripetizione concorre con la sede e a parità di autorità la vince quando la sua forma è più vicina alla domanda, mentre un rinvio ridotto all'essenziale non concorre, perché non ne porta il contenuto.

La dichiarazione è un'asserzione sul contenuto e va mantenuta con esso.
Un artefatto che acquista una norma propria cambia valore, e uno che la cede a un'altra sede lo cambia nel verso opposto.

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
