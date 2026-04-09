# Principi Guida — Hodos

Questo documento descrive i valori fondamentali su cui Hodos è costruita.
Non è una guida operativa: è il "perché" della metodologia. Leggerlo aiuta
a capire le scelte progettuali di Hodos e a valutare se è adatta al proprio
contesto prima di adottarla.

---

## Semplicità

Un processo deve essere comprensibile e applicabile senza formazione specialistica.
Ogni meccanismo che non porta valore misurabile è un peso, non una garanzia.

Hodos non mira a essere completo né potente: mira a essere il minimo necessario
per lavorare in modo tracciabile e governato. Quando una funzionalità è
in discussione, la domanda non è "potrebbe servire?" ma "serve ora, in modo
misurabile?".

Criterio di adozione: comprendere i principi guida dovrebbe essere sufficiente
per cogliere la logica della metodologia. Apprendere il protocollo non richiede
sforzo eccessivo: dopo un warmup proporzionato — leggere il protocollo, applicarlo
a un caso concreto — un operatore dovrebbe essere in grado di usare Hodos tanto
su opere elementari quanto su processi ad alto grado di complessità, ricavandone
valore in entrambi i casi.

## Adattabilità

Il nucleo del processo deve potersi calare in contesti diversi senza modifiche
strutturali. Le varianti dipendenti dal dominio, dagli strumenti o dalle
preferenze del team sono arricchimenti opzionali, non requisiti.

Hodos separa esplicitamente il nucleo obbligatorio dagli arricchimenti: il
percorso a fasi P0-P4, l'integrazione con git, le automazioni AI — sono tutti
strati aggiuntivi che non condizionano il funzionamento del processo base.

Criterio di adozione: se adottare Hodos richiede di cambiare il proprio dominio
o i propri strumenti, il problema non è Hodos — è che l'arricchimento scelto
non è quello giusto. Il nucleo si adatta; gli arricchimenti si scelgono.

## Indipendenza dal Dominio

Hodos è progettata per funzionare allo stesso modo in un'opera editoriale,
in un processo legislativo, in un progetto artigianale o in un contesto software.
Non assume nulla sul tipo di artefatto prodotto né sul dominio di applicazione.

Questa indipendenza non è neutralità: è una scelta progettuale precisa.
Ogni termine tecnico legato a un dominio specifico è una barriera all'adozione
in altri contesti. Hodos usa un vocabolario astratto proprio per questo.

Criterio di adozione: se il protocollo Hodos può essere letto da un professionista
non tecnico senza incontrare termini che richiamano esclusivamente un altro
contesto, il principio è rispettato.

## Neutralità Strumentale

Hodos è applicabile con soli strumenti tradizionali — carta, penna, file di
testo. L'uso di strumenti digitali, automazioni o intelligenza artificiale
è un'accelerazione opzionale, non un prerequisito.

Questo principio garantisce che la metodologia non dipenda dalla disponibilità
di tecnologie specifiche o dalla volontà di adottarle. Un team può scegliere
di usare Hodos con strumenti minimi e poi aggiungere automazioni quando e se
ha senso farlo. Gli strumenti arricchiscono Hodos — la accelerano, la rendono
più efficiente, ne ampliano le possibilità — senza modificarne l'essenza
né condizionarne il funzionamento.

Criterio di adozione: se Hodos non funziona senza uno strumento specifico,
il principio è violato. La scelta degli strumenti deve restare libera
e reversibile in qualsiasi momento.

## Univocità Terminologica

Ogni termine usato nel processo ha un significato preciso e stabile. Un termine
non assume valenze diverse a seconda della fase, del contesto o dell'interlocutore.
Quando si introduce un termine nuovo, va definito esplicitamente nel glossario.

L'ambiguità terminologica è una delle cause più frequenti di incomprensioni
nei processi collaborativi. Hodos la tratta come un problema da eliminare, non
da tollerare. Il glossario non è un accessorio: è parte integrante del processo.

Criterio di adozione: se due persone usano lo stesso termine con significati
diversi senza accorgersene, il processo non può funzionare in modo affidabile.
Hodos è adatta a contesti dove c'è disponibilità a costruire e rispettare
un vocabolario condiviso.

## Approvazioni Esplicite

Ogni ciclo rilevante richiede approvazione esplicita di chi governa prima di
avanzare. Il processo non avanza autonomamente: chi detiene l'autorità
decisionale deve confermare prima che il lavoro prosegua.

Questo principio protegge da due rischi opposti: l'inerzia (nessuno decide
e il lavoro si blocca) e la deriva (il lavoro avanza senza controllo e si
allontana dagli obiettivi). L'approvazione esplicita è il momento in cui
chi governa esercita la sua responsabilità.

Come si materializza operativamente l'approvazione, o chi ne sia responsabile,
è una scelta lasciata a chi adotta la metodologia: puo essere in capo ad una o più persone ed essere espressa con una firma, un messaggio, una riunione o
qualsiasi altro atto riconoscibile come deliberato.

Hodos può essere adottata anche da chi lavora da solo: in quel caso, chi governa
e chi realizza coincidono nella stessa persona. L'approvazione esplicita diventa
un atto deliberato di autogoverno — un momento di verifica consapevole prima di
procedere, che distingue il lavoro guidato dall'accumulo non governato.

Criterio di adozione: Hodos è adatta a contesti dove chi governa è disponibile
a partecipare attivamente al processo, non solo a riceverne i risultati. Questo
vale tanto per un team quanto per chi lavora in autonomia.

## Tracciabilità delle Decisioni

Ogni scelta non ovvia va documentata con la motivazione e le alternative
considerate. Il valore della tracciabilità non è burocratico: è la possibilità
di capire — anche quando il tempo avrà invecchiato la memoria — perché si è
scelto in un certo modo, e di valutare se quella scelta regge ancora alla luce di nuove informazioni.

Il mastro è lo strumento principale di tracciabilità in Hodos: registro
immutabile delle decisioni prese, con motivazione e impatto. Non viene mai
modificato: ogni nuova entry si aggiunge in cima, preservando la storia
completa del processo.

Criterio di adozione: se un team non è disposto a documentare le proprie
decisioni, Hodos non aggiunge valore — il processo diventerebbe solo un peso
formale senza il beneficio della memoria collettiva.

---

> I termini con valenza specifica in questo documento sono definiti in
> `guide/glossario.md`.
