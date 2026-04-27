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
