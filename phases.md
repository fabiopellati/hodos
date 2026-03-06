Percorso di riferimento opzionale per opere che adottano un ciclo di vita
a fasi sequenziali. Questo skill e' descrittivo: non esegue azioni, non crea
file. Fornisce il contesto necessario a chi governa o all'AI per applicare
il percorso P0-P4 quando e come opportuno.

---

## Percorso P0-P4

Il percorso si articola in cinque fasi sequenziali. Ogni fase si chiude con
un gate di approvazione esplicita prima di procedere alla successiva.

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

**Directory**: `docs/inception/`

**Artefatti attesi**:
- `objectives.md` — obiettivi misurabili, vincoli, stakeholder, criteri di successo
- `features-overview.md` — funzionalita' in/out scope, priorita'

**Gate**: approvazione di entrambi gli artefatti prima di aprire P1.

---

## P1 — Analysis

**Scopo**: tradurre gli obiettivi in specifiche realizzabili.

**Domande guida**:
- Quali sono gli scenari d'uso rilevanti?
- Quali requisiti funzionali e non funzionali emergono?
- Come e' strutturato il risultato atteso?
- In quale ordine si realizza?

**Directory**: `docs/analysis/`

**Artefatti attesi**:
- `use-cases.md` — scenari d'uso rilevanti
- `specs-functional.md` — requisiti funzionali
- `specs-non-functional.md` — requisiti non funzionali
- `architecture.md` — struttura del risultato atteso
- `execution-plan.md` — unita' di lavoro, ordine, milestone

**Gate**: approvazione del piano esecutivo. Il piano autorizza l'avvio della
realizzazione.

---

## P2 — Realizzazione

**Scopo**: realizzare quanto pianificato, unita' per unita'.

**Ciclo per ogni unita'**:
1. Design — progettazione dettagliata
2. Gate: approvazione del design
3. Iterazioni — cicli brevi: pianifica / realizza / verifica / chiudi
4. Integrazione nell'aggregato o nell'opera

**Directory**: `docs/unita'/[nome]/`

**Artefatti attesi per unita'**:
- `design.md` — progettazione dettagliata
- `backlog.md` — iterazioni con obiettivi, backlog item, note

**Nota**: finding e problemi inattesi vanno in `issues.md`, non nel backlog.
Il backlog e' proattivo (nasce dalla pianificazione); l'issue e' reattivo
(nasce da un problema).

---

## P3 — Integration

**Scopo**: verificare il risultato nel suo insieme.

**Domande guida**:
- Le unita' si integrano correttamente?
- Il risultato complessivo rispetta le specifiche di P1?
- Ci sono disallineamenti tra unita' o rispetto alle aspettative?

**Directory**: nessuna propria. La verifica opera sugli artefatti delle
fasi precedenti.

**Nota**: gli issue che emergono qui non sono anomalie di singole unita'
(P2) ma disallineamenti sistemici. Se un issue invalida assunzioni di fasi
precedenti, aprire issue collegati (propagazione a ritroso).

**Gate**: approvazione prima di aprire P4.

---

## P4 — Consegna

**Scopo**: portare a destinazione una versione stabile.

**Attivita'**:
- Verifiche finali
- Approvazione della versione
- Consegna al destinatario o messa a disposizione

**Gate**: approvazione esplicita della consegna.

---

## Struttura directory di riferimento

```
docs/
  inception/
    objectives.md
    features-overview.md
  analysis/
    use-cases.md
    specs-functional.md
    specs-non-functional.md
    architecture.md
    execution-plan.md
  unita'/
    [nome-unita']/
      design.md
      backlog.md
    [nome-aggregato]/
      design.md
      backlog.md
      [nome-unita']/
        design.md
        backlog.md
```
