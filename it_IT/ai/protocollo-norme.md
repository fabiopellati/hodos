---
tipo-artefatto: riferimento-normativo
documento: protocollo-norme
descrizione: testo normativo degli articoli del protocollo Hodos — strumenti
  di governo, tipi di questione, stati e transizioni, mastro, RFC outbound
  inbound e informativa
fonte: protocollo.md
---

# Norme del Protocollo — Hodos

Questo documento è la trascrizione fedele degli articoli normativi di
`protocollo.md`, resa disponibile per la consultazione tramite MCP. In
caso di discrepanza, il testo autoritativo è `protocollo.md`.

---

## Art. 1 — Scopo e campo di applicazione

1. Hodos è una metodologia di processo applicabile a qualsiasi contesto in
   cui sia necessario prendere decisioni ed eseguirle, indipendentemente da
   strumenti, tecnologie o dominio.

2. Il presente documento costituisce il riferimento normativo di Hodos.
   Definisce gli strumenti operativi, le regole di governo e il ciclo di
   vita delle questioni.

3. I principi che motivano le scelte operative sono definiti in
   `principi.md` e richiamati in questo documento dove necessario, senza
   essere ridefiniti.

4. I termini con valenza specifica sono definiti in `guide/glossario.md`.

---

## Art. 2 — Categorie di strumenti

1. Un'opera Hodos produce e utilizza strumenti riconducibili alle seguenti
   categorie:
   - gli strumenti di governo, conservati in `project/`, tracciano le
     decisioni atomiche e la storia del processo; ne fanno parte
     `questioni.md`, `mastro.md` e `note.md`;
   - gli artefatti della metodologia, conservati in `artefatti/`,
     definiscono come si usa Hodos; ne fanno parte `protocollo.md`, le
     guide e gli skills;
   - gli elaborati dell'opera, conservati in `documenti/`, documentano
     le analisi e le decisioni tecniche prodotte nel corso dell'opera;
   - il prodotto è il deliverable dell'opera.

---

## Art. 3 — Strumenti di governo

1. Ogni opera mantiene tre strumenti di governo trasversali:
   - `questioni.md`
   - `note.md`
   - `mastro.md`

   Sono strumenti trasversali e vivono per tutta la durata dell'opera.

2. L'organizzazione del lavoro nel tempo — fasi, iterazioni, milestone —
   è fuori dal perimetro di questo protocollo. Chi adotta Hodos la
   definisce autonomamente.

---

## Art. 4 — questioni.md

1. `questioni.md` contiene le questioni aperte dell'opera: in analisi,
   in attesa, rimandati. Quando una questione viene chiusa, viene rimossa
   da `questioni.md` e la sua risoluzione viene registrata in `mastro.md`.

2. La struttura di una questione è definita nell'Allegato A.

3. Il documento è preceduto da un indice in intestazione che riporta ID,
   titolo e stato corrente di ogni questione presente.

4. Le questioni sono ordinate in senso decrescente: ogni nuova questione
   viene inserita prima delle precedenti. L'ordine è immutabile dopo la
   creazione.

5. Il campo `Questioni collegate` è opzionale, ma diventa obbligatorio
   per le questioni di tipo rilievo con campo `Impatto` non vuoto.

6. I campi `Domande aperte` e `Impatto` sono mutabili per addizione nel
   corso del ciclo. Due regole garantiscono la tracciabilità:
   - una voce esistente non può essere rimossa; può essere dichiarata
     superata o inattuata con motivazione esplicita inline;
   - nuove voci possono essere aggiunte in qualsiasi momento,
     documentando il motivo.

---

## Art. 5 — note.md

1. `note.md` raccoglie osservazioni, memo e idee in incubazione che non
   richiedono ancora una decisione formale. Una nota non ha stati, non
   produce una voce nel mastro e non richiede approvazione.

2. Il ciclo di vita di una nota è libero: può essere archiviata nel
   mastro quando ha esaurito il suo scopo, oppure restare
   indefinitamente.

3. Il corpo di una nota è immutabile dopo la scrittura. Le rettifiche o
   le nuove conoscenze sullo stesso argomento vanno inserite nella
   sezione `Commenti`: ogni commento è additivo, immutabile e numerato
   localmente alla nota (COMMENTO-001, COMMENTO-002, ...).

4. Le casistiche tipiche di una nota sono:
   - osservazione in incubazione — idea non ancora matura per diventare
     questione;
   - questione prematura — si sa già cosa fare, ma il momento non è
     ancora maturo per aprire una questione formale;
   - memo — riferimento, vincolo o promemoria che serve a non perdere
     un'informazione.

---

## Art. 6 — mastro.md

1. `mastro.md` è il registro immutabile delle decisioni prese. Contiene
   solo cicli chiusi. Ogni voce descrive cosa è emerso, cosa è stato
   deciso e perché.

2. Le voci sono ordinate in senso decrescente: ogni nuova voce viene
   inserita prima delle precedenti (prepend-only). Una voce non viene
   mai modificata dopo la scrittura.

3. La sezione `Percorso` va inclusa quando la questione ha avuto un
   ciclo significativo — stati multipli, ripensamenti, alternative
   scartate. Quando la decisione è stata diretta, si omette.

4. La brevità non è un valore primario delle voci. L'omissione del
   Percorso è legittima solo quando il ciclo è stato effettivamente
   diretto — apertura e chiusura senza stati intermedi. Ometterla per
   concisione vanifica il valore del registro.

---

## Art. 7 — Tipi di questione

1. Una questione può essere di tre tipi:
   - rilievo — conoscenza nuova emersa che modifica la comprensione del
     dominio;
   - revisione — correzione o affinamento di un artefatto esistente;
   - anomalia — comportamento o risultato difforme da quanto atteso.

2. Il criterio per distinguere rilievo da revisione è l'intenzione al
   momento dell'apertura: se si è identificato qualcosa ma non si è
   ancora pronti ad agire, è un rilievo; se si sa già cosa fare e si è
   pronti ad agire, è una revisione.

3. I tipi sono costrutti di governo: definiscono il comportamento del
   ciclo della questione, non la natura semantica del lavoro. I tipi non
   sono estendibili dagli arricchimenti.

4. Il tipo è immutabile dopo l'apertura. Se la classificazione iniziale
   si rivela errata, la questione deve essere chiusa e riaperta con il
   tipo corretto.

5. Il rilievo è il contenitore deliberativo del processo: la sede in cui
   una scoperta viene analizzata, discussa e compresa. Il rilievo non
   può modificare artefatti: il suo compito è produrre conoscenza, non
   applicarla. Se durante l'analisi emerge una soluzione chiara e
   l'operatore è pronto ad agire, deve aprire una revisione e agire
   tramite essa.

---

## Art. 8 — Stati e transizioni

1. Gli stati validi di una questione sono:
   - `open` — creata, da analizzare;
   - `in-progress` — analisi in corso;
   - `pending-approval` — proposta redatta, in attesa di approvazione;
   - `pending-rfc` — RFC in corso: dall'invio fino all'avvio effettivo
     del lavoro da parte dell'attore ricevente;
   - `in-verification` — risposta RFC ricevuta, verifica in corso; al
     completamento la questione torna a `open`;
   - `deferred` — rimandato con motivazione esplicita;
   - `closed` — risolto, rimosso da `questioni.md` e registrato in
     `mastro.md`.

2. La storia di una questione cattura ogni evento significativo — cambio
   di stato o no — con una nota che risponde al "perché".

3. Quando una questione viene chiusa, la voce corrispondente nell'indice
   viene rimossa.

---

## Art. 9 — Proiezione del rilievo in revisione

1. Quando nel corso di un rilievo emergono impatti concreti, la
   conoscenza acquisita si proietta naturalmente in una o più questioni
   di revisione collegate. Ogni revisione prende in carico un impatto
   specifico e lo porta a esecuzione. Il rilievo resta come testimonianza
   del percorso deliberativo; le revisioni sono i suoi effetti operativi.

2. Un rilievo con campo `Impatto` non vuoto non può essere chiuso finché
   non esiste almeno una questione di tipo revisione aperta nel campo
   `Questioni collegate`.

3. La revisione collegata non deve essere necessariamente completata
   prima della chiusura del rilievo: deve però esistere, a testimonianza
   che il lavoro di applicazione è stato preso in carico.

---

## Art. 10 — Immutabilità del mastro e tracciamento dei cambiamenti

1. Il mastro è immutabile: una voce registrata non può essere modificata
   né rimossa.

2. Se una decisione precedente viene cambiata o invalidata, il
   cambiamento viene tracciato aprendo una nuova questione. La chiusura
   di questa questione produce una nuova voce nel mastro che documenta la
   decisione aggiornata.

3. Il mastro preserva la sequenza storica, non lo stato corrente
   dell'opera. La coesistenza di una decisione e della sua successiva
   revisione è corretta e attesa.

---

## Art. 11 — Coordinamento esterno: RFC

1. Una RFC è un documento formale generato quando una questione richiede
   intervento nell'ambito di competenza di un attore esterno. È
   autocontenuta: leggibile senza conoscere la storia interna dell'opera
   richiedente.

2. La sezione di richiesta è immutabile dopo la generazione. I contributi
   successivi avvengono esclusivamente tramite la sezione Response RFC
   e commenti.

**RFC Outbound**

3. La RFC Outbound viene generata quando una questione interna non può
   essere risolta senza intervento esterno. Il ciclo è:
   - la questione passa allo stato `pending-rfc`;
   - la RFC viene generata e consegnata all'attore esterno;
   - l'attore esterno compila la sezione Response RFC e restituisce la
     RFC;
   - il richiedente verifica che il lavoro soddisfi l'esigenza;
   - solo se la verifica ha esito positivo, la questione viene chiusa.

4. Il completamento del lavoro da parte dell'attore esterno non chiude
   la questione: sblocca la fase di verifica. La responsabilità della
   verifica resta in capo al richiedente.

**RFC Inbound**

5. La RFC Inbound viene ricevuta quando un attore esterno richiede un
   intervento nell'opera. Il ciclo è:
   - la RFC viene valutata prima di aprire qualsiasi questione;
   - la valutazione determina la distribuzione del lavoro;
   - viene aperta una questione appropriata;
   - il lavoro segue il normale ciclo di realizzazione;
   - al completamento, la sezione Response RFC viene compilata e
     restituita;
   - la questione viene chiusa.

6. La chiusura della questione segna il completamento del ciclo RFC nella
   sua interezza, inclusa la restituzione della risposta. Non è un atto
   separabile dalla consegna.

**RFC Informativa**

7. Una RFC può essere emessa come comunicazione unidirezionale verso un
   attore esterno, senza attesa di risposta. In questo caso il documento
   dichiara `Tipo: informativa` nell'intestazione e la questione di
   origine non transita allo stato `pending-rfc`; il suo ciclo prosegue
   indipendentemente dall'invio.

---

## Allegato A — Struttura di una questione

```
## QUESTIONE-XXX — Titolo

**Tipo**: rilievo | revisione | anomalia
**Stato**: [stato corrente]

**Storia**
- YYYY-MM-DD [stato] — motivazione

**Questioni collegate**: [QUESTIONE-YYY, ...] (opzionale)

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

---

## Allegato B — Struttura di una nota

```
## NOTA-XXX — YYYY-MM-DD — Titolo sintetico

[corpo della nota, formato libero]

**Commenti** (opzionale)

COMMENTO-NNN — YYYY-MM-DD
[testo del commento]
```

---

## Allegato C — Struttura di una voce del mastro

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
