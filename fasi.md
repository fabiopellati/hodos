Percorso di riferimento opzionale per opere che adottano un ciclo di vita
a fasi sequenziali. Questo skill e' descrittivo: non esegue azioni, non crea
file. Fornisce il contesto necessario a chi governa o all'AI per applicare
il percorso P0-P4 quando e come opportuno.

---

## Percorso P0-P4

Il percorso si articola in cinque fasi sequenziali. Ogni fase si chiude con
un'approvazione esplicita prima di procedere alla successiva.

Non e' obbligatorio attraversarle tutte: un'opera semplice puo' partire
direttamente da P2. Il percorso e' un riferimento, non un vincolo.

---

## P0 — Inception

**Scopo**: capire il problema prima di qualsiasi soluzione.

**Domande guida**:
- Qual e' l'obiettivo dell'opera?
- Chi sono gli stakeholder e cosa si aspettano?
- Quali sono i vincoli non negoziabili?
- Cosa e' in scope e cosa no?

**Directory**: `documenti/definizione/`

**Artefatti attesi**:
- `obiettivi.md` — obiettivi misurabili, vincoli, stakeholder, criteri di successo
- `panoramica-funzionalita.md` — funzionalita' in/out scope, priorita'

**Approvazione**: approvazione di entrambi gli artefatti prima di aprire P1.

---

## P1 — Analisi

**Scopo**: tradurre gli obiettivi in specifiche realizzabili.

**Domande guida**:
- Quali sono gli scenari d'uso rilevanti?
- Quali requisiti funzionali e non funzionali emergono?
- Come e' strutturato il risultato atteso?
- In quale ordine si realizza?

**Directory**: `documenti/analisi/`

**Artefatti attesi**:
- `scenari.md` — scenari d'uso rilevanti
- `requisiti.md` — requisiti funzionali
- `vincoli.md` — requisiti non funzionali
- `struttura.md` — struttura del risultato atteso
- `piano-esecutivo.md` — unita' di lavoro, ordine, milestone

**Approvazione**: approvazione del piano esecutivo. Il piano autorizza l'avvio
della realizzazione.

---

## P2 — Realizzazione

**Scopo**: realizzare quanto pianificato, unita' per unita'.

**Ciclo per ogni unita'**:
1. Design — progettazione dettagliata
2. Approvazione del design
3. Iterazioni — cicli brevi: pianifica / realizza / verifica / chiudi
4. Integrazione nell'aggregato o nell'opera

**Directory**: `documenti/unita/[nome]/`

**Artefatti attesi per unita'**:
- `design.md` — progettazione dettagliata
- `attivita.md` — iterazioni con obiettivi, voci di attivita', note

**Nota**: rilievi e problemi inattesi vanno in `questioni.md`, non nell'attivita'.
L'attivita' e' proattiva (nasce dalla pianificazione); la questione e' reattiva
(nasce da un problema).

---

## P3 — Integrazione

**Scopo**: verificare il risultato nel suo insieme.

**Domande guida**:
- Le unita' si integrano correttamente?
- Il risultato complessivo rispetta le specifiche di P1?
- Ci sono disallineamenti tra unita' o rispetto alle aspettative?

**Directory**: nessuna propria. La verifica opera sugli artefatti delle
fasi precedenti.

**Nota**: le questioni che emergono qui non sono anomalie di singole unita'
(P2) ma disallineamenti sistemici. Se una questione invalida assunzioni di
fasi precedenti, aprire questioni collegate (propagazione a ritroso).

**Approvazione**: approvazione prima di aprire P4.

---

## P4 — Consegna

**Scopo**: portare a destinazione una versione stabile.

**Attivita'**:
- Verifiche finali
- Approvazione della versione
- Consegna al destinatario o messa a disposizione

**Approvazione**: approvazione esplicita della consegna.

---

## Struttura directory di riferimento

```
documenti/
  definizione/
    obiettivi.md
    panoramica-funzionalita.md
  analisi/
    scenari.md
    requisiti.md
    vincoli.md
    struttura.md
    piano-esecutivo.md
  unita/
    [nome-unita]/
      design.md
      attivita.md
    [nome-aggregato]/
      design.md
      attivita.md
      [nome-unita]/
        design.md
        attivita.md
```
