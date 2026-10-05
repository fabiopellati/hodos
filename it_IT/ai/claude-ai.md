---
tipo-artefatto: guida
documento: guida-ai
descrizione: istruzioni operative per l'agente AI che lavora in un'opera Hodos
autorita: operativa
---

# Guida AI — Layer operativo sopra il Protocollo

Questa guida descrive come l'agente AI applica il protocollo di processo definito
in `protocollo.md`. È un layer opzionale: il processo è applicabile senza AI.
L'agente accelera l'esecuzione ma non sostituisce le decisioni umane.

Per le norme vincolanti proprie dell'agente (principi operativi, recupero
obbligatorio del template, limiti di autonomia) consultare `norme-ai.md`.
La norma sul Percorso ha sede nell'Art. 6 del protocollo.

---

## Dove si scrive, e dove non si scrive mai

Gli strumenti di governo sono collezioni segregate: ogni elemento vive nel
proprio file dentro `questioni/`, `note/` o `mastro/` (Art. 3 comma 3).
I tre file `questioni.md`, `note.md` e `mastro.md` sono **indici derivati**, non
documenti: si rigenerano dai frontmatter e non si modificano mai a mano
(Art. 3 comma 4). Ogni scrittura avviene sul file dell'elemento; l'indice si
rigenera dopo, con lo strumento dell'opera.

Prima di creare o modificare un elemento si recupera il template dal server MCP
con `get_template`, e le regole applicabili con `get_protocol_rules`: la forma
non si ricostruisce a memoria né si deduce dagli elementi esistenti, che possono
portare derive o convenzioni di versioni passate.

---

## Workflow tipico per un'attività

1. **Apri una questione** nel proprio file `questioni/Q{NNN}-slug.md`, con stato `open`
2. **Porta a `in-progress`** prima di iniziare il lavoro
3. **Svolgi il lavoro**
4. **Porta a `pending-approval`** al completamento
5. **Attendi l'approvazione umana** — non procedere oltre
6. **Alla conferma**: chiudi secondo l'Art. 6 comma 2 e rigenera gli indici

---

## Gestione delle questioni

**Aprire**: creare il file nella collezione `questioni/`. Se il tipo
(rilievo/revisione/anomalia) o la descrizione non sono chiari dal contesto,
chiedere prima di procedere.

**Aggiornare lo stato**: la motivazione del cambio di stato è sempre
obbligatoria. Non cambiare stato senza una voce nella Storia che dica il perché
e non il cosa (Art. 8 comma 2).

**Consolidare il corpo**: finché la questione è aperta il corpo è modificabile e
si preferisce il consolidamento all'accumulo di commenti. L'immutabilità del
corpo appartiene alla nota e alla voce del mastro, non alla questione aperta.

**Chiudere**: verificare che le domande aperte siano risolte, aggiungere al file
la sezione `Decisioni prese` e il `Percorso` ove dovuto, spostare il file da
`questioni/` a `mastro/` aggiornandone il frontmatter, e rigenerare i due indici
(Art. 6 comma 2). Un rilievo con `Impatto` non vuoto non si chiude senza una
revisione aperta che lo dichiari nel proprio campo `related` (Art. 9 comma 2).

**Propagazione a ritroso**: se una questione emerge in una fase avanzata e
invalida assunzioni di fasi precedenti, aprire le questioni collegate nelle fasi
impattate, dichiarando il legame nel campo `related` del frontmatter di ciascuna
(Art. 3 comma 6). Indicare esplicitamente Fase di origine, Propagazione e
Sintesi, e risolvere dalla fase radice verso quella più avanzata.

---

## Gestione delle note

**Aprire una nota**: creare il file `note/NOTA-{NNN}-slug.md` con
identificativo univoco, descrizione sintetica e data, e rigenerare l'indice.
Il corpo della nota è immutabile dopo la scrittura: ogni rettifica o nuova
conoscenza sullo stesso argomento va nella sezione `Commenti` (Art. 5 comma 5).

**Quando usare una nota invece di una questione**: quando non c'è ancora una
decisione da prendere, quando la decisione esiste ma il processo non è nella
fase giusta, o come semplice memo. Se c'è qualcosa da decidere ora, aprire
una questione.

**Archiviazione**: una nota può essere archiviata nel mastro quando ha esaurito
il suo scopo. Non ci sono vincoli su quando o come farlo.

---

## Gestione delle RFC

**RFC outbound**: aprire una RFC quando una questione richiede intervento
esterno. Il documento deve essere autocontenuto: verificare che un lettore
esterno possa capire richiesta e contesto senza conoscere il progetto.

**RFC inbound**: valutare la RFC ricevuta prima di aprire qualsiasi questione.
La valutazione determina fase e distribuzione del lavoro. La questione generata
segue il normale ciclo, inclusa la verifica di conformità prima della chiusura.

---

## Glossario e terminologia

Usare sempre i termini definiti in `glossario.md`. Se durante la
redazione di un documento emerge un termine con valenza specifica non ancora
nel glossario, aggiungerlo immediatamente prima di continuare.

Non usare "nostro team" o "team esterno": usare Team-A e Team-B.
Non usare "append-only" per il mastro: il termine corretto è prepend-only.
