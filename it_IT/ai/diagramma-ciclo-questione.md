---
tipo-artefatto: guida
documento: diagramma-ciclo-questione
descrizione: diagramma e riferimento visivo del ciclo di vita di una questione
autorita: informativa
---

# Ciclo di vita di una questione

Riferimento visivo: `../diagrams/ciclo-questione.puml`

---

## Stati

- `open` — Creata, da analizzare
- `in-progress` — Analisi in corso
- `pending-approval` — Proposta redatta, in attesa di approvazione umana
- `pending-rfc` — RFC in corso: dall'invio fino all'avvio effettivo del
  lavoro da parte dell'attore ricevente
- `in-verification` — Risposta RFC ricevuta, verifica in corso
- `deferred` — Rimandato con motivazione esplicita
- `closed` — Risolto: rimosso da questioni.md, registrato in mastro.md

---

## Transizioni valide

- Da —:
  - → `open`: apertura questione
- Da `open`:
  - → `in-progress`: analisi avviata
  - → `deferred`: rimandato con motivazione
- Da `in-progress`:
  - → `pending-approval`: proposta redatta
  - → `pending-rfc`: richiede intervento esterno via RFC
  - → `deferred`: rimandato con motivazione
- Da `pending-approval`:
  - → `in-progress`: revisione richiesta dall'approvatore
  - → `closed`: approvato, precondizioni soddisfatte
- Da `pending-rfc`:
  - → `in-verification`: risposta RFC ricevuta
- Da `in-verification`:
  - → `open`: verifica completata
- Da `deferred`:
  - → `open`: ripreso

Transizioni non elencate non sono valide.

---

## Precondizioni per la chiusura

Condizione necessaria per qualsiasi questione: tutte le domande aperte sono risolte.

Condizione aggiuntiva per questioni di tipo **rilievo** con campo `Impatto` non vuoto:
il campo `Questioni collegate` deve contenere almeno una questione di tipo revisione
in stato aperto. La revisione non deve essere completata prima della chiusura del rilievo:
deve esistere, a testimonianza che il lavoro di applicazione è stato preso in carico.

Se la precondizione non è soddisfatta, la chiusura è bloccata.

---

## Regole operative

- Ogni cambio di stato richiede una nota nella sezione Storia che risponde al "perché", non al "cosa".
- Il tipo (rilievo / revisione / anomalia) è immutabile dopo l'apertura. Se la classificazione è errata, chiudere e riaprire con il tipo corretto.
- Un rilievo non può modificare artefatti nel corso del suo ciclo. Se durante l'analisi emerge una soluzione pronta, aprire una revisione e agire tramite essa.
- La motivazione nella Storia è obbligatoria per qualsiasi cambio di stato.
- Prima di chiudere: scrivere l'entry in mastro.md, poi rimuovere la questione da questioni.md. Mai nell'ordine inverso.
