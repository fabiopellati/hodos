---
tipo-artefatto: regola
documento: protocollo
descrizione: testo normativo vigente del protocollo Hodos, con gli articoli su strumenti
  di governo, tipi e stati della questione, mastro, note, RFC e ciclo di vita degli
  artefatti di processo
---

# Protocollo di Processo — Hodos

**Versione**: 1.1.0
**Stato**: forma normativa vigente

> Nota di compatibilità (1.1.0).
> Questa versione aggiunge il campo `descrizione` al frontmatter delle
> questioni e delle voci del mastro: la sintesi distillata delle motivazioni
> della questione — il "prima" — che affianca `decisioni`, il "dopo".
> È un'aggiunta additiva rispetto alla 1.0.0; le opere già in forma segregata
> popolano il nuovo campo tramite l'arricchimento di bonifica.
>
> Nota di compatibilità (1.0.0).
> La 1.0.0 ha introdotto la forma segregata degli strumenti di governo
> (`questioni`, `note`, `mastro`), con rottura di compatibilità rispetto alla
> forma monolitica precedente.
> Ogni strumento passa da un unico file accumulante a una collezione di file,
> uno per elemento, con frontmatter di metadati e indice derivato.
> Le opere costruite sulla forma monolitica restano valide ma non conformi:
> la migrazione è descritta dall'arricchimento di bonifica
> (`arricchimenti/bonifica-forma-segregata`).

---

## Premessa

Costruire qualcosa richiede un processo.

Ogni lavoro organizzato — un sistema software, la redazione di un documento,
la gestione di un progetto complesso — produce decisioni, questioni aperte,
cambiamenti di direzione. Senza un modo per tracciarli, la storia del lavoro
si perde e le stesse discussioni si ripetono.

Hodos è una metodologia di processo. Definisce come registrare le decisioni,
come gestire le questioni aperte e come coordinare il lavoro tra chi governa
e chi realizza. Non prescrive strumenti, tecnologie o domini: è applicabile
a qualsiasi contesto in cui sia necessario prendere decisioni ed eseguirle.

Questo documento è il riferimento normativo. Descrive le regole operative:
quali metodi si usano, come funzionano, come si apre e come si chiude un
ciclo di lavoro, come si comunica con l'esterno del gruppo e come si passa
dall'idea al manufatto.

---

## Art. 1 — Scopo e campo di applicazione

1. Hodos è una metodologia di processo applicabile a qualsiasi contesto in
   cui sia necessario prendere decisioni ed eseguirle, indipendentemente da
   strumenti, tecnologie o dominio.

2. Il presente documento costituisce il riferimento normativo di Hodos. Definisce
   gli strumenti operativi, le regole di governo e il ciclo di vita delle
   questioni.

3. I principi che motivano le scelte operative sono definiti in `principi.md`
   e richiamati in questo documento dove necessario, senza essere ridefiniti.

4. I termini con valenza specifica sono definiti in `guide/glossario.md`.

---

## Art. 2 — Categorie di strumenti

1. Un'opera Hodos produce e utilizza strumenti riconducibili alle seguenti
   categorie:
   a) gli strumenti di governo, conservati in `project/`, tracciano le decisioni
      atomiche e la storia del processo; ne fanno parte `questioni.md`,
      `mastro.md` e `note.md`;
   b) gli artefatti della metodologia, conservati in `artefatti/`, definiscono
      come si usa Hodos; ne fanno parte `protocollo.md`, le guide e gli skills;
   c) gli elaborati dell'opera, conservati in `documenti/`, documentano le analisi
      e le decisioni tecniche prodotte nel corso dell'opera: obiettivi, scenari,
      requisiti, design, attività;
   d) il prodotto è il deliverable dell'opera; quando è costituito da file,
      è conservato in `artefatti/` o in una directory equivalente.

---

## Art. 3 — Strumenti di governo

1. Ogni opera mantiene tre strumenti di governo trasversali: le questioni,
   le note e il mastro.
   Sono strumenti trasversali e vivono per tutta la durata dell'opera.

2. L'organizzazione del lavoro nel tempo — fasi, iterazioni, milestone — è
   fuori dal perimetro di questo protocollo. Chi adotta Hodos la definisce
   autonomamente.

3. Ciascuno dei tre strumenti è una **collezione segregata**: non un unico
   file accumulante, ma una cartella che raccoglie un file per ogni elemento.
   Le cartelle sono `questioni/`, `note/` e `mastro/`.
   Ogni elemento vive nel proprio file con nome parlante:
   `Q{NNN}-slug.md` per le questioni e le voci del mastro,
   `NOTA-{NNN}-slug.md` per le note.
   La segregazione rende i diff minimi per costruzione, perché ogni elemento
   è isolato nel proprio file e nessuna riga preesistente viene spostata
   all'inserimento di un elemento nuovo.

4. A ciascuna collezione è affiancato un **indice**: `questioni.md`,
   `note.md` e `mastro.md`.
   L'indice è una **proiezione derivata** dei frontmatter degli elementi
   della collezione: viene rigenerato da uno strumento, è committato per
   comodità di lettura e navigazione, ma non è mai una seconda sorgente
   indipendente rispetto ai file-elemento.
   Un indice non va mai modificato a mano: la modifica avviene sull'elemento,
   e l'indice si rigenera.

5. Ogni elemento porta un **frontmatter YAML** di metadati strutturati, che
   affianca il corpo markdown senza sostituirne le sezioni.
   Corpo e frontmatter sono due canali con audience diversa: il corpo è
   narrazione per il lettore umano, il frontmatter è la proiezione queryable
   per l'automazione (indici, ricerche, validazione).
   La loro duplicazione controllata è deliberata e va presidiata da un
   validatore che ne verifica la coerenza.
   I campi comuni a ogni famiglia sono `id`, `titolo`, `tipo-elemento`,
   `related` e `tag`; le famiglie aggiungono i campi propri, definiti negli
   Allegati A, B e C.

6. I legami tra elementi sono espressi dal campo `related`, come lista di
   identificativi (`QUESTIONE-NNN`, `NOTA-NNN`).
   Il legame si dichiara una sola volta, sull'elemento che lo origina; le
   back-reference — quali elementi citano un dato elemento — sono derivate
   dallo strumento e non si scrivono a mano.
   I legami sono così traversabili in modo deterministico, non affidati alla
   prosa.

7. Il protocollo prescrive la forma e le invarianti — un file per elemento,
   frontmatter per famiglia, indice come proiezione derivata, `related`
   traversabile, doppio regime del mastro (Art. 6 e 10).
   La realizzazione degli strumenti che generano gli indici e validano i
   frontmatter è lasciata a chi adotta Hodos, secondo il proprio stack
   tecnologico: il protocollo non impone un linguaggio né un'architettura.

---

## Art. 4 — Le questioni

1. La cartella `questioni/` contiene le questioni aperte dell'opera: in
   analisi, in attesa, rimandate.
   Ogni questione vive nel proprio file `Q{NNN}-slug.md`.
   Quando una questione viene chiusa, il suo file viene spostato in `mastro/`
   (Art. 6) e rimosso da `questioni/`.

2. La struttura di una questione, corpo e frontmatter, è definita
   nell'Allegato A.

3. L'indice `questioni.md` è la proiezione derivata dei frontmatter dei file
   in `questioni/` e riporta ID, titolo e stato corrente di ogni questione
   presente.
   Non si mantiene a mano: si rigenera dai frontmatter (Art. 3).

4. L'ordine di presentazione nell'indice è decrescente per identificativo:
   le questioni più recenti compaiono per prime.
   L'ordinamento è una proprietà dell'indice, non dei file, che sono
   indipendenti l'uno dall'altro.

5. Il campo `related` è opzionale, ma diventa obbligatorio per le questioni
   di tipo *rilievo* con campo `Impatto` non vuoto (vedi Art. 9).

6. I campi `Domande aperte` e `Impatto` del corpo sono mutabili per addizione
   nel corso del ciclo. Due regole garantiscono la tracciabilità in entrambi
   i campi:
   a) una voce esistente non può essere rimossa; può essere dichiarata
      superata o inattuata con motivazione esplicita inline;
   b) nuove voci possono essere aggiunte in qualsiasi momento, documentando
      il motivo.

---

## Art. 5 — Le note

1. La cartella `note/` raccoglie osservazioni, memo e idee in incubazione che
   non richiedono ancora una decisione formale.
   Ogni nota vive nel proprio file `NOTA-{NNN}-slug.md`.
   Una nota non ha stati, non produce una voce nel mastro e non richiede
   approvazione.

2. L'indice `note.md` è la proiezione derivata dei frontmatter dei file in
   `note/` e riporta ID, titolo e data di ogni nota.
   Come gli altri indici, si rigenera e non si mantiene a mano.

3. Il ciclo di vita di una nota è libero: può essere archiviata nel mastro
   quando ha esaurito il suo scopo, oppure restare indefinitamente.

4. La struttura di una nota, corpo e frontmatter, è definita nell'Allegato B.

5. Il corpo di una nota è immutabile dopo la scrittura. Le rettifiche o le
   nuove conoscenze sullo stesso argomento vanno inserite nella sezione
   `Commenti`: ogni commento è additivo, immutabile e numerato localmente
   alla nota (COMMENTO-001, COMMENTO-002, ...).

5. Le casistiche tipiche di una nota sono:
   a) *osservazione in incubazione* — idea non ancora matura per diventare
      questione;
   b) *questione prematura* — si sa già cosa fare, ma il momento non è
      ancora maturo per aprire una questione formale;
   c) *memo* — riferimento, vincolo o promemoria che serve a non perdere
      un'informazione.

---

## Art. 6 — Il mastro

1. La cartella `mastro/` è il registro delle decisioni prese. Contiene solo
   cicli chiusi: una questione chiusa diventa un file `Q{NNN}-slug.md` in
   `mastro/`.
   Ogni voce descrive cosa è emerso, cosa è stato deciso e perché.

2. La chiusura di una questione è un atto meccanico:
   a) si aggiunge al file-questione la sezione `Decisioni prese` (e il
      `Percorso`, se dovuto);
   b) si sposta il file da `questioni/` a `mastro/`, aggiornandone il
      frontmatter (`tipo-elemento`, `stato: closed`, `chiusa`, e i campi di
      distillazione `decisioni` e `file-toccati`);
   c) si rigenerano gli indici `questioni.md` e `mastro.md`.
   Questo atto è distinto dal lavoro di giudizio che crea il valore della
   decisione, e non richiede di spostare testo dentro un file monolitico.

3. L'indice `mastro.md` è la proiezione derivata dei frontmatter dei file in
   `mastro/` e ne offre il sommario cronologico decrescente.

4. La struttura di ogni voce del mastro, corpo e frontmatter, è definita
   nell'Allegato C.

5. La sezione `Percorso` va inclusa quando la questione ha avuto un ciclo
   significativo — stati multipli, ripensamenti, alternative scartate. Quando
   la decisione è stata diretta, si omette.

6. La brevità non è un valore primario delle voci. L'omissione del Percorso
   è legittima solo quando il ciclo è stato effettivamente diretto — apertura
   e chiusura senza stati intermedi. Ometterla per concisione vanifica il
   valore del registro.

7. Il file del mastro adotta un **doppio regime** (vedi Art. 10):
   il corpo markdown è immutabile, il frontmatter è mutabile.
   Il corpo è la testimonianza storica della decisione e non si tocca dopo la
   scrittura; il frontmatter può essere corretto per sanare disallineamenti,
   affinare i campi di giudizio (`decisioni`, `related`, `tag`) o eseguire una
   bonifica di versione.

---

## Art. 7 — Tipi di questione

1. Una questione può essere di tre tipi:
   a) *rilievo* — conoscenza nuova emersa che modifica la comprensione del
      dominio;
   b) *revisione* — correzione o affinamento di un artefatto esistente;
   c) *anomalia* — comportamento o risultato difforme da quanto atteso.

2. Il criterio per distinguere rilievo da revisione è l'intenzione al momento
   dell'apertura: se si è identificato qualcosa ma non si è ancora pronti
   ad agire, è un rilievo; se si sa già cosa fare e si è pronti ad agire,
   è una revisione.

3. I tipi sono costrutti di governo: definiscono il comportamento del ciclo
   della questione, non la natura semantica del lavoro. I tipi non sono
   estendibili dagli arricchimenti.

4. Il tipo è immutabile dopo l'apertura. Se la classificazione iniziale si
   rivela errata, la questione deve essere chiusa e riaperta con il tipo
   corretto.

5. Il rilievo è il contenitore deliberativo del processo: la sede in cui
   una scoperta viene analizzata, discussa e compresa. Nel corso del suo
   ciclo raccoglie approfondimenti, valutazioni e conclusioni che portano
   dalla scoperta alla comprensione del problema e delle sue implicazioni.
   Il rilievo non può modificare artefatti: il suo compito è produrre
   conoscenza, non applicarla. Se durante l'analisi emerge una soluzione
   chiara e l'operatore è pronto ad agire, deve aprire una revisione e
   agire tramite essa.

---

## Art. 8 — Stati e transizioni

1. Gli stati validi di una questione sono:
   a) `open` — creata, da analizzare;
   b) `in-progress` — analisi in corso;
   c) `pending-approval` — proposta redatta, in attesa di approvazione;
   d) `pending-rfc` — RFC in corso: dall'invio fino all'avvio effettivo del
      lavoro da parte dell'attore ricevente;
   e) `in-verification` — risposta RFC ricevuta, verifica in corso; al
      completamento la questione torna a `open`;
   f) `deferred` — rimandato con motivazione esplicita;
   g) `closed` — risolto, rimosso da `questioni.md` e registrato in `mastro.md`.

2. La storia di una questione cattura ogni evento significativo — cambio di
   stato o no — con una nota che risponde al "perché".

3. Quando una questione viene chiusa, la voce corrispondente nell'indice
   viene rimossa.

Diagramma: [ciclo di vita di una questione](diagrams/ciclo-questione.puml)

---

## Art. 9 — Proiezione del rilievo in revisione

1. Quando nel corso di un rilievo emergono impatti concreti, la conoscenza
   acquisita si proietta naturalmente in una o più questioni di revisione
   collegate. Ogni revisione prende in carico un impatto specifico e lo
   porta a esecuzione. Il rilievo resta come testimonianza del percorso
   deliberativo; le revisioni sono i suoi effetti operativi.

2. Un rilievo con campo `Impatto` non vuoto non può essere chiuso finché non
   esiste almeno una questione di tipo *revisione* aperta nel campo
   `Questioni collegate`.

3. La revisione collegata non deve essere necessariamente completata prima
   della chiusura del rilievo: deve però esistere, a testimonianza che il
   lavoro di applicazione è stato preso in carico.

---

## Art. 10 — Doppio regime del mastro e tracciamento dei cambiamenti

1. Il **corpo** di una voce del mastro è immutabile: una volta registrato non
   può essere modificato né rimosso.
   Il corpo è la testimonianza storica della decisione.

2. Il **frontmatter** di una voce del mastro è mutabile.
   Può essere corretto per sanare un disallineamento con il corpo, per
   affinare i campi di giudizio (`decisioni`, `related`, `tag`) o nel corso di
   una bonifica di versione dell'opera.
   La mutabilità del frontmatter non intacca l'immutabilità del corpo: sono
   due canali distinti, e ogni modifica del frontmatter resta tracciata dalla
   cronologia di versione.

3. Se una decisione precedente viene cambiata o invalidata, il cambiamento
   viene tracciato aprendo una nuova questione. La chiusura di questa questione
   produce una nuova voce nel mastro che documenta la decisione aggiornata.
   Correggere il corpo di una voce esistente non è mai il modo di cambiare una
   decisione: per questo si apre una nuova questione.

4. Il mastro preserva la sequenza storica, non lo stato corrente dell'opera.
   La coesistenza di una decisione e della sua successiva revisione è corretta e attesa.

---

## Art. 11 — Coordinamento esterno: RFC

1. Una RFC è un documento formale generato quando una questione richiede
   intervento nell'ambito di competenza di un attore esterno. È autocontenuto:
   leggibile senza conoscere la storia interna dell'opera richiedente.

2. La RFC è bidirezionale: l'attore ricevente compila una sezione
   **Response RFC** e restituisce il documento. Questo vale sia per RFC
   outbound che inbound.

3. La sezione di richiesta è immutabile dopo la generazione. I contributi
   successivi avvengono esclusivamente tramite la sezione Response RFC
   e commenti.

**RFC Outbound**

4. La RFC Outbound viene generata quando una questione interna non può essere
   risolta senza intervento esterno. Il ciclo è:
   a) la questione passa allo stato `pending-rfc`;
   b) la RFC viene generata e consegnata all'attore esterno;
   c) l'attore esterno compila la sezione Response RFC e restituisce la RFC;
   d) il richiedente verifica che il lavoro soddisfi l'esigenza;
   e) solo se la verifica ha esito positivo, la questione viene chiusa;
   f) il lavoro in attesa può procedere.

5. Il completamento del lavoro da parte dell'attore esterno non chiude la
   questione: sblocca la fase di verifica. La responsabilità della verifica
   resta in capo al richiedente.

**RFC Inbound**

6. La RFC Inbound viene ricevuta quando un attore esterno richiede un
   intervento nell'opera. Il ciclo è:
   a) la RFC viene valutata prima di aprire qualsiasi questione;
   b) la valutazione determina la distribuzione del lavoro;
   c) viene aperta una questione appropriata;
   d) il lavoro segue il normale ciclo di realizzazione, inclusi verifica
      e conformità rispetto alla richiesta;
   e) al completamento, la sezione Response RFC viene compilata e restituita;
   f) la questione viene chiusa.

7. La chiusura della questione segna il completamento del ciclo RFC nella sua
   interezza, inclusa la restituzione della risposta. Non è un atto
   separabile dalla consegna.

**RFC Informativa**

8. Una RFC può essere emessa come comunicazione unidirezionale verso un
   attore esterno, senza attesa di risposta. In questo caso il documento
   dichiara `Tipo: informativa` nell'intestazione e la questione di
   origine non transita allo stato `pending-rfc`; il suo ciclo prosegue
   indipendentemente dall'invio.

Diagramma: [flusso RFC outbound e inbound](diagrams/flusso-rfc.puml)

---

## Art. 12 — Flusso di processo

[da redigere]

---

## Allegato A — Struttura di una questione

File: `questioni/Q{NNN}-slug.md`.

Frontmatter:

```yaml
---
id: QUESTIONE-XXX
titolo: Titolo della questione
descrizione: sintesi distillata delle motivazioni della questione (il "prima")
tipo-elemento: questione
tipo: rilievo | revisione | anomalia
stato: open | in-progress | pending-approval | pending-rfc | in-verification | deferred
aperta: YYYY-MM-DD
aggiornata: YYYY-MM-DD
related: [QUESTIONE-YYY, ...]
tag: [tema-uno, tema-due]
---
```

Corpo:

```
## QUESTIONE-XXX — Titolo

**Tipo**: rilievo | revisione | anomalia
**Stato**: [stato corrente]

**Storia**
- YYYY-MM-DD [stato] — motivazione

**Descrizione**
[corpo della questione]

**Domande aperte**
- [ ] domanda

**Impatto**
- `artefatto` — descrizione

**Commenti** (opzionale)

COMMENTO-NNN — YYYY-MM-DD
[testo del commento]
```

I campi `tipo` e `stato` compaiono sia nel frontmatter sia nel corpo: il
frontmatter è il canale queryable, il corpo il canale narrativo.
La coerenza tra i due è presidiata dal validatore dell'opera.
Il legame con altre questioni si dichiara nel campo `related` del frontmatter,
non più in una sezione `Questioni collegate` del corpo.

---

## Allegato B — Struttura di una nota

File: `note/NOTA-{NNN}-slug.md`.

Frontmatter:

```yaml
---
id: NOTA-XXX
titolo: Titolo sintetico
tipo-elemento: nota
data: YYYY-MM-DD
related: [QUESTIONE-YYY, NOTA-ZZZ, ...]
tag: [tema-uno]
---
```

Corpo:

```
## NOTA-XXX — YYYY-MM-DD — Titolo sintetico

[corpo della nota, formato libero]

**Commenti** (opzionale)

COMMENTO-NNN — YYYY-MM-DD
[testo del commento]
```

---

## Allegato C — Struttura di una voce del mastro

File: `mastro/Q{NNN}-slug.md`.
Il corpo è immutabile; il frontmatter è mutabile (Art. 10).

Frontmatter:

```yaml
---
id: QUESTIONE-XXX
titolo: Titolo della questione
descrizione: sintesi distillata delle motivazioni della questione (il "prima")
tipo-elemento: voce-mastro
tipo: rilievo | revisione | anomalia
stato: closed
chiusa: YYYY-MM-DD
related: [QUESTIONE-YYY, ...]
tag: [tema-uno, tema-due]
decisioni:
  - sintesi distillata di una decisione presa
file-toccati:
  - percorso/artefatto/uno
---
```

Corpo:

```
## YYYY-MM-DD — Chiusura [QUESTIONE-ID]: Titolo

**Questione**: [QUESTIONE-ID] — Titolo

**Percorso** (opzionale)
[sintesi del percorso: stati intermedi, ripensamenti, alternative valutate]

**Decisioni prese**
[elenco delle decisioni con motivazione]

**Impatto**
[artefatti modificati o da modificare]
```

Il campo `descrizione` del frontmatter è la sintesi distillata delle
motivazioni della questione — il "prima" —; i campi `decisioni` e
`file-toccati` sono la distillazione queryable, rispettivamente, della sezione
`Decisioni prese` e della sezione `Impatto` del corpo — il "dopo".
