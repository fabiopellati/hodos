# Guida AI — Layer Claude sopra il Protocollo

Questa guida descrive come Claude applica il protocollo di processo definito
in `protocollo.md`. E' un layer opzionale: il processo e' applicabile
senza AI. Claude accelera l'esecuzione ma non sostituisce le decisioni umane.

---

## Principi operativi

**Il processo guida Claude, non viceversa.** Prima di qualsiasi azione,
Claude verifica lo stato corrente del progetto (questioni aperte, note attive,
CLAUDE.md), quale questione e' in corso e quale stato ha. Non chiude questioni
senza approvazione.

**Ogni artefatto rilevante passa per una questione.** La redazione di un documento,
la creazione di diagrammi, la scrittura di skill: ogni attivita' non banale
viene tracciata con una questione aperta prima di iniziare e portata a
`pending-approval` al completamento. L'umano approva esplicitamente.

**L'umano approva le approvazioni.** Claude non avanza da una fase alla successiva
autonomamente. Il superamento di un'approvazione richiede sempre conferma esplicita
dell'umano.

**I file di processo si aggiornano in tempo reale.** Quando una questione cambia
stato, quando viene chiusa, quando una entry va nel mastro: Claude aggiorna
i file immediatamente, non a fine sessione.

---

## Workflow tipico per un'attivita'

1. **Apri una questione** con `/questione` o manualmente, con stato `open`
2. **Aggiorna a `in-progress`** con `/aggiorna-questione` prima di iniziare
3. **Svolgi il lavoro**
4. **Aggiorna a `pending-approval`** al completamento
5. **Attendi l'approvazione umana** — non procedere oltre
6. **Alla conferma**: chiudi con `/aggiorna-questione` stato `closed` e scrivi nel mastro

---

## Gestione delle questioni

**Aprire**: usare `/questione`. Se il tipo (rilievo/revisione/anomalia)
o la descrizione non sono chiari dal contesto, chiedere prima di procedere.

**Aggiornare lo stato**: usare `/aggiorna-questione`. La motivazione del cambio
di stato e' sempre obbligatoria. Non cambiare stato senza nota nella Storia.

**Chiudere**: usare `/aggiorna-questione` con stato `closed`. Verificare che le
domande aperte siano tutte risolte prima di procedere. Lo skill scrive l'entry
nel mastro prima di rimuovere la questione da questioni.md.

**Propagazione a ritroso**: se una questione emerge in una fase avanzata e
invalida assunzioni di fasi precedenti, aprire questioni collegate nelle fasi
impattate. Indicare esplicitamente Fase di origine, Propagazione, Sintesi
e Questioni collegate. Risolvere dalla fase radice verso quella piu' avanzata.

---

## Gestione delle note

**Aprire una nota**: usare `/nota`. La nota viene scritta in `notes.md` con
identificativo univoco `NOTA-NNN`, descrizione sintetica e data. L'indice
viene aggiornato automaticamente.

**Quando usare una nota invece di una questione**: quando non c'e' ancora una
decisione da prendere, quando la decisione esiste ma il processo non e' nella
fase giusta, o come semplice memo. Se c'e' qualcosa da decidere ora, aprire
una questione.

**Archiviazione**: una nota puo' essere archiviata nel mastro e rimossa da
`notes.md` quando ha esaurito il suo scopo. Non ci sono vincoli su quando
o come farlo.

---

## Gestione delle RFC

**RFC outbound**: usare `/rfc` quando una questione richiede intervento esterno.
Il documento deve essere autocontenuto: verificare che un lettore esterno
possa capire richiesta e contesto senza conoscere il progetto.

**RFC inbound**: valutare la RFC ricevuta prima di aprire qualsiasi questione.
La valutazione determina fase e distribuzione del lavoro. La questione generata
segue il normale ciclo, inclusa la verifica di conformita' prima della chiusura.

---

## Glossario e terminologia

Usare sempre i termini definiti in `glossario.md`. Se durante la
redazione di un documento emerge un termine con valenza specifica non ancora
nel glossario, aggiungerlo immediatamente prima di continuare.

Non usare "nostro team" o "team esterno": usare Team-A e Team-B.
Non usare "append-only" per mastro.md: il termine corretto e' prepend-only.

---

## Cosa Claude non decide autonomamente

- Quale stato assegnare a un'approvazione (approvato / da rivedere)
- Se una questione puo' essere chiusa con domande ancora aperte
- Se avanzare alla fase successiva
- Se una RFC inbound va accettata, rifiutata o rimandata
