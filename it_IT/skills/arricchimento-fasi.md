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
- `6-struttura.md` — struttura del risultato atteso
- `7-piano-esecutivo.md` — unità di lavoro, ordine, milestone

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
- `design.md` — progettazione dettagliata (file singolo)
- `attivita.md` — iterazioni con obiettivi, voci di attività, note

Quando la complessità dell'unità lo richiede, il design può articolarsi in
una directory di documenti: vedi la sezione dedicata più avanti.

**Nota**: rilievi e problemi inattesi vanno in `questioni.md`, non nell'attività.
L'attività è proattiva (nasce dalla pianificazione); la questione è reattiva
(nasce da un problema).

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
- `documenti/unita/[nome]/design.md` (o `0-design.md` + documenti di approfondimento)
- `documenti/unita/[nome]/attivita.md`
```

La granularità minima è una questione per fase significativa e una per
unità. Non si aprono questioni per ogni micro-passo: i passi di esecuzione
vivono nell'`attivita.md` dell'unità.

Questo modello vale per umano e AI. Quando l'AI elabora un ciclo P0-P4
in autonomia, apre la questione di fase, produce gli elaborati nei propri
file, aggiorna la storia al completamento di ogni elaborato significativo,
e chiude la questione quando la fase è verificata e approvata.

---

## Ciclo post-release

Dopo P4 approvato e prima release taggata su `main`, l'opera entra nel
regime iterativo post-release. La definizione normativa del ciclo —
condizioni di ingresso, modello iterativo, ruolo del backlog, caso hotfix —
è in `ai/ciclo-post-release.md`.

Operativamente, ogni ciclo post-release si traccia con questioni nel normale
ciclo Hodos e produce una release approvata taggata su `main`.

---

## Design articolato per unità complesse

Un'unità semplice usa un singolo `design.md` nella propria directory.
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
  attivita.md       <- voci di attività (invariato)
```

**Convenzioni**:

- Il file `0-design.md` è il punto di ingresso che soddisfa la
  prescrizione del protocollo. Deve contenere le decisioni chiave e un
  indice ragionato dei documenti di approfondimento.
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
      design.md
      attivita.md
    [unita-complessa]/
      0-design.md
      1-obiettivi.md
      2-scenari.md
      3-requisiti.md
      4-vincoli.md
      5-struttura.md
      attivita.md
    [nome-aggregato]/
      design.md
      attivita.md
      [nome-unita]/
        design.md
        attivita.md
```
