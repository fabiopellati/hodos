---
tipo-artefatto: guida
documento: diagramma-fasi-p0-p4
descrizione: diagramma e riferimento visivo del percorso a fasi P0-P4
autorita: informativa
---

# Percorso P0-P4

Riferimento visivo: `../diagrams/fasi-p0-p4.puml`

Percorso di riferimento opzionale per opere che adottano un ciclo di vita a fasi
sequenziali. Non e' obbligatorio attraversarle tutte: un'opera semplice puo'
partire direttamente da P2. Il percorso e' un riferimento, non un vincolo.

---

## Fasi e approvazioni

| Fase | Nome | Scopo | Approvazione per procedere |
|---|---|---|---|
| P0 | Definizione | Capire il problema prima di qualsiasi soluzione | Si, prima di aprire P1 |
| P1 | Analisi | Tradurre obiettivi in specifiche realizzabili | Si (piano esecutivo), prima di aprire P2 |
| P2 | Realizzazione | Realizzare quanto pianificato, unita' per unita' | Per ogni unita': design prima delle iterazioni |
| P3 | Integrazione | Verificare il risultato nel suo insieme | Si, prima di aprire P4 |
| P4 | Consegna | Portare a destinazione una versione stabile | Si (approvazione consegna) |

---

## Artefatti attesi per fase

**P0** (`documenti/definizione/`)
- `1-obiettivi.md` — obiettivi misurabili, vincoli, stakeholder, criteri di successo
- `2-panoramica-funzionalita.md` — funzionalita' in/out scope, priorita'

**P1** (`documenti/analisi/`)
- `3-scenari.md` — scenari d'uso rilevanti
- `4-requisiti.md` — requisiti funzionali
- `5-vincoli.md` — requisiti non funzionali
- `6-struttura.md` — struttura del risultato atteso
- `7-piano-esecutivo.md` — unita' di lavoro, ordine, milestone

**P2** (`documenti/unita/[nome]/`)
Per ogni unita':
- `design.md` — progettazione dettagliata
- `attivita.md` — iterazioni con obiettivi, voci di attivita', note

**P3** — nessuna directory propria; la verifica opera sugli artefatti delle fasi precedenti.

**P4** — verifiche finali, approvazione, consegna al destinatario.

---

## Ciclo per unita' in P2

1. Design — progettazione dettagliata
2. Approvazione del design
3. Iterazioni — cicli brevi: pianifica / realizza / verifica / chiudi
4. Integrazione nell'aggregato o nell'opera

---

## Regole

- Ogni fase si chiude con un'approvazione esplicita prima di procedere alla successiva. L'AI non avanza autonomamente.
- Rilievi e problemi inattesi vanno in questioni.md, non in attivita.md. L'attivita' e' proattiva (nasce dalla pianificazione); la questione e' reattiva (nasce da un problema).
- Questioni che emergono in P3 e invalidano assunzioni di fasi precedenti richiedono questioni collegate con propagazione a ritroso: si risolve dalla fase radice verso quella piu' avanzata.
- Per tracciare il ciclo in questioni.md: una questione di revisione per fase significativa, una per unita'. I passi di esecuzione vivono in attivita.md, non come questioni separate.
