---
skill: arricchimento-fasi
client: Claude Code CLI
invocazione: /hodos-arricchimento-fasi
tipo: descrittivo
locale: it_IT
---

Percorso di riferimento opzionale per opere che adottano un ciclo di vita
a fasi sequenziali. Questo skill e' descrittivo: non esegue azioni, non crea
file. Fornisce il contesto necessario a chi governa o all'AI per applicare
il percorso P0-P4 quando e come opportuno.

---

## Percorso P0-P4

Il percorso si articola in cinque fasi sequenziali. Ogni fase si chiude con
un'approvazione esplicita prima di procedere alla successiva.

Diagramma: [percorso P0-P4](../diagrams/fasi-p0-p4.puml)

Non e' obbligatorio attraversarle tutte: un'opera semplice puo' partire
direttamente da P2. Il percorso e' un riferimento, non un vincolo.

---

## P0 — Definizione

**Scopo**: capire il problema prima di qualsiasi soluzione.

**Domande guida**:
- Qual e' l'obiettivo dell'opera?
- Chi sono gli stakeholder e cosa si aspettano?
- Quali sono i vincoli non negoziabili?
- Cosa e' in scope e cosa no?

**Directory**: `documenti/definizione/`

**Artefatti attesi** (in ordine di redazione):
- `1-obiettivi.md` — obiettivi misurabili, vincoli, stakeholder, criteri di successo
- `2-panoramica-funzionalita.md` — funzionalita' in/out scope, priorita'

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

**Artefatti attesi** (in ordine di redazione):
- `3-scenari.md` — scenari d'uso rilevanti
- `4-requisiti.md` — requisiti funzionali
- `5-vincoli.md` — requisiti non funzionali
- `6-struttura.md` — struttura del risultato atteso
- `7-piano-esecutivo.md` — unita' di lavoro, ordine, milestone

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

**Una questione di revisione per unita' di esecuzione:**

```
## QUESTIONE-NNN — Unita': [nome unita']

**Tipo**: revisione
**Stato**: open

**Storia**
- YYYY-MM-DD open — Avvio design unita'.
- YYYY-MM-DD in-progress — Design approvato, avvio iterazioni.
- YYYY-MM-DD closed — Unita' completata e integrata.

**Elaborati prodotti**
- `documenti/unita/[nome]/design.md`
- `documenti/unita/[nome]/attivita.md`
```

La granularita' minima e' una questione per fase significativa e una per
unita'. Non si aprono questioni per ogni micro-passo: i passi di esecuzione
vivono nell'`attivita.md` dell'unita'.

Questo modello vale per umano e AI. Quando l'AI elabora un ciclo P0-P4
in autonomia, apre la questione di fase, produce gli elaborati nei propri
file, aggiorna la storia al completamento di ogni elaborato significativo,
e chiude la questione quando la fase e' verificata e approvata.

---

## Ciclo post-release

Dopo P4 approvato e prima release taggata su `main`, l'opera entra nel
regime iterativo post-release. Ogni release successiva e' un ciclo compiuto,
non un regime indefinito.

**Modello**: il backlog alimenta ogni ciclo. Ogni ciclo produce una release.

### Condizione di ingresso

Il ciclo post-release si attiva quando:
- P4 e' approvato
- La prima release e' taggata su `main` con versione semantica

Prima di questa condizione, non esiste ancora un "in produzione" a cui riferirsi.

### Come funziona il ciclo

1. **Raccolta**: il backlog raccoglie richieste, bug segnalati, miglioramenti emersi post-consegna
2. **Prioritizzazione**: chi governa seleziona e ordina gli item per la release successiva
3. **Mini-ciclo P1-P2-P3**: l'insieme degli item selezionati percorre un ciclo ridotto di analisi, realizzazione e integrazione
4. **Release (P4)**: il ciclo si chiude con una nuova release approvata e taggata su `main`

La granularita' del mini-ciclo e' proporzionale alla complessita' degli item.
Per fix minori, P1 puo' ridursi a pochi appunti di analisi. Per evoluzioni
significative, il percorso completo e' appropriato.

### Come si traccia il lavoro

Il lavoro post-release si traccia con questioni nel normale ciclo Hodos:
- Una questione di revisione per ogni release (copre l'intero mini-ciclo)
- Questioni operative per item significativi

Non e' necessaria una struttura di documenti separata: si estendono le
directory esistenti o se ne aggiungono di nuove nella stessa opera.

### Il ruolo del backlog

Il backlog e' lo strumento di raccolta e prioritizzazione degli item
post-release. Non e' un documento di fase: e' trasversale al ciclo.

Negli arricchimenti che prevedono un file di backlog (`backlog.md`),
questo file persiste tra un ciclo e l'altro e raccoglie item in attesa
di essere inclusi in una release futura.

### Hotfix

Un hotfix e' un caso speciale: un bug critico in produzione che non puo'
attendere il prossimo ciclo ordinario. Si realizza su un branch `hotfix/*`
(vedi arricchimento-git), bypassa il normale backlog, e produce una release
corretta direttamente su `main`.

La questione per un hotfix e' distinta dalle questioni del ciclo ordinario
e si chiude con la release del fix.

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
