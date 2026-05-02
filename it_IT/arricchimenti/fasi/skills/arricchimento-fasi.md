---
skill: arricchimento-fasi
client: Claude Code CLI
invocazione: /hodos-arricchimento-fasi
tipo: descrittivo
locale: it_IT
---

Percorso di riferimento opzionale per opere che adottano un ciclo di vita
a fasi sequenziali. Questo skill è descrittivo: non esegue azioni, non crea
file. Fornisce il contesto necessario a chi governa o all'AI per applicare
il percorso P0-P4 quando e come opportuno.

---

## Percorso P0-P4

Il percorso si articola in cinque fasi sequenziali. Ogni fase si chiude con
un'approvazione esplicita prima di procedere alla successiva.

Diagramma: [percorso P0-P4](../diagrams/fasi-p0-p4.puml)

Non è obbligatorio attraversarle tutte: un'opera semplice può partire
direttamente da P2. Il percorso è un riferimento, non un vincolo.

---

## P0 — Definizione

**Scopo**: capire il problema prima di qualsiasi soluzione.

**Domande guida**:
- Qual è l'obiettivo dell'opera?
- Chi sono gli stakeholder e cosa si aspettano?
- Quali sono i vincoli non negoziabili?
- Cosa è in scope e cosa no?

**Directory**: `documenti/definizione/`

**Artefatti attesi** (in ordine di redazione):
- `1-obiettivi.md` — obiettivi misurabili, vincoli, stakeholder, criteri di successo
- `2-panoramica-funzionalita.md` — funzionalità in/out scope, priorità

**Identificatori**: prima di redigere gli artefatti P0,
consultare la guida `identificatori-item` con
`search_knowledge("identificatori item documenti fase")`
per applicare la convenzione di identificazione univoca
agli item (obiettivi, stakeholder, vincoli, criteri di
successo, funzionalità).

**Approvazione**: approvazione di entrambi gli artefatti prima di aprire P1.

---

## P1 — Analisi

**Scopo**: tradurre gli obiettivi in specifiche realizzabili.

**Domande guida**:
- Quali sono gli scenari d'uso rilevanti?
- Quali requisiti funzionali e non funzionali emergono?
- Come è strutturato il risultato atteso?
- In quale ordine si realizza?

**Directory**: `documenti/analisi/`

**Artefatti attesi** (in ordine di redazione):
- `3-scenari.md` — scenari d'uso rilevanti
- `4-requisiti.md` — requisiti funzionali
- `5-vincoli.md` — requisiti non funzionali
- `6-struttura.md` — struttura del risultato atteso: parti
  che lo compongono e decisioni strutturali (DST)
- `7-piano-esecutivo.md` — unità di lavoro, ordine, milestone

**Identificatori**: prima di redigere gli artefatti P1,
consultare la guida `identificatori-item` con
`search_knowledge("identificatori item documenti fase")`
per applicare la convenzione di identificazione univoca
agli item (scenari, requisiti funzionali, vincoli non
funzionali, decisioni strutturali) e le regole di
tracciabilità cross-documento.

**Approvazione**: approvazione del piano esecutivo. Il piano autorizza l'avvio
della realizzazione.

---

## P2 — Realizzazione

**Scopo**: realizzare quanto pianificato, unità per unità.

**Ciclo per ogni unità**:
1. Design — progettazione dettagliata
2. Approvazione del design
3. Iterazioni — cicli brevi: pianifica / realizza / verifica / chiudi
4. Integrazione nell'aggregato o nell'opera

**Directory**: `documenti/unita/[nome]/`

**Artefatti attesi per unità**:
- `1-design.md` — progettazione dettagliata (file singolo)
- `2-attivita.md` — iterazioni con obiettivi, voci di attività, note

Il prefisso numerico indica l'ordine naturale di lettura,
coerentemente con la convenzione adottata in P0 e P1.

Quando la complessità dell'unità lo richiede, il `1-design.md` può
articolarsi in una directory di documenti: vedi la sezione dedicata
più avanti.

**Nota**: rilievi e problemi inattesi vanno in `questioni.md`, non nell'attività.
L'attività è proattiva (nasce dalla pianificazione); la questione è reattiva
(nasce da un problema).

### Aggregato

Un aggregato è un raggruppamento di unità per correlazione forte.
Le unità dentro un aggregato hanno una relazione semantica più
stretta tra loro che con il resto dell'opera, ma questo non esclude
che abbiano relazioni con unità fuori dall'aggregato. Il valore è
organizzativo e di navigazione: chi legge la struttura documentale
trova le unità raggruppate per affinità di dominio anziché in un
elenco piatto. Non è un confine rigido di isolamento.

**Criterio di attivazione**: la decisione di raggruppare unità in
un aggregato si prende nel piano esecutivo (P1), quando chi governa
riconosce una correlazione forte che giustifica un raggruppamento
semantico. Non si introduce un aggregato durante P2.

**Artefatti dell'aggregato**:
- `design.md` — motiva il criterio di raggruppamento: perché
  queste unità stanno insieme, qual è la correlazione che le lega.
  Non prescrive decisioni architetturali alle unità contenute.

L'aggregato non ha un proprio `2-attivita.md`. Le unità gestiscono
le proprie attività in autonomia.

**Vincolo di profondità**: un aggregato contiene unità, mai altri
aggregati.

---

## P3 — Integrazione

**Scopo**: verificare il risultato nel suo insieme.

**Domande guida**:
- Le unità si integrano correttamente?
- Il risultato complessivo rispetta le specifiche di P1?
- Ci sono disallineamenti tra unità o rispetto alle aspettative?

**Directory**: nessuna propria. La verifica opera sugli artefatti delle
fasi precedenti.

**Nota**: le questioni che emergono qui non sono anomalie di singole unità
(P2) ma disallineamenti sistemici. Se una questione invalida assunzioni di
fasi precedenti, aprire questioni collegate (propagazione a ritroso).

**Approvazione**: approvazione prima di aprire P4.

---

## P4 — Consegna

**Scopo**: portare a destinazione una versione stabile.

**Attività**:
- Verifiche finali
- Approvazione della versione
- Consegna al destinatario o messa a disposizione

**Approvazione**: approvazione esplicita della consegna.

---

## Questioni e wall

Le questioni in `questioni.md` tracciano il processo, non lo contengono.
Gli elaborati prodotti da ogni fase vivono nei propri file; il wall
registra apertura, progressione e chiusura.

**Una questione di revisione per fase o blocco di fasi:**

```
## QUESTIONE-NNN — Fase P0-P1: [titolo opera]

**Tipo**: revisione
**Stato**: open

**Storia**
- YYYY-MM-DD open — Avvio P0: raccolta obiettivi e vincoli.
- YYYY-MM-DD in-progress — P0 completato, avvio P1.
- YYYY-MM-DD closed — Piano esecutivo approvato.

**Elaborati prodotti**
- `documenti/definizione/1-obiettivi.md`
- `documenti/analisi/7-piano-esecutivo.md`
```

**Una questione di revisione per unità di esecuzione:**

```
## QUESTIONE-NNN — Unità: [nome unità]

**Tipo**: revisione
**Stato**: open

**Storia**
- YYYY-MM-DD open — Avvio design unità.
- YYYY-MM-DD in-progress — Design approvato, avvio iterazioni.
- YYYY-MM-DD closed — Unità completata e integrata.

**Elaborati prodotti**
- `documenti/unita/[nome]/1-design.md` (o `0-design.md` + documenti di approfondimento)
- `documenti/unita/[nome]/2-attivita.md`
```

La granularità minima è una questione per fase significativa e una per
unità. Non si aprono questioni per ogni micro-passo: i passi di esecuzione
vivono nel `2-attivita.md` dell'unità.

Questo modello vale per umano e AI. Quando l'AI elabora un ciclo P0-P4
in autonomia, apre la questione di fase, produce gli elaborati nei propri
file, aggiorna la storia al completamento di ogni elaborato significativo,
e chiude la questione quando la fase è verificata e approvata.

---

## RFC di dispaccio verso operations esterno

In P2 e nelle fasi successive, governance può dover delegare l'esecuzione
di un pacchetto di BL o EVO a un team esterno che svolge il ruolo di
operations senza accesso ai documenti di processo Hodos. In questo contesto
la RFC è lo strumento di comunicazione corretto.

**Quando usarla**: quando operations esterno deve ricevere un insieme di
item da eseguire in autonomia e restituire evidenza del completamento per
consentire la verifica da parte di governance.

**Come funziona**:

1. Governance apre una questione che traccia il dispaccio e la porta a
   `pending-rfc`.
2. Genera la RFC con la sezione Richiesta strutturata come elenco di BL
   o EVO, ciascuno con contesto sufficiente per l'esecuzione autonoma.
3. Team-B riceve la RFC, valuta e può accettare, rifiutare con motivazione
   o posticipare.
4. Se Team-B accetta, esegue il lavoro e compila la Response RFC.
5. Governance verifica e chiude la questione.

**Ciclo multi-round**: se Team-B rileva un gap che non può risolvere
autonomamente, rifiuta e lo documenta come COMMENTO-NNN alla RFC. Governance
analizza il gap, risponde con il commento successivo che chiarisce o risolve,
e Team-B può procedere. La Response RFC è unica: è la risposta conclusiva
definitiva. Il ciclo può iterarsi più volte; la questione resta in
`pending-rfc` per l'intera durata.

---

## Ciclo post-release

Dopo P4 approvato e prima release taggata su `main`, l'opera entra nel
regime iterativo post-release. La definizione normativa del ciclo —
condizioni di ingresso, modello iterativo, ruolo del backlog, caso hotfix —
è in `../ai/ciclo-post-release.md`.

Operativamente, ogni ciclo post-release si traccia con questioni nel normale
ciclo Hodos e produce una release approvata taggata su `main`.

---

## Evoluzione di unità mature

Quando un'unità è stata consegnata e i suoi documenti di design
riflettono lo stato corrente, le modifiche successive si gestiscono
in funzione della loro scala.

### Modifiche minori

Una modifica minore è una variazione entro i pattern esistenti
dell'unità: un nuovo filtro, un campo aggiuntivo, una regola di
validazione. Non introduce nuovi scenari d'uso, non modifica il
modello dati o le transizioni di stato, non ha impatto su altre
unità.

Il flusso è un BL in `2-attivita.md` che prescrive nella sezione
Richiesta sia la realizzazione sia l'aggiornamento dei documenti
di design impattati. I Criteri di verifica devono includere la
coerenza tra il design aggiornato e la realizzazione. La
tracciabilità è garantita da git (il commit modifica codice e
documenti insieme) e dalla questione che motiva la variazione.

### Modifiche significative — evoluzione

Una modifica è significativa quando soddisfa uno o più di questi
criteri:

- introduce nuovi scenari d'uso
- modifica il modello dati o le transizioni di stato
- ha impatto su altre unità

Questi criteri sono una guida per chi governa, non una regola
binaria. La decisione sulla scala della modifica è di chi governa.

Per le modifiche significative si redige un'**evoluzione**
(`EVO-{N}-{titolo}.md`), un artefatto che documenta il passaggio
da uno stato del design a un altro. L'evoluzione viene approvata
prima della realizzazione. Dopo l'approvazione, la realizzazione
avviene tramite BL in `2-attivita.md` e include l'aggiornamento
dei documenti di design per assorbire il delta.

L'evoluzione resta nella directory dell'unità come documento
storico congelato: non si modifica dopo l'approvazione. Nel tempo,
la sequenza delle evoluzioni forma una catena narrativa che spiega
come l'unità è giunta allo stato corrente. Il design riflette
sempre lo stato attuale; le evoluzioni spiegano le transizioni.

### Evoluzioni cross-unità

Un'evoluzione che coinvolge più unità richiede un documento di
coordinamento che descrive la visione d'insieme: motivazione,
coordinamento tra unità, flusso end-to-end. La collocazione segue
una regola a due livelli:

- Se tutte le unità coinvolte appartengono allo stesso aggregato,
  l'evoluzione di coordinamento vive nella directory
  dell'aggregato.
- Se l'evoluzione attraversa aggregati diversi o coinvolge unità
  isolate, l'evoluzione di coordinamento vive a livello di opera
  in `documenti/evoluzioni/EVO-{N}-{titolo}.md`.

Le evoluzioni locali generate nelle singole unità impattate vivono
nella directory di ciascuna unità e fanno riferimento
all'evoluzione di coordinamento. Ogni sequenza numerica è
indipendente.

---

## Design articolato per unità complesse

Un'unità semplice usa un singolo `1-design.md` nella propria directory.
Un'unità complessa — con scenari d'uso multipli, modelli dati articolati,
transizioni di stato e vincoli di dominio propri — può articolare il
design in una directory di documenti. La scelta tra le due forme è di
chi governa l'unità, in base alla profondità analitica necessaria.

**Struttura del design articolato**:

```
documenti/unita/[nome-unita]/
  0-design.md       <- punto di ingresso e indice ragionato
  1-obiettivi.md    <- perché, scope, criteri di successo
  2-scenari.md      <- scenari d'uso del dominio
  3-requisiti.md    <- requisiti funzionali dell'unità
  4-vincoli.md      <- requisiti non funzionali, vincoli
  5-struttura.md    <- architettura, modello dati, integrazioni
  2-attivita.md     <- voci di attività (invariato)
```

**Convenzioni**:

- Il file `0-design.md` è il punto di ingresso che sostituisce
  `1-design.md` nel caso articolato. Deve contenere le decisioni
  chiave e un indice ragionato dei documenti di approfondimento.
- I documenti da 1 a 5 articolano il design in profondità. Il prefisso
  numerico indica l'ordine di lettura, non l'ordine di produzione. Non
  tutti i documenti sono obbligatori.
- La struttura rispecchia quella dei documenti di progetto (P0/P1) perché
  il lavoro analitico ha la stessa forma a qualsiasi scala.

**Approvazione**: l'approvazione di `0-design.md` copre l'intero pacchetto
di design. Non è necessaria un'approvazione esplicita per ciascun
documento di approfondimento.

---

## Struttura directory di riferimento

```
documenti/
  definizione/
    1-obiettivi.md
    2-panoramica-funzionalita.md
  analisi/
    3-scenari.md
    4-requisiti.md
    5-vincoli.md
    6-struttura.md
    7-piano-esecutivo.md
  unita/
    [unita-semplice]/
      1-design.md
      2-attivita.md
      EVO-1-titolo.md        <- evoluzione (se presente)
    [unita-complessa]/
      0-design.md
      1-obiettivi.md
      2-scenari.md
      3-requisiti.md
      4-vincoli.md
      5-struttura.md
      2-attivita.md
      EVO-1-titolo.md        <- evoluzione (se presente)
    [nome-aggregato]/
      design.md
      EVO-1-titolo.md        <- evo cross-unità intra-aggregato
      [nome-unita]/
        1-design.md
        2-attivita.md
  evoluzioni/                <- evo cross-unità inter-aggregato
    EVO-1-titolo.md
```
