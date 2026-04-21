---
tipo-artefatto: guida
documento: diagramma-fasi-p0-p4
descrizione: diagramma e riferimento visivo del percorso a fasi P0-P4
autorita: informativa
---

# Percorso P0-P4

Riferimento visivo: `../diagrams/fasi-p0-p4.puml`

Percorso di riferimento opzionale per opere che adottano un ciclo di vita a fasi
sequenziali. Non è obbligatorio attraversarle tutte: un'opera semplice può
partire direttamente da P2. Il percorso è un riferimento, non un vincolo.

---

## Fasi e approvazioni

| Fase | Nome | Scopo | Approvazione per procedere |
|---|---|---|---|
| P0 | Definizione | Capire il problema prima di qualsiasi soluzione | Si, prima di aprire P1 |
| P1 | Analisi | Tradurre obiettivi in specifiche realizzabili | Si (piano esecutivo), prima di aprire P2 |
| P2 | Realizzazione | Realizzare quanto pianificato, unità per unità | Per ogni unità: design prima delle iterazioni |
| P3 | Integrazione | Verificare il risultato nel suo insieme | Si, prima di aprire P4 |
| P4 | Consegna | Portare a destinazione una versione stabile | Si (approvazione consegna) |

---

## Artefatti attesi per fase

**P0** (`documenti/definizione/`)
- `1-obiettivi.md` — obiettivi misurabili, vincoli, stakeholder, criteri di successo
- `2-panoramica-funzionalita.md` — funzionalità in/out scope, priorità

**P1** (`documenti/analisi/`)
- `3-scenari.md` — scenari d'uso rilevanti
- `4-requisiti.md` — requisiti funzionali
- `5-vincoli.md` — requisiti non funzionali
- `6-struttura.md` — struttura del risultato atteso
- `7-piano-esecutivo.md` — unità di lavoro, ordine, milestone

**P2** (`documenti/unita/[nome]/`)
Per ogni unità:
- `design.md` — progettazione dettagliata (file singolo)
- `attivita.md` — iterazioni con obiettivi, voci di attività, note

Quando la complessità dell'unità lo richiede, il design può
articolarsi in una directory di documenti anziché in un file
singolo. La sezione "Design articolato per unità complesse"
descrive la struttura e le regole applicabili.

**P3** — nessuna directory propria; la verifica opera sugli artefatti delle fasi precedenti.

**P4** — verifiche finali, approvazione, consegna al destinatario.

---

## Ciclo per unità in P2

1. Design — progettazione dettagliata
2. Approvazione del design
3. Iterazioni — cicli brevi: pianifica / realizza / verifica / chiudi
4. Integrazione nell'aggregato o nell'opera

---

## Design articolato per unità complesse

Un'unità semplice usa un singolo `design.md` nella propria
directory. Un'unità complessa — con scenari d'uso multipli,
modelli dati articolati, transizioni di stato e vincoli di
dominio propri — può articolare il design in una directory di
documenti. La scelta tra le due forme è di chi governa l'unità,
in base alla profondità analitica necessaria.

### Struttura

```
documenti/unita/[nome-unita]/
  0-design.md       <- punto di ingresso e indice ragionato
  1-obiettivi.md    <- perché, scope, criteri di successo
  2-scenari.md      <- scenari d'uso del dominio
  3-requisiti.md    <- requisiti funzionali dell'unità
  4-vincoli.md      <- requisiti non funzionali, vincoli,
                       dipendenze dalla piattaforma
  5-struttura.md    <- architettura, modello dati,
                       transizioni di stato, integrazioni
  attivita.md       <- voci di attività (invariato)
```

### Convenzioni

- Il file `0-design.md` è il punto di ingresso che soddisfa la
  prescrizione del protocollo: è l'artefatto che viene prodotto,
  revisionato e approvato. Deve contenere le decisioni chiave e
  un indice ragionato che descriva il contenuto e la funzione di
  ciascun documento di approfondimento.
- I documenti da 1 a 5 sono articolazioni del design che
  sviluppano in profondità ciascun aspetto. Il prefisso numerico
  indica l'ordine di lettura, non l'ordine di produzione.
- La struttura rispecchia quella dei documenti di progetto
  (P0/P1) perché il lavoro analitico necessario ha la stessa
  forma a qualsiasi scala. I documenti di progetto descrivono la
  piattaforma a livello strategico; quelli dell'unità descrivono
  il dominio applicativo a livello operativo.
- Non tutti i documenti sono obbligatori: se un'unità non ha
  vincoli propri, il file `4-vincoli.md` non è necessario.
- Il file `attivita.md` non ha prefisso numerico perché non è
  un documento analitico ma lo strumento operativo che
  accompagna la realizzazione.

### Approvazione

L'approvazione di `0-design.md` copre l'intero pacchetto di
design. Non è necessaria un'approvazione esplicita per ciascun
documento di approfondimento: chi approva il punto di ingresso
approva il design nel suo insieme, compresi i documenti a cui
il punto di ingresso fa riferimento.

Chi governa l'approvazione può comunque richiedere revisioni su
documenti specifici prima di approvare il punto di ingresso.

---

## Regole

- Ogni fase si chiude con un'approvazione esplicita prima di procedere alla successiva. L'AI non avanza autonomamente.
- Rilievi e problemi inattesi vanno in questioni.md, non in attivita.md. L'attività è proattiva (nasce dalla pianificazione); la questione è reattiva (nasce da un problema).
- Questioni che emergono in P3 e invalidano assunzioni di fasi precedenti richiedono questioni collegate con propagazione a ritroso: si risolve dalla fase radice verso quella più avanzata.
- Per tracciare il ciclo in questioni.md: una questione di revisione per fase significativa, una per unità. I passi di esecuzione vivono in attivita.md, non come questioni separate.
