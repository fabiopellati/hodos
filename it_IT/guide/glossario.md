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
di stato dell'opera (`questioni.md`, `mastro.md`, `notes.md`) che sono strumenti
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

**Aggregato**
Insieme di unità correlate che condividono un obiettivo comune in P2. Può
contenere più unità ma non altri aggregati. Equivalente astratto di modulo
o epic nel contesto software.

**Voce di attività**
Unità di lavoro pianificata in P2 per la realizzazione di un'unità.
Funziona come contratto in due tempi: all'apertura definisce la richiesta e
i criteri di verifica; alla chiusura documenta la consegna e la conformità
rispetto alla richiesta originale. Distinta dalla questione, che è reattiva;
la voce di attività è proattiva — nasce dalla pianificazione, non da un problema.

**Conformità** (attività)
Verifica che quanto realizzato soddisfi la richiesta originale della voce di
attività. Valutata rispetto ai Criteri di verifica definiti all'apertura. Può
essere: conforme, parziale (con motivazione degli scostamenti), non conforme
(con motivazione).

**Artefatto consolidato**
Documento che rappresenta lo stato corrente della verità in una fase. Viene
aggiornato in-place durante i cicli di affinamento. Distinto da `questioni.md` e
`mastro.md` che sono strumenti di governo del processo.

**Iterazione**
Ciclo breve di realizzazione all'interno di P2 per una singola unità.
Segue il pattern: pianifica / realizza / verifica / chiudi. Ogni iterazione
ha obiettivi definiti e si chiude con una verifica di quanto consegnato.
Le iterazioni sono tracciate nell'attivita.md dell'unità.

**Rilievo**
Tipo di questione che porta conoscenza nuova — non nota prima dell'analisi — che
modifica o arricchisce la comprensione del dominio. Distinto da *revisione*.
Quando il campo `Impatto` non è vuoto, il rilievo non può essere chiuso senza
almeno una questione di *revisione* collegata aperta (vedi *Questioni collegate*).

Criterio di scelta: aprire un rilievo quando si è identificato qualcosa di
rilevante ma non si è ancora pronti ad agire — perché serve analisi, perché
la soluzione non è chiara, o perché la decisione spetta a qualcun altro.
Esempio: durante l'analisi emerge che un requisito contraddice un vincolo già
documentato. Il problema è chiaro, ma la direzione da prendere no — rilievo.
Se invece la direzione è chiara e si è pronti ad agire, aprire una *revisione*.

**Approvazione**
Punto di approvazione esplicita tra una fase e la successiva. Il passaggio
alla fase successiva non può avvenire senza che l'approvazione sia stata
ottenuta. Come si materializza operativamente è una scelta lasciata a chi
adotta la metodologia.

**Questione**
Problema aperto che deve essere risolto prima di procedere. Può essere di
natura *rilievo*, *revisione* o *anomalia*. Vive in `questioni.md` finché non
viene chiusa; alla chiusura viene rimossa e la risoluzione registrata in
`mastro.md`.

**Questioni collegate**
Campo opzionale di una questione che elenca i riferimenti ad altre questioni
correlate. Diventa obbligatorio per le questioni di tipo *rilievo* con campo
`Impatto` non vuoto: in quel caso deve contenere almeno un riferimento a una
questione di tipo *revisione* aperta prima che il rilievo possa essere chiuso.

**Nota**
Osservazione, memo o idea in incubazione registrata in `notes.md`. Non è una
questione: non ha stati, non produce una entry nel mastro, non richiede
approvazione. Il corpo è immutabile dopo la scrittura. Può ricevere commenti
(COMMENTO-NNN) per rettifiche o nuove conoscenze sullo stesso argomento, senza
dover aprire una nota separata.

**mastro.md**
Registro immutabile delle decisioni prese. Contiene solo cicli chiusi.
Ordine decrescente (prepend-only): le entry più recenti stanno in cima.
Una entry non viene mai modificata dopo la scrittura.

**questioni.md**
Documento che contiene le questioni aperte di una fase. Ordine decrescente e
immutabile dopo la creazione. Include una sezione di intestazione con l'indice
e lo stato corrente di ogni questione. Quando una questione viene chiusa, viene
rimossa dal file.

**Fase**
Periodo del ciclo di lavoro con scopo, artefatti e approvazione definiti. Hodos
non prescrive fasi obbligatorie: il percorso P0-P4 è un arricchimento opzionale
descritto nello skill `arricchimento-fasi.md`.

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

**Propagazione a ritroso**
Meccanismo per cui una questione emersa in una fase avanzata invalida assunzioni
di fasi precedenti, generando questioni collegate nelle fasi impattate. Le
questioni propagate sono collegate esplicitamente alla questione di origine.

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

**Unità**
Elemento atomico di realizzazione in P2. Ha un design proprio, un'attività
e un ciclo di iterazioni. Può essere raggruppata in un aggregato. Equivalente
astratto di componente nel contesto software.
