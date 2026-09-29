---
tipo-artefatto: guida
documento: glossario
descrizione: termini del protocollo Hodos in ordine alfabetico, ciascuno introdotto nel punto
  in cui il protocollo lo nomina per la prima volta
---

# Glossario — Hodos

**Versione**: bozza (in redazione parallela al protocollo)

I termini sono in ordine alfabetico. Ogni termine compare qui nel momento in
cui viene introdotto per la prima volta nel protocollo.

---

## Termini

**Artefatti di Hodos**
I documenti consegnabili della metodologia, classificati in tre livelli gerarchici.
Livello primario: `protocollo.md` — normativo, per umano non tecnico. Livello
secondario: `guide/` — operativo, per umano che applica il processo. Livello
terziario: skills in `skills/` — procedurale, per agente esecutore (AI); formulati
per efficacia ed efficienza del modello, autocontenuti. Distinti dai documenti
di stato dell'opera (`questioni.md`, `mastro.md`, `note.md`) che sono strumenti
di governo del processo, non artefatti distribuibili.

**Team-A**
Il team interno che gestisce il progetto e le sue questioni. Nei diagrammi e nel
protocollo, Team-A è sempre il soggetto attivo: apre questioni, genera RFC
outbound, riceve e valuta RFC inbound, verifica il lavoro esterno.

**Team-B**
Un team esterno che gestisce un sistema correlato. Nei diagrammi e nel protocollo,
Team-B è il destinatario di una RFC outbound o il mittente di una RFC inbound.
Team-B non partecipa al processo interno di Team-A: interagisce solo attraverso
il documento RFC.

**Commento**
Contributo additivo e immutabile aggiunto a una questione o a una nota dopo
la sua creazione. Serve a rettificare, integrare o contestualizzare il
contenuto originale senza modificarlo. Ogni commento è numerato localmente
all'artefatto a cui appartiene (COMMENTO-001, COMMENTO-002, ...) e reca la
data di inserimento. Non modifica lo stato né il corpo dell'artefatto a cui
si riferisce.

**Anomalia**
Tipo di questione che segnala un comportamento o risultato difforme da quanto
atteso. Distinto da *rilievo* e *revisione*: non porta conoscenza nuova né
corregge un artefatto, ma indica che qualcosa non funziona come dovrebbe.

**Artefatto consolidato**
Documento che rappresenta lo stato corrente della verità in una fase. Viene
aggiornato in-place durante i cicli di affinamento. Distinto da `questioni.md` e
`mastro.md` che sono strumenti di governo del processo.

**Rilievo**
Tipo di questione che porta conoscenza nuova — non nota prima dell'analisi — che
modifica o arricchisce la comprensione del dominio. Distinto da *revisione*.
Quando il campo `Impatto` non è vuoto, il rilievo non può essere chiuso senza
almeno una questione di *revisione* aperta che lo dichiari nel proprio campo
`related` (vedi *related*).

Criterio di scelta: aprire un rilievo quando si è identificato qualcosa di
rilevante ma non si è ancora pronti ad agire — perché serve analisi, perché
la soluzione non è chiara, o perché la decisione spetta a qualcun altro.
Esempio: durante l'analisi emerge che un requisito contraddice un vincolo già
documentato. Il problema è chiaro, ma la direzione da prendere no — rilievo.
Se invece la direzione è chiara e si è pronti ad agire, aprire una *revisione*.

**Questione**
Problema aperto che deve essere risolto prima di procedere. Può essere di
natura *rilievo*, *revisione* o *anomalia*. Vive nel proprio file della
collezione `questioni/` finché non viene chiusa; alla chiusura il file viene
spostato nella collezione `mastro/`, e i due indici derivati si rigenerano.

**related**
Campo opzionale del frontmatter di un elemento, che elenca i riferimenti agli
altri elementi correlati della medesima opera. Sostituisce la sezione
«Questioni collegate» che il corpo portava nelle versioni anteriori alla 1.0.0.

Il legame si dichiara una volta sola, sull'elemento che lo origina, e le
back-reference sono derivate dallo strumento e non si scrivono a mano
(Art. 3 comma 6). Ne discende la direzione dell'obbligo nel caso del rilievo
con `Impatto` non vuoto: è la questione di *revisione* a dover dichiarare il
rilievo nel proprio `related` prima che il rilievo possa essere chiuso, non il
rilievo a elencare la revisione (Art. 9 comma 2).

Il perimetro del campo è locale all'opera: il legame verso un'altra opera si
scrive in prosa nel corpo dell'elemento che lo origina.

**Nota**
Osservazione, memo o idea in incubazione, che vive nel proprio file della
collezione `note/` ed è sommariata dall'indice derivato `note.md`. Non è una
questione: non ha stati, non produce una entry nel mastro, non richiede
approvazione. Il corpo è immutabile dopo la scrittura. Può ricevere commenti
(COMMENTO-NNN) per rettifiche o nuove conoscenze sullo stesso argomento, senza
dover aprire una nota separata.

**mastro.md**
Indice derivato della collezione `mastro/`, il registro delle decisioni prese,
che contiene solo cicli chiusi. Ne offre il sommario cronologico decrescente:
le voci più recenti stanno in cima. Come gli altri indici si rigenera dai
frontmatter e non si mantiene a mano.

La voce del mastro ha un **doppio regime** (Art. 6 comma 7 e Art. 10): il corpo
markdown è immutabile e non si tocca dopo la scrittura, perché è la
testimonianza storica della decisione; il frontmatter è mutabile e si corregge
per sanare un disallineamento, per affinare i campi di giudizio (`decisioni`,
`related`, `tag`) o nel corso di una bonifica di versione.

**questioni.md**
Indice derivato della collezione `questioni/`, che riporta identificativo,
titolo e stato corrente di ogni questione presente, in ordine decrescente per
identificativo (Art. 4 commi 3 e 4). Non è la sorgente delle questioni — la
sorgente è il singolo file `questioni/Q{NNN}-slug.md` — e non si mantiene a
mano: si rigenera dai frontmatter.

Le questioni chiuse non vi compaiono perché il loro file esce dalla collezione
per andare in `mastro/` (Art. 4 comma 1), e non perché l'indice filtri sullo
stato: il campo `stato` serve a distinguere gli stati che nella collezione
convivono, da `open` a `in-progress`, `pending-approval` e `deferred`.

**Opera**
Istanza di lavoro organizzato che adotta Hodos come metodologia di processo.
Un'opera ha una durata definita, produce elaborati propri (in `documenti/`) e
mantiene tre strumenti di governo trasversali: `questioni.md`, `mastro.md` e
`note.md`. Il termine designa il lavoro nella sua interezza — indipendentemente
dal dominio, dalla tecnologia o dalla dimensione. Radice latina *opus* (lavoro,
creazione): neutro rispetto ai domini e ai contesti in cui Hodos viene adottato.

**Prepend-only**
Modalità di inserimento in cui ogni nuova entry viene inserita prima delle
entry esistenti dello stesso tipo, mantenendo l'ordine decrescente per data.
Il prepend riguarda l'ordine tra le entry: le sezioni strutturali del documento
(intestazione, indice, note a piè) restano nelle loro posizioni. Usato per
`mastro.md` e `questioni.md`. Equivalente funzionale di *append-only* con
ordine invertito.

**Revisione**
Tipo di questione che corregge o affina un artefatto esistente. Distinta da
*rilievo*, che porta conoscenza nuova.

Criterio di scelta: aprire una revisione quando si sa già cosa fare e si è
pronti ad agire — la soluzione è definita, l'artefatto da modificare è
identificato, manca solo l'esecuzione.
Esempio: si decide di aggiungere una voce al glossario perché un termine è
usato nel protocollo senza essere definito. L'azione è chiara — revisione.

**RFC (Request for Change)**
Documento formale generato quando una questione richiede intervento su un sistema
o team esterno. Autocontenuto e bidirezionale: include una sezione Response RFC
compilata dal team ricevente. Può essere *outbound* (generata dal nostro team)
o *inbound* (ricevuta da un team esterno).

**RFC inbound**
RFC ricevuta da un team esterno che richiede intervento nel sistema di Team-A.
Prima di aprire una questione, la RFC viene valutata dal team per determinare
fase e distribuzione del lavoro.

**RFC outbound**
RFC generata da Team-A verso un sistema o team esterno, originata da una
questione interna che non può essere risolta senza intervento esterno.

**Response RFC**
Sezione della RFC compilata dal team ricevente al completamento del lavoro.
Contiene: decisione presa, descrizione di quanto realizzato, eventuali
deviazioni dalla request originale.


