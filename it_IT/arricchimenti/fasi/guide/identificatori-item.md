---
tipo-artefatto: guida
documento: identificatori-item
descrizione: convenzione di identificazione univoca per gli item nei documenti di fase P0-P1
autorita: operativa
arricchimento: fasi
---

# Convenzione di Identificazione — Item dei
# Documenti di Fase P0-P1

Quando l'arricchimento fasi è attivo, i documenti di
progetto delle fasi P0 e P1 contengono item che
rappresentano unità concettuali distinte: obiettivi,
stakeholder, funzionalità, scenari, requisiti e così
via. Ciascun item deve portare un identificatore
univoco che consenta di riferirlo in modo non ambiguo
all'interno dell'opera, sia nel documento che lo
definisce sia in qualsiasi altro documento che vi
faccia riferimento.

Senza una convenzione esplicita, l'agente introduce
identificatori in modo arbitrario e incoerente, oppure
non li introduce affatto. Il risultato è una
documentazione che non consente la tracciabilità tra
fasi: un requisito senza riferimento all'obiettivo che
lo motiva o allo scenario che lo descrive perde la
catena di derivazione che dà valore al percorso P0-P4.

---

## Schema di nomenclatura

Il formato di un identificatore è:

```
{PREFISSO}-{NNN}
```

Il prefisso è una sigla di tre lettere maiuscole che
identifica il tipo di item. La numerazione è
progressiva, con padding a tre cifre (001, 002, ...).
La numerazione è locale al documento: il primo item di
ciascun tipo parte da 001.

Nelle fasi P0 e P1 la località al documento produce di
fatto l'unicità nell'opera, perché i documenti di quelle
fasi esistono in una sola copia: c'è un solo
`3-scenari.md` e un solo `4-requisiti.md`, sicché
`SCN-002` individua un solo item ovunque lo si citi.
La proprietà non vale però per costruzione, e cade
appena il documento che ospita la numerazione esiste in
più copie, come accade in P2, dove ogni unità ha i
propri documenti. Su questo si veda la sezione
«Citazione fuori dall'ambito di numerazione».

---

## Tipi di item e prefissi

### P0 — Definizione

Gli item dei documenti P0 usano i prefissi seguenti.

- **OBT** — Obiettivo. Definito in `1-obiettivi.md`.
  Rappresenta un obiettivo misurabile dell'opera.
- **STK** — Stakeholder. Definito in `1-obiettivi.md`.
  Rappresenta un attore o un gruppo portatore di
  interesse.
- **VPR** — Vincolo di progetto. Definito in
  `1-obiettivi.md`. Rappresenta un vincolo non
  negoziabile che condiziona l'intera opera.
- **CRS** — Criterio di successo. Definito in
  `1-obiettivi.md`. Rappresenta una condizione
  verificabile per il successo dell'opera.
- **FNZ** — Funzionalità. Definita in
  `2-panoramica-funzionalita.md`. Rappresenta una
  capacità in scope o esclusa dallo scope.

### P1 — Analisi

Gli item dei documenti P1 usano i prefissi seguenti.

- **SCN** — Scenario. Definito in `3-scenari.md`.
  Rappresenta uno scenario d'uso rilevante.
- **RFN** — Requisito funzionale. Definito in
  `4-requisiti.md`. Rappresenta un requisito che
  descrive cosa il risultato deve fare.
- **VNF** — Vincolo non funzionale. Definito in
  `5-vincoli.md`. Rappresenta un requisito di qualità,
  prestazione, sicurezza o altro vincolo non funzionale.
- **DST** — Decisione strutturale. Definita in
  `6-struttura.md`. Rappresenta una scelta progettuale
  significativa sulla struttura del risultato. Le DST
  determinano implicitamente le *parti* che
  compongono l'opera: una parte può emergere da una
  o più DST e una DST può determinare la forma di una
  o più parti.

Il piano esecutivo (`7-piano-esecutivo.md`) non
introduce un prefisso proprio: le unità di lavoro
definite nel piano sono identificate dal nome che
assumeranno nella fase P2 e riferiscono esplicitamente
le decisioni strutturali (DST) che realizzano,
oltre agli altri item delle fasi precedenti che le
motivano. La cardinalità della relazione fra parti
(DST) e unità è scelta di chi governa l'opera: può
essere uno-a-uno, molti-a-molti o mista. Il piano
esecutivo dichiara esplicitamente, per ciascuna unità,
le DST coinvolte.

---

## Tracciabilità cross-documento

Ogni item di P1 deve dichiarare la propria derivazione
dagli item delle fasi precedenti mediante riferimenti
espliciti. La derivazione segue la direzione naturale
del percorso: dagli obiettivi verso i requisiti.

Le regole di derivazione sono le seguenti.

- Ogni **scenario** (SCN) riferisce almeno un obiettivo
  (OBT) o una funzionalità (FNZ) da cui deriva.
- Ogni **requisito funzionale** (RFN) riferisce almeno
  uno scenario (SCN) che lo motiva.
- Ogni **vincolo non funzionale** (VNF) riferisce
  l'obiettivo (OBT), il vincolo di progetto (VPR) o lo
  scenario (SCN) che lo origina.
- Ogni **decisione strutturale** (DST) riferisce i
  requisiti (RFN) o i vincoli (VNF) che la determinano.

Il riferimento si esprime inserendo gli identificatori
tra parentesi tonde dopo la definizione dell'item o in
una riga dedicata. Il formato è libero purché gli
identificatori siano riconoscibili. Due esempi
equivalenti:

```markdown
- RFN-003 — Il sistema deve notificare l'operatore
  quando un dispositivo supera la soglia configurata
  (SCN-002, OBT-001)
```

```markdown
- RFN-003 — Il sistema deve notificare l'operatore
  quando un dispositivo supera la soglia configurata
  - Deriva da: SCN-002, OBT-001
```

La derivazione non deve essere forzata. Se un item
non ha una derivazione significativa da documentare
(per esempio un vincolo non funzionale che discende
da una norma esterna e non da un obiettivo interno),
il riferimento può essere omesso con una nota che
spiega l'origine.

---

## Citazione fuori dall'ambito di numerazione

Un identificatore numerato localmente individua il proprio item soltanto dentro l'ambito in cui la numerazione è locale.
Finché la citazione resta in quell'ambito la sigla nuda basta ed è la forma corretta: nel documento che definisce l'item non si scrive altro.
Appena la citazione esce dall'ambito, la sigla nuda non è più risolvibile, perché lo stesso identificatore esiste in ogni altra copia del documento che ospita quella numerazione.

Vale allora la regola seguente, che è una proprietà della struttura degli artefatti e non una convenzione di stile.

- Una citazione che esce dal proprio ambito di numerazione porta con sé il contesto sufficiente a risolvere l'identificatore, cioè l'ambito da cui proviene.
- Il contesto si accumula man mano che la citazione si allontana: una citazione interna all'opera dichiara l'unità di provenienza, una citazione che esce dall'opera dichiara anche l'opera.
- La forma concreta con cui il contesto si esprime è libera, purché sia riconoscibile e uniforme dentro la stessa opera.
  Chi adotta Hodos la fissa come propria convenzione, e questa guida non ne prescrive una: prescrive che il contesto ci sia.

La regola non è un'aggiunta al modo di titolare gli item, che resta quello dichiarato dallo schema di nomenclatura: riguarda la citazione, non la definizione.
Il titolo di un item non va quindi caricato del proprio contesto per renderlo citabile, perché il contesto appartiene a chi cita e non a chi definisce.

Il caso in cui la regola si applica più spesso è quello degli identificatori numerati localmente all'unità nella fase P2, cioè le voci di attività e le evoluzioni, che ripartono da uno in ciascuna unità.
Per le evoluzioni la necessità è esplicita nel percorso stesso, perché le evoluzioni locali generate nelle unità impattate da un'evoluzione cross-unità devono riferire l'evoluzione di coordinamento, che vive fuori dall'unità.

## Unicità e stabilità

Un identificatore, una volta assegnato, non viene mai
riassegnato a un item diverso, nemmeno se l'item
originale viene rimosso. Se un item viene eliminato
durante una revisione, il suo identificatore resta
vacante.

L'identificatore è stabile tra le versioni del
documento: un riferimento a RFN-003 in un documento di
P1 deve continuare a puntare allo stesso requisito
anche dopo revisioni successive del documento che lo
definisce.

---

## Ambito di applicazione

Questa convenzione si applica ai documenti di progetto
delle fasi P0 e P1 quando l'arricchimento fasi è
attivo. Non si applica ai documenti di processo
(questioni.md, mastro.md, notes.md), che hanno le
proprie convenzioni di identificazione (QUESTIONE-NNN,
NOTA-NNN, COMMENTO-NNN).

Per i documenti di P2 (design di unità), la
convenzione si estende naturalmente quando l'unità
adotta il design articolato: gli item nei documenti
di approfondimento dell'unità usano gli stessi prefissi
con numerazione locale al documento dell'unità.

In P2 quella località non produce però l'unicità nell'opera, a differenza di quanto accade in P0 e in P1, perché i documenti di unità esistono in una copia per ciascuna unità.
Vale quindi per essi la sezione «Citazione fuori dall'ambito di numerazione», che vale del pari per gli altri identificatori numerati localmente all'unità e non coperti da questo schema di nomenclatura, cioè le voci di attività (`BL-{N}`) e le evoluzioni (`EVO-{N}`).
