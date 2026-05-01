# Mappa Terminologica — Hodos

Tabella di conversione da termini software-specifici di playbook ai termini
astratti di opus. Guida la trasformazione di documenti e skills negli Step 3 e 4.

I termini non presenti in questa tabella sono già astratti e non richiedono
modifica.

---

## Fasi e ciclo di vita

- `P2 — Development` → `P2 — Realizzazione`: copre produzione di
  qualsiasi artefatto, non solo software
- `sviluppo` → `realizzazione`: idem
- `implementare` → `realizzare`: idem
- `implementazione` → `realizzazione`: idem
- `P4 — Release` → `P4 — Consegna`: Release è termine software;
  consegna è universale
- `portare in produzione` → `consegnare`: idem

---

## Struttura progetto

- `componente` (struttura) → `parte`: elemento della struttura del
  risultato atteso
- `componente` (lavoro) → `unità`: pacchetto di lavoro con design
  proprio e ciclo di iterazioni
- `modulo` → `aggregato`: insieme di unità correlate, senza
  implicazioni tecniche
- `epic` → `aggregato`: allineato alla sostituzione di modulo
- `bug` → `difetto`: più generico, non implica software

Il termine playbook `componente` porta due accezioni distinte che
nel lessico di opus vengono rese da due termini diversi. La
**parte** è un elemento della struttura del risultato (che cosa
compone l'opera) e si registra in `6-struttura.md` attraverso le
decisioni strutturali (DST). L'**unità** è un pacchetto di lavoro
per la realizzazione (come si costruisce l'opera) e si pianifica
in `7-piano-esecutivo.md` per essere realizzata in P2. Le due
viste sono distinte e la cardinalità della relazione fra parti e
unità è scelta di chi governa l'opera.

---

## Artefatti di analisi (P1)

- `use-cases.md` → `scenari.md`: scenari d'uso senza il gergo software
- `specs-functional.md` → `requisiti.md`: più generico di "functional
  specs"
- `specs-non-functional.md` → `vincoli.md`: vincoli non funzionali,
  performance, qualità, limiti
- `architecture.md` → `struttura.md`: struttura della soluzione, non
  architettura software

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
