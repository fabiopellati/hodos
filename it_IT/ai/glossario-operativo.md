---
tipo-artefatto: guida
documento: glossario-operativo
descrizione: mappa i termini naturali dell'operatore alle operazioni del protocollo Hodos — ottimizzato per retrieval semantico
autorita: operativa
---

# Glossario Operativo — Riconoscimento Semantico per l'Agente AI

Questo glossario e' il punto di riferimento dell'agente AI per riconoscere
l'intenzione operativa dell'utente a partire da un prompt in linguaggio naturale.
Ogni voce associa un termine del protocollo Hodos ai sinonimi, alle varianti
colloquiali e alle espressioni che un operatore potrebbe usare per riferirsi
alla stessa operazione.

L'agente consulta questo glossario quando riceve un prompt che potrebbe
riferirsi a un'operazione Hodos. Il riconoscimento di un termine non autorizza
l'esecuzione automatica: attiva solo la richiesta di conferma all'operatore
(vedi regole-ingaggio.md).

---

## Questione

Termine del protocollo che indica un problema aperto da tracciare e risolvere.
La questione ha un ciclo di vita (apertura, analisi, approvazione, chiusura)
e tre tipi distinti.

**Espressioni che indicano l'apertura di una questione:**
apri una questione, nuova questione, c'e' un problema, ho trovato un problema,
segnalo un problema, devo tracciare, va tracciato, apri un ticket, registra
questo, tieni traccia, qualcosa non va, abbiamo un tema, serve una decisione,
dobbiamo decidere.

**Espressioni che indicano un aggiornamento di stato:**
aggiorna la questione, cambia stato, metti in progress, pronto per approvazione,
ho finito il lavoro, aspettiamo risposta, rimandiamo, parcheggia, rimandato,
sospendi, bloccato.

**Espressioni che indicano la chiusura:**
chiudi la questione, risolto, completato, fatto, possiamo chiudere, archivia,
questione risolta, deciso.

---

## Rilievo

Tipo di questione che porta conoscenza nuova — qualcosa che non si sapeva prima
e che modifica la comprensione del dominio. Il rilievo registra la scoperta ma
non agisce: se l'azione e' gia' chiara, serve una revisione.

**Espressioni che indicano un rilievo:**
rilievo, ho notato che, mi sono accorto che, emerge che, risulta che, scopro che,
non sapevamo che, nuova informazione, nuova conoscenza, finding, osservazione,
ho scoperto, attenzione a questo, importante sapere che, da considerare.

**Distinzione critica:** se l'operatore descrive un problema senza indicare
la soluzione, e' probabilmente un rilievo. Se descrive cosa fare per risolverlo,
e' probabilmente una revisione. In caso di dubbio, l'agente chiede.

---

## Revisione

Tipo di questione che corregge o affina un artefatto esistente. La soluzione e'
definita, l'artefatto da modificare e' identificato, manca l'esecuzione.

**Espressioni che indicano una revisione:**
revisione, correggi, modifica, aggiorna, va cambiato, va corretto, da rivedere,
fix, sistema questo, aggiungi al documento, togli dal documento, riformula,
riscrivi, integra, completa il documento, manca questo nel protocollo.

**Distinzione critica:** se l'operatore sa gia' cosa fare e su quale artefatto,
e' una revisione. Se ha identificato un problema ma la soluzione richiede
analisi, e' un rilievo.

---

## Anomalia

Tipo di questione che segnala un comportamento difforme da quanto atteso.
Non porta conoscenza nuova ne' corregge un artefatto: indica che qualcosa
non funziona come dovrebbe.

**Espressioni che indicano un'anomalia:**
anomalia, bug, non funziona, errore, malfunzionamento, dovrebbe fare X ma fa Y,
si e' rotto, non va, difetto, guasto, regressione, comportamento inatteso,
prima funzionava, non e' conforme.

---

## Nota

Osservazione, memo o idea registrata in notes.md. Non ha stati, non produce
entry nel mastro, non richiede approvazione. Serve per annotare informazioni
che non richiedono ancora una decisione.

**Espressioni che indicano una nota:**
nota, annotazione, memo, appunto, segna che, ricorda che, per memoria,
da tenere a mente, promemoria, idea, pensiero, spunto, segniamoci.

**Distinzione critica:** se c'e' qualcosa da decidere, non e' una nota ma una
questione. Se e' solo un'informazione da registrare senza azione, e' una nota.

---

## Commento

Contributo additivo e immutabile aggiunto a una questione o a una nota gia'
esistente. Serve a rettificare, integrare o contestualizzare senza modificare
il corpo originale.

**Espressioni che indicano un commento:**
aggiungi un commento, nota aggiuntiva, integrazione, rettifica, preciso che,
correggo il commento, a proposito di, aggiunta, aggiorno, specifico meglio.

---

## Inizializzazione

Creazione dello scaffolding di un'opera Hodos: CLAUDE.md, questioni.md,
mastro.md, notes.md.

**Espressioni che indicano inizializzazione:**
inizializza hodos, crea il progetto, setup, prepara i file, scaffolding,
bootstrap, avvia l'opera, parti con hodos, nuovo progetto hodos.

---

## RFC

Documento formale per comunicare con un team esterno quando una questione
non puo' essere risolta internamente.

**Espressioni che indicano una RFC:**
manda una rfc, richiesta esterna, serve il team esterno, dobbiamo chiedere a,
richiesta di modifica, coinvolgi il team, invia la richiesta.

---

## Mastro

Registro immutabile delle decisioni prese. L'operatore non interagisce
direttamente col mastro: le entry vengono scritte automaticamente alla
chiusura di una questione.

**Espressioni che indicano consultazione del mastro:**
cosa abbiamo deciso, decisioni prese, storico, registro, che fine ha fatto,
quando abbiamo chiuso, riassunto delle decisioni.

---

## Segnali di ambiguita'

Queste espressioni sono troppo generiche per essere associate a un'operazione
specifica. L'agente non deve operare sui file di processo ma deve chiedere
chiarimento.

**Espressioni ambigue:**
registra questo, traccia questo, salva, documenta, gestisci, occupati di,
fai qualcosa, sistema.

L'agente chiede: "Vuoi aprire una questione, aggiungere una nota, o e'
solo un'osservazione?"
