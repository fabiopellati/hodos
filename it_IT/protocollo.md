# Protocollo di Processo — Hodos

**Versione**: bozza
**Stato**: in redazione

> I termini con valenza specifica in questo documento sono definiti in
> `guide/glossario.md`, redatto in parallelo. Ogni termine compare nel glossario
> nel momento in cui viene introdotto per la prima volta.

---

## Principi Fondamentali

I principi guida di Hodos — semplicita', adattabilita', indipendenza dal dominio,
strumento-agnostic, univocita' terminologica, approvazioni esplicite, tracciabilita'
delle decisioni — sono descritti con motivazione estesa e criteri di adozione in
`principi.md`.

Questo protocollo li richiama dove necessario per motivare le scelte operative,
senza ridefinirli.

---

## Artefatti del Processo

Ogni opera mantiene tre documenti trasversali che non sono artefatti consolidati
ma strumenti di governo del processo. Non appartengono a nessuna fase specifica:
vivono per tutta la durata dell'opera.

Hodos non prescrive un ciclo di vita a fasi. Chi adotta la metodologia definisce
il proprio percorso. Un percorso di riferimento opzionale basato su fasi
sequenziali (P0-P4) e' descritto nello skill `arricchimento-fasi.md`.

### questioni.md

Contiene i problemi aperti della fase: in analisi, in attesa, rimandati.
Quando una questione viene chiusa, viene rimossa da `questioni.md` e la sua
risoluzione viene registrata in `mastro.md`.

**Struttura**:

```
# Questioni — [nome progetto]

## Indice

| ID | Titolo | Stato |
|---|---|---|
| QUESTIONE-XXX | ... | [stato] |

---

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
- `artefatto` — descrizione (obbligatorio se tipo e' rilievo)

**Commenti** (opzionale)

COMMENTO-NNN — YYYY-MM-DD
[testo del commento]
```

Il campo `Questioni collegate` e' opzionale nella struttura generale, ma diventa
obbligatorio per le questioni di tipo *rilievo* che hanno il campo `Impatto` non
vuoto (vedi regola di chiusura sotto).

**Ordine**: decrescente — ogni nuova questione viene inserita prima delle
precedenti. L'ordine riflette la sequenza cronologica di inserimento, che e'
informazione di processo rilevante: sapere quando e' emerso un problema rispetto
agli altri aiuta a ricostruire il contesto decisionale. Per questa ragione
l'ordine e' immutabile dopo la creazione. Le sezioni strutturali del documento
(intestazione, indice) restano nelle loro posizioni. L'indice in intestazione
compensa l'immutabilita' mostrando lo stato corrente di ogni questione.

**Natura delle questioni**: una questione puo' essere di tre nature:
- *rilievo* — conoscenza nuova emersa che modifica la comprensione del dominio
- *revisione* — correzione o affinamento di un artefatto esistente
- *anomalia* — comportamento o risultato difforme da quanto atteso

Il criterio per scegliere tra rilievo e revisione e' l'intenzione al momento
dell'apertura: se si e' identificato qualcosa ma non si e' ancora pronti ad agire,
e' un rilievo; se si sa gia' cosa fare e si e' pronti ad agire, e' una revisione.

Il tipo e' immutabile dopo l'apertura. Se la classificazione iniziale si rivela
errata, la strada corretta e' chiudere la questione e riaprirla con il tipo giusto,
non modificare il tipo in corso d'opera.

**Perimetro del rilievo**: nel corso del suo ciclo, un rilievo non puo' modificare
artefatti. Il suo compito e' registrare conoscenza e identificare cosa vale la pena
fare — non farlo. Se durante l'analisi emerge una soluzione chiara e l'operatore
e' pronto ad agire, la strada corretta e' aprire immediatamente una revisione e
agire tramite essa. L'overhead e' minimo; il guadagno e' che ogni modifica a un
artefatto e' sempre governata da una questione dedicata, con la propria storia e
il proprio ciclo.

Questo vincolo esiste per una ragione precisa: senza di esso, il rilievo tende a
espandersi fino a eseguire l'impatto che ha identificato, aggirando la distinzione
concettuale tra "ho capito cosa c'e' da fare" e "l'ho fatto". Il mastro registra
decisioni, non esecuzioni; la revisione e' lo strumento che collega le due cose.

**Stati**:

| Stato | Significato |
|---|---|
| `open` | creata, da analizzare |
| `in-progress` | analisi in corso |
| `pending-approval` | proposta redatta, in attesa di approvazione umana |
| `pending-rfc` | RFC in corso: dall'invio fino all'avvio effettivo del lavoro da parte del team ricevente |
| `in-verification` | risposta ricevuta, verifica in corso |
| `deferred` | rimandato con motivazione esplicita |
| `closed` | risolto, rimosso da questioni.md e registrato in mastro.md |

La storia cattura ogni evento significativo della questione — cambio di stato
o no — con una nota che risponde al "perche'".
Quando una questione viene chiusa e spostata nel mastro, anche la relativa voce
in indice viene rimossa.

**Chiusura di un rilievo con impatto**: un rilievo porta conoscenza nuova che
modifica la comprensione del dominio. Quando questa conoscenza richiede modifiche
concrete ad artefatti esistenti — cioe' quando il campo `Impatto` non e' vuoto
— la decisione da sola non basta: serve che qualcuno si faccia carico di
applicarla. Questo e' il ruolo della questione di revisione collegata: e' il
modo con cui il processo garantisce che l'impatto non resti solo dichiarato.

Per questo, un rilievo con campo `Impatto` non vuoto non puo' essere chiuso
finche' non esiste almeno una questione di tipo *revisione* aperta nel campo
`Questioni collegate`. La revisione collegata non deve essere necessariamente
completata prima della chiusura del rilievo: deve pero' esistere, a testimonianza
che il lavoro di applicazione e' stato preso in carico.

### notes.md

Raccoglie osservazioni, memo e idee in incubazione che non richiedono ancora
una decisione formale. Una nota non e' una questione: non ha stati, non produce
una entry nel mastro, non richiede approvazione. Il suo ciclo di vita e' libero:
puo' essere archiviata nel mastro quando ha esaurito il suo scopo, oppure restare
indefinitamente.

**Struttura**:

```
# Note — [nome progetto]

## NOTA-XXX — YYYY-MM-DD — Titolo sintetico

[corpo della nota, formato libero]

**Commenti** (opzionale)

COMMENTO-NNN — YYYY-MM-DD
[testo del commento]

---

## Indice

| ID | Descrizione | Data |
|---|---|---|
| NOTA-XXX | ... | YYYY-MM-DD |

> Ultima nota inserita: NOTA-XXX — YYYY-MM-DD.
```

**Immutabilita' e commenti**: il corpo di una nota e' immutabile dopo la scrittura.
Per aggiungere una rettifica, un'obiezione o una nuova conoscenza sullo stesso
argomento senza aprire una nota separata, si usa la sezione `Commenti`: ogni
commento e' additivo, immutabile e numerato localmente alla nota (COMMENTO-001,
COMMENTO-002, ...). La sezione e' opzionale: se la nota non ha commenti, non
compare.

**Casistiche**:
- *Osservazione in incubazione* — idea non ancora matura per diventare questione
- *Questione prematura* — la decisione esiste ma il processo non e' nella fase giusta
- *Memo* — riferimento, vincolo tecnico o promemoria che serve a non perdere un'informazione

**Destinatari**: primariamente chi scrive. Le note possono essere knowledge
collettiva del team e input attivo per l'AI come contesto di supporto.

### mastro.md

Registro immutabile delle decisioni prese. Contiene solo cicli chiusi.
Ogni entry descrive cosa e' emerso, cosa e' stato deciso e perche'.

**Ordine**: decrescente — ogni nuova entry viene inserita prima delle precedenti
(prepend-only). L'ordine cronologico inverso serve a trovare rapidamente le
decisioni piu' recenti senza scorrere l'intero registro. Una entry nel mastro
non viene mai modificata dopo la scrittura: il mastro e' testimonianza storica,
non uno strumento di lavoro corrente — modificarlo significherebbe alterare la
memoria del processo.

**Struttura di una entry**:

```
## YYYY-MM-DD — Chiusura [QUESTIONE-ID]: Titolo

**Questione**: [QUESTIONE-ID] — Titolo

**Percorso** (opzionale)
[arco sintetico del ciclo: stati intermedi, ripensamenti, alternative valutate]

**Decisioni prese**
[elenco delle decisioni con motivazione]

**Impatto**
[artefatti modificati o da modificare]
```

La sezione **Percorso** e' opzionale: va inclusa quando la questione ha avuto
un ciclo significativo — stati multipli, ripensamenti, alternative scartate.
Quando la decisione e' stata diretta, si omette. La sua presenza garantisce
che il mastro possa rispondere non solo a "cosa si e' deciso" ma anche a
"come si e' arrivati a deciderlo".

---

## Questioni con Propagazione a Ritroso

Una questione emersa in una fase avanzata puo' invalidare assunzioni di fasi
precedenti. In questo caso genera questioni collegate nelle fasi impattate e ne
annota i riferimenti.

La struttura include campi aggiuntivi:

```
**Fase di origine**: [fase dove e' emerso]
**Propagazione**: [fasi e artefatti impattati]
**Sintesi**: [narrativa che da' il quadro senza dover aprire i mastri delle altre fasi]
**Questioni collegate**: [lista con riferimenti espliciti]
```

La sintesi narrativa consente di capire la catena senza aprire piu' documenti.
I riferimenti espliciti consentono di seguire la catena per chi vuole la profondita'.

---

## RFC — Request for Change

Una RFC e' un documento formale generato quando una questione richiede intervento
su un sistema gestito da Team-B. E' autocontenuto: leggibile senza conoscere la
storia interna del progetto richiedente.

La RFC e' bidirezionale: il team ricevente compila una sezione **Response RFC**
(decisione, cosa e' stato fatto, eventuali deviazioni) e restituisce il documento.
Questo vale sia per RFC outbound che inbound.

**Immutabilita' della richiesta**: la sezione di richiesta e' immutabile dopo la
generazione. I contributi successivi avvengono esclusivamente tramite la sezione
Response RFC e commenti.

### RFC Outbound

Generata quando una questione interna non puo' essere risolta senza intervento
esterno.

**Ciclo**:
1. La questione passa allo stato `pending-rfc`
2. La RFC viene generata e consegnata al Team-B
3. Il Team-B compila la sezione Response RFC e restituisce la RFC
4. Team-A verifica che il lavoro soddisfi l'esigenza
5. Solo se la verifica ha esito positivo, la questione viene chiusa
6. Il lavoro in attesa puo' procedere

Il *done* del Team-B non chiude la questione: sblocca la fase di verifica.
La responsabilita' della verifica resta in capo a Team-A.

### RFC Inbound

Ricevuta quando Team-B richiede un intervento nel sistema di Team-A.

**Ciclo**:
1. La RFC viene valutata da Team-A prima di aprire qualsiasi questione
2. La valutazione determina la fase di appartenenza e la distribuzione del lavoro
3. Viene aperta una questione nella fase appropriata
4. Il lavoro segue il normale ciclo di realizzazione, inclusi verifica e conformita'
   rispetto alla request
5. Al completamento, Team-A compila la sezione Response RFC e la restituisce
6. La questione viene chiusa

La chiusura della questione segna il completamento del ciclo RFC nella sua
interezza, inclusa la restituzione della risposta. Non e' un atto separabile
dalla consegna.

La verifica di conformita' e' implicita nel processo: la questione non si chiude
prima che il risultato sia verificato rispetto alla request originale.
