---
tipo-artefatto: guida
documento: glossario-fasi
descrizione: termini introdotti dall'arricchimento fasi P0-P4
autorita: informativa
arricchimento: fasi
---

# Glossario — Arricchimento Fasi

Termini introdotti dal percorso P0-P4 e dalla fase di
realizzazione P2. Integrano il glossario del protocollo
base quando l'arricchimento fasi è abilitato nell'opera.

---

## Termini

**Aggregato**
Raggruppamento di unità per correlazione forte in P2.
Le unità dentro un aggregato hanno una relazione
semantica più stretta tra loro che con il resto
dell'opera, ma questo non esclude relazioni con unità
di altri aggregati o con unità isolate. Un aggregato
contiene unità, mai altri aggregati. Il valore è
organizzativo e di navigazione, non un confine rigido
di isolamento.

**Approvazione**
Punto di approvazione esplicita tra una fase e la
successiva. Il passaggio alla fase successiva non può
avvenire senza che l'approvazione sia stata ottenuta.
Come si materializza operativamente è una scelta
lasciata a chi adotta la metodologia.

**Artefatto consolidato**
Documento che rappresenta lo stato corrente della
verità in una fase. Viene aggiornato in-place durante
i cicli di affinamento. Distinto da `questioni.md` e
`mastro.md` che sono strumenti di governo del processo.

**Conformità** (attività)
Verifica che quanto realizzato soddisfi la richiesta
originale della voce di attività. Valutata rispetto ai
Criteri di verifica definiti all'apertura. Può essere:
conforme, parziale (con motivazione degli scostamenti),
non conforme (con motivazione).

**Design articolato**
Modalità di strutturazione del design di un'unità
complessa in P2, alternativa al singolo `1-design.md`.
Il design si articola in una directory di documenti con
un punto di ingresso (`0-design.md`) e documenti di
approfondimento numerati (`1-obiettivi.md`,
`2-scenari.md`, `3-requisiti.md`, `4-vincoli.md`,
`5-struttura.md`). La struttura rispecchia quella dei
documenti di progetto (P0/P1) applicata alla scala
dell'unità. L'approvazione del punto di ingresso copre
l'intero pacchetto. La scelta tra design semplice e
articolato è di chi governa l'unità.

**Evoluzione**
Artefatto che documenta il passaggio da uno stato del
design a un altro per un'unità matura in P2. Descrive
il delta (cosa cambia e perché), viene approvata prima
della realizzazione e resta nella directory dell'unità
come documento storico congelato. Il file si chiama
`EVO-{N}-{titolo}.md` con numerazione progressiva
locale all'unità. Le modifiche minori (entro i pattern
esistenti) non richiedono un'evoluzione e si gestiscono
con un BL in `2-attivita.md`.

**Fase**
Periodo del ciclo di lavoro con scopo, artefatti e
approvazione definiti. Hodos non prescrive fasi
obbligatorie: il percorso P0-P4 è un arricchimento
opzionale descritto nello skill `arricchimento-fasi`.

**Iterazione**
Ciclo breve di realizzazione all'interno di P2 per una
singola unità. Segue il pattern: pianifica / realizza /
verifica / chiudi. Ogni iterazione ha obiettivi definiti
e si chiude con una verifica di quanto consegnato. Le
iterazioni sono tracciate nel `2-attivita.md`
dell'unità.

**Parte**
Elemento della struttura del risultato atteso. Le parti
emergono dalle decisioni strutturali (DST) registrate
in `6-struttura.md` e descrivono *cosa* compone
l'opera. Sono distinte dalle unità, che descrivono
*come* l'opera si realizza. La corrispondenza fra
parti e unità è scelta di chi governa l'opera: può
essere uno-a-uno, molti-a-molti o mista, secondo
quanto risulta più adatto al dominio. Equivalente
astratto della parte architetturale (o del componente
strutturale) nel contesto software.

**Propagazione a ritroso**
Meccanismo per cui una questione emersa in una fase
avanzata invalida assunzioni di fasi precedenti,
generando questioni collegate nelle fasi impattate. Le
questioni propagate sono collegate esplicitamente alla
questione di origine.

**Unità**
Pacchetto di lavoro con design proprio e ciclo di
iterazioni in P2. Distinta dalla *parte*, che descrive
la struttura del risultato: l'unità descrive *come*
si realizza una porzione dell'opera, non *cosa* la
compone. Una unità può raggruppare la realizzazione di
una o più parti, una parte può essere realizzata da
una o più unità, e la cardinalità è scelta di chi
governa. Una unità può essere raggruppata in un
aggregato. Equivalente astratto del pacchetto di
lavoro (o del componente di realizzazione) nel
contesto software. Un'unità semplice usa un singolo
`1-design.md`; un'unità complessa può usare un
*design articolato* con più documenti di
approfondimento.

**Voce di attività**
Unità di lavoro pianificata in P2 per la realizzazione
di un'unità. Funziona come contratto in due tempi:
all'apertura definisce la richiesta e i criteri di
verifica; alla chiusura documenta la consegna e la
conformità rispetto alla richiesta originale. Distinta
dalla questione, che è reattiva; la voce di attività è
proattiva — nasce dalla pianificazione, non da un
problema.
