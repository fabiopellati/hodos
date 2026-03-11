---
skill: questione
client: Claude Code CLI
invocazione: /hodos-questione
tipo: operativo
locale: it_IT
---

Gestisci il ciclo di vita di una questione nel file questioni.md del progetto
corrente: apertura, aggiornamento di stato, esecuzione di azioni, chiusura.

L'azione da svolgere viene determinata dalla combinazione tra il prompt di
lancio e lo stato corrente della questione. Non e' necessario scegliere una
skill diversa per fasi diverse del ciclo.

## 1. Trova questioni.md

Cerca `questioni.md` nella directory corrente e nelle sottodirectory immediate
(es. `documenti/`, `project/`).

Se non esiste, chiedi all'utente dove crearlo prima di procedere.

## 2. Determina l'operazione

Leggi il prompt e identifica l'operazione richiesta:

- **apertura** — il prompt descrive un nuovo problema, rilievo o revisione da
  tracciare (nessun ID specificato, o ID non presente in questioni.md)
- **aggiornamento stato** — il prompt specifica un ID e un nuovo stato
  (`in-progress`, `pending-approval`, `pending-rfc`, `in-verification`,
  `deferred`, `closed`)
- **commento** — il prompt chiede di aggiungere un commento a una questione
  esistente
- **chiusura** — il prompt specifica `closed` oppure usa termini come "chiudi",
  "completa", "risolvi"

Se l'operazione non e' chiara, chiedi tramite AskUserQuestion.

---

## Operazione A — Apertura

### A1. Determina i parametri

Se il contesto del messaggio non fornisce tutte le informazioni necessarie,
usa AskUserQuestion per raccogliere:

- **Tipo**: `rilievo` (conoscenza nuova emersa), `revisione` (correzione
  artefatto esistente) o `anomalia` (comportamento difforme da quanto atteso)
- **Titolo**: breve e descrittivo
- **Descrizione**: il problema, il rilievo, la revisione o l'anomalia

Se il tipo e' `rilievo`, verifica con l'operatore:

> Stai aprendo un rilievo — conoscenza nuova emersa, soluzione non ancora
> definita. Se sai gia' cosa fare e sei pronto ad agire, apri una revisione
> invece. Il rilievo registra conoscenza; la revisione esegue l'impatto.
> Confermi rilievo?

Se l'operatore corregge in revisione, procedi con `revisione`. Il tipo e'
immutabile dopo l'apertura.

### A2. Determina l'ID

Leggi il file per identificare tutti gli ID esistenti (formato `QUESTIONE-NNN`).
Assegna il prossimo ID disponibile. Ogni ID deve essere univoco.

### A3. Scrivi la questione

Inserisci la nuova questione in cima al file, dopo la sezione Indice:

```markdown
## QUESTIONE-{ID} — {Titolo}

**Tipo**: {rilievo | revisione | anomalia}
**Stato**: open

**Storia**
- {YYYY-MM-DD} open — {motivazione apertura, una riga}

**Descrizione**

{descrizione del problema, rilievo, revisione o anomalia}

**Domande aperte**
- [ ] {prima domanda, se presente}

**Impatto**
- {artefatto o fase} — {descrizione dell'impatto}

---
```

### A4. Aggiorna l'indice

Aggiungi una riga in cima alla tabella dell'indice:

```markdown
| QUESTIONE-{ID} | {Titolo} | open |
```

Aggiorna la nota:

```
> Ultima questione inserita: QUESTIONE-{ID} — {YYYY-MM-DD}.
```

---

## Operazione B — Aggiornamento stato

### B1. Identifica la questione

Se il messaggio specifica un ID, individua la questione direttamente.
Altrimenti mostra la lista tramite AskUserQuestion e chiedi quale aggiornare.

### B2. Determina il nuovo stato

Stati validi:

| Stato | Quando usarlo |
|---|---|
| `in-progress` | analisi avviata o ripresa dopo blocco |
| `pending-approval` | proposta redatta, in attesa di approvazione umana |
| `pending-rfc` | RFC inviata a Team-B, in attesa di risposta |
| `in-verification` | risposta RFC ricevuta, verifica in corso |
| `deferred` | rimandato con motivazione esplicita |
| `closed` | risolto — avvia il ramo di chiusura (Operazione D) |

Se il nuovo stato e' `closed`, passa a Operazione D.

### B3. Richiedi la motivazione

Ogni cambio di stato richiede una nota che risponde al "perche'".
Se non presente nel contesto, chiedila prima di procedere.

### B4. Aggiorna il file

Modifica il campo **Stato** della questione e aggiungi una riga in fondo alla
sezione **Storia**:

```markdown
- {YYYY-MM-DD} {nuovo-stato} — {motivazione}
```

Aggiorna la riga corrispondente nell'indice con il nuovo stato.

---

## Operazione C — Commento

### C1. Identifica la questione

Se il messaggio specifica un ID, individua la questione direttamente.

### C2. Determina il numero del commento

Leggi i commenti esistenti nella questione (formato `COMMENTO-NNN`).
Assegna il prossimo numero disponibile, locale alla questione.

### C3. Aggiungi il commento

Inserisci in fondo alla sezione **Commenti** della questione (creala se assente):

```markdown
**Commenti**

COMMENTO-{NNN} — {YYYY-MM-DD}
{testo del commento}
```

Il commento e' immutabile dopo la scrittura: additivo, non modificabile.

---

## Operazione D — Chiusura

### D1. Identifica la questione

Se il messaggio specifica un ID, individua la questione direttamente.
Cerca anche `mastro.md`. Se non esiste, interrompi e avvisa l'utente.

### D2. Verifica precondizione chiusura rilievo

Se la questione e' di tipo **rilievo** e il campo `Impatto` e' non vuoto:

- Verifica che il campo `Questioni collegate` esista e contenga almeno un
  riferimento a una questione di tipo *revisione* in stato aperto.
- Se la precondizione non e' soddisfatta, **interrompi** e avvisa l'utente:
  > Impossibile chiudere: rilievo con impatto non vuoto richiede almeno una
  > questione di revisione collegata aperta. Aggiungere il campo
  > `Questioni collegate` con il riferimento alla revisione prima di procedere.

Se la questione ha domande ancora aperte, avvisa l'utente prima di procedere.

### D3. Raccogli le informazioni per il mastro

Se non presenti nel contesto, chiedi:

- **Decisioni prese**: cosa e' stato risolto e perche' (una o piu' voci)
- **Impatto**: quali artefatti sono stati modificati o lo saranno

Poi valuta il Percorso: se il ciclo ha avuto complessita' (stati multipli,
ripensamenti, alternative), proponi una sintesi del percorso per approvazione.
Se la storia della questione e' nel contesto, puoi redigerla direttamente.

Il bias corretto e' includere il Percorso: l'omissione e' giustificata solo
quando la decisione e' stata diretta (apertura e chiusura senza stati intermedi).
Se il materiale e' molto esteso (allegati, commenti lunghi), proponi una sintesi
e chiedi conferma prima di scrivere.

### D4. Scrivi l'entry in mastro.md

Inserisci in cima al file (prepend):

```markdown
## {YYYY-MM-DD} — Chiusura {QUESTIONE-ID}: {Titolo}

**Questione**: {QUESTIONE-ID} — {Titolo}

**Percorso** (opzionale — ometti se la decisione e' stata diretta)

{sintesi del percorso: aperta per X, bloccata per Y, reindirizzata per Z}

**Decisioni prese**

- {decisione con motivazione}

**Impatto**

- `{artefatto}` — {descrizione della modifica applicata}

---
```

### D5. Rimuovi la questione da questioni.md

- Rimuovi l'intero blocco (dal titolo `## QUESTIONE-{ID}` fino al `---` finale)
- Rimuovi la riga corrispondente dalla tabella dell'indice
- Aggiorna la nota:

```
> Ultima questione chiusa: QUESTIONE-{ID} — {YYYY-MM-DD}.
```

### D6. Elimina il file RFC se presente

Cerca in `rfc/` un file il cui nome contiene l'ID della questione appena chiusa.
Se trovato:
- Verifica che la questione contenga un commento con la sintesi RFC (step B6
  di hodos-rfc). Se assente, avvisa l'utente prima di procedere.
- Elimina il file con `git rm`.

### D7. Valuta se suggerire /compact

1. Raccogli tutti gli ID citati nei campi `Questioni collegate` delle questioni
   ancora presenti nel file (non chiuse).
2. Per ciascun ID citato, verifica se e' ancora presente in `questioni.md`.
3. Se almeno un ID citato NON e' presente (quindi e' chiuso): non suggerire.
4. Se tutti gli ID citati sono ancora presenti, oppure nessuna questione aperta
   ha `Questioni collegate`: aggiungi questa nota al termine della risposta:

> Il contesto di questa chiusura e' completamente persistito nei file.
> Se la sessione e' lunga, questo e' un buon momento per /compact.

---

## Regole

- Non modificare mai il corpo della questione (Descrizione, Domande aperte,
  Impatto): usa un commento (Operazione C) per rettifiche o integrazioni
- La motivazione e' obbligatoria per qualsiasi cambio di stato
- Nel ramo chiusura: scrivi l'entry nel mastro prima di rimuovere la questione
- L'entry nel mastro e' immutabile dopo la scrittura: non modificarla mai
- Non comprimere le entry del mastro: il bias corretto e' includere il Percorso
  ogni volta che il ciclo ha avuto qualsiasi complessita'. L'omissione e'
  giustificata solo quando la decisione e' stata diretta (nessuno stato
  intermedio significativo). In caso di dubbio, includere.
- Se la questione e' di tipo rilievo: non puo' modificare artefatti nel corso
  del suo ciclo. Se durante l'analisi emerge una soluzione pronta ad essere
  eseguita, aprire una revisione prima di agire. Segnalare questa regola se
  l'operatore intende agire su un artefatto nel contesto di un rilievo aperto.
- Una questione aperta non contiene mai la soluzione, solo il problema
- La motivazione nella Storia deve rispondere al "perche'" non al "cosa"
