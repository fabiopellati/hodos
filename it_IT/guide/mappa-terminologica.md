# Mappa Terminologica — Hodos

Tabella di conversione da termini software-specifici di playbook ai termini
astratti di opus. Guida la trasformazione di documenti e skills negli Step 3 e 4.

I termini non presenti in questa tabella sono già astratti e non richiedono
modifica.

---

## Fasi e ciclo di vita

| Termine playbook | Termine opus | Motivazione |
|---|---|---|
| `P2 — Development` | `P2 — Realizzazione` | Copre produzione di qualsiasi artefatto, non solo software |
| `sviluppo` | `realizzazione` | Idem |
| `implementare` | `realizzare` | Idem |
| `implementazione` | `realizzazione` | Idem |
| `P4 — Release` | `P4 — Consegna` | Release è termine software; consegna è universale |
| `portare in produzione` | `consegnare` | Idem |

---

## Struttura progetto

| Termine playbook | Termine opus | Motivazione |
|---|---|---|
| `componente` | `unità` | Neutro, applicabile a qualsiasi dominio |
| `modulo` | `aggregato` | Insieme di unità correlate, senza implicazioni tecniche |
| `epic` | `aggregato` | Allineato alla sostituzione di modulo |
| `bug` | `difetto` | Più generico, non implica software |

---

## Artefatti di analisi (P1)

| Termine playbook | Termine opus | Motivazione |
|---|---|---|
| `use-cases.md` | `scenari.md` | Scenari d'uso senza il gergo software |
| `specs-functional.md` | `requisiti.md` | Più generico di "functional specs" |
| `specs-non-functional.md` | `vincoli.md` | Vincoli non funzionali: performance, qualità, limiti |
| `architecture.md` | `struttura.md` | Struttura della soluzione, non architettura software |

---

## Git e infrastruttura di versionamento

Git è uno strumento di chi adotta Hodos, non un oggetto del suo dominio. Il
protocollo definisce le fasi in termini di processo puro (approvazione esplicita,
passaggio autorizzato). Come si materializza tecnicamente è una scelta
implementativa lasciata a chi adotta la metodologia.

I riferimenti a git vengono rimossi dal nucleo del protocollo e dai diagrammi.
Chi usa git trova la guida di integrazione nello skill `versionamento-git.md`
(arricchimento opzionale).

---

## Worklog

Il worklog è rendicontazione ex-post, non processo. Non appartiene al dominio
di opus. La skill worklog.md verrà rimossa da opus/code/ nello Step 4.

---

## Note

- I percorsi di file vanno aggiornati dove compare terminologia software:
  `components/` → `unità/`, `analysis/` → invariato.
