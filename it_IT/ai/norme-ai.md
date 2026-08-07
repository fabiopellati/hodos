---
tipo-artefatto: guida
documento: norme-ai
descrizione: norme vincolanti per l'agente AI che opera in un'opera Hodos — derivate dal protocollo
autorita: normativa
---

# Norme AI — Vincoli protocollari per l'agente

Queste norme derivano dal protocollo Hodos e hanno valore vincolante. In caso
di conflitto con istruzioni operative o arricchimenti opzionali, queste norme
prevalgono.

---

## Principi operativi

**Il processo guida l'agente, non viceversa.** Prima di qualsiasi azione,
l'agente verifica lo stato corrente del progetto (questioni aperte, note attive,
CLAUDE.md), quale questione è in corso e quale stato ha. Non chiude questioni
senza approvazione.

**Ogni artefatto rilevante passa per una questione.** La redazione di un documento,
la creazione di diagrammi, la scrittura di skill: ogni attività non banale
viene tracciata con una questione aperta prima di iniziare e portata a
`pending-approval` al completamento. L'umano approva esplicitamente.

**L'umano approva le approvazioni.** L'agente non avanza da una fase alla
successiva autonomamente. Il superamento di un'approvazione richiede sempre
conferma esplicita dell'umano.

**I file di processo si aggiornano in tempo reale.** Quando una questione cambia
stato, quando viene chiusa, quando una voce va nel mastro: l'agente aggiorna
i file immediatamente, non a fine sessione. Dopo aver modificato un file-elemento
in `questioni/`, `note/` o `mastro/`, l'agente rigenera l'indice corrispondente.

---

## Forma segregata: indici derivati e doppio regime del mastro

Gli strumenti di governo sono collezioni segregate: una cartella
(`questioni/`, `note/`, `mastro/`) con un file per elemento, più un indice
(`questioni.md`, `note.md`, `mastro.md`) che è proiezione derivata dei
frontmatter. Ne discendono due vincoli.

**Gli indici non si modificano a mano.** L'indice è generato dai frontmatter
degli elementi. L'agente non scrive né corregge l'indice direttamente: modifica
il file-elemento e poi rigenera l'indice con lo strumento dell'opera. Scrivere a
mano nell'indice introduce una seconda sorgente divergente, che è esattamente
ciò che la forma segregata elimina.

**Il mastro ha un doppio regime.** Nei file di `mastro/` il corpo markdown è
immutabile — testimonianza storica della decisione, mai modificata dopo la
scrittura — mentre il frontmatter è mutabile, per sanare disallineamenti,
affinare i campi di giudizio (`decisioni`, `related`, `tag`) o eseguire una
bonifica di versione. Cambiare una decisione non si fa mai correggendo il corpo
di una voce esistente: si apre una nuova questione.

---

## La questione aperta è un documento di lavoro

**Hodos non è esclusivamente additivo.** Il protocollo concede l'immutabilità
del corpo in modo esplicito e solo dove la vuole: alla nota (Art. 5 comma 5) e
alla voce del mastro (Art. 6 comma 7 e Art. 10 comma 1). Sulla questione vincola
per addizione i soli campi `Domande aperte` e `Impatto` (Art. 4 comma 6), e tace
sul resto del corpo. Finché la questione non è chiusa il suo corpo è quindi
modificabile, e l'agente non deve trattarlo come intoccabile.

**Preferire il consolidamento all'accumulo.** Quando una rettifica renderebbe la
questione più chiara, più ordinata e più concreta, l'agente consolida il corpo
invece di aggiungere l'ennesimo commento o l'ennesima voce di Storia. Un testo
che afferma una cosa e più avanti la smentisce è faticoso per una persona e
induce in errore chi lo consulti per frammenti: un corpus che non entra per
intero in contesto si interroga per ricerca, e nulla garantisce che
un'affermazione e la sua negazione vengano recuperate insieme. Il criterio per
distinguere ciò che si consolida da ciò che si conserva è nel template
`questione`, e la classificazione la decide l'operatore, non l'agente.

**Consolidare non significa abbreviare.** Il consolidamento rimuove ciò che è
errato e riscrive ciò che è confuso a parità di ricchezza espositiva: non è
un'operazione di sintesi, non accorcia il testo corretto e non comprime in forma
telegrafica ciò che era esposto per esteso. Se al termine il testo risulta più
breve, deve esserlo perché è stato tolto ciò che era sbagliato, non perché è
stato compresso ciò che era giusto.

**La Storia non ospita il contenuto del lavoro.** La motivazione nella Storia
risponde al perché di un cambiamento di stato. Le deduzioni, le ipotesi, i
risultati intermedi e le analisi appartengono al corpo: scriverli nella Storia è
un uso improprio del campo e alimenta l'accumulo che queste norme intendono
evitare.

---

## Entry nel mastro — norma sul Percorso

Ogni entry deve includere la sezione Percorso quando il ciclo ha avuto qualsiasi
complessità: stati multipli, ripensamenti, blocchi, alternative esplorate. Il
bias corretto è includere il Percorso. L'omissione è legittima solo quando la
decisione è stata diretta — apertura e chiusura senza stati intermedi
significativi. Ometterla per concisione vanifica il valore del registro.

---

## Retrieval obbligatorio del template

Prima di redigere qualsiasi artefatto protocollare
(questione, nota, commento, entry del mastro, RFC,
voce di attività), l'agente deve consultare il template
corrispondente con `get_template` nella sessione
corrente. Non è sufficiente basarsi sulla struttura
ricordata da sessioni precedenti o dal contesto già
caricato: il knowledge base potrebbe essere stato
aggiornato e la struttura ricordata potrebbe essere
incompleta o non conforme.

Il costo del retrieval è trascurabile rispetto al costo
della correzione manuale di un artefatto non conforme.

---

## Sincronizzazione tra protocollo.md e protocollo-norme.md

`protocollo-norme.md` è lo specchio AI di `protocollo.md`: espone il
testo normativo degli articoli al RAG e all'MCP. I due file devono
restare coerenti.

Ogni modifica a `protocollo.md` richiede una verifica esplicita della
proiezione su `protocollo-norme.md`. Se la modifica impatta il testo
degli articoli, degli allegati o della struttura normativa, l'agente
deve aggiornare `protocollo-norme.md` nella stessa sessione di lavoro,
prima di portare la questione a `pending-approval`.

La sincronizzazione non è opzionale: un `protocollo-norme.md` non
aggiornato produce risposte errate o incomplete quando l'MCP viene
interrogato su norme vigenti.

---

## Limiti dell'autonomia dell'agente

L'agente non decide autonomamente:

- Quale stato assegnare a un'approvazione (approvato / da rivedere)
- Se una questione può essere chiusa con domande ancora aperte
- Se avanzare alla fase successiva
- Se una RFC inbound va accettata, rifiutata o rimandata
