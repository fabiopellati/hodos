---
skill: rfc
client: Claude Code CLI
invocazione: /hodos-rfc
tipo: operativo
locale: it_IT
---

Gestisci il ciclo RFC: generazione outbound, acquisizione risposta, ricezione inbound.
L'operazione deve essere dichiarata esplicitamente nel messaggio.

## 1. Determina l'operazione

Leggi il messaggio dell'utente e identifica l'operazione richiesta:

- **generazione** — creare una nuova RFC da una questione in stato `pending-rfc`
- **acquisizione** — registrare la risposta ricevuta a una RFC outbound
- **inbound** — ricevere e processare una RFC inviata da un team esterno

Se l'operazione non e' chiara, chiedi tramite AskUserQuestion.

---

## Operazione A — Generazione outbound

### A1. Trova questioni.md

Cerca `questioni.md` nella directory corrente e nelle sottodirectory immediate.

### A2. Identifica la questione

Se il messaggio specifica un ID, individua la questione e verifica che sia in
stato `pending-rfc`. Altrimenti mostra tramite AskUserQuestion le questioni
in stato `pending-rfc` e chiedi quale usare.

### A3. Raccogli le informazioni mancanti

Leggi la questione per estrarre il contesto disponibile. Per le informazioni
non deducibili dalla questione, chiedi tramite AskUserQuestion:

- **Team-B**: nome e contatto del team destinatario
- **Sistema**: sistema o unita' su cui e' richiesto l'intervento
- **Criteri di accettazione**: come Team-A verifichera' il lavoro

### A4. Determina il percorso del file RFC

Il file RFC va nella stessa directory di questioni.md, in una sottodirectory `rfc/`.
Crea la directory se non esiste.

Nome file: `rfc-{progetto}-{YYYY-MM-DD}-{slug-titolo}.md`

Dove `{progetto}` e' l'identificatore kebab-case del progetto mittente
(es. `rfc-hodos-2026-03-11-template-ai-frontmatter.md`).
La questione di origine e' tracciata nel campo `**Questione di origine**` nell'header.

### A5. Scrivi il file RFC

```markdown
# RFC — {QUESTIONE-ID}

**Data**: {YYYY-MM-DD}
**Commit generazione**: {da compilare dopo il commit}
**Da**: Team-A / {nome progetto}
**A**: {Team-B}
**Questione di origine**: {QUESTIONE-ID} — {Titolo questione}
**Consegna RFC**: {opzionale — canale usato per consegnare questa RFC a Team-B, es. mail a <indirizzo>, copia in file:///path, sftp://host/path}
**Consegna risposta**: {opzionale — canale che Team-B deve usare per restituire la risposta, es. mail a <indirizzo>, copia in file:///path}

## Contesto

{Descrizione del progetto e del contesto. Autocontenuto: leggibile senza
conoscere la storia interna del progetto richiedente.}

## Richiesta

{Descrizione precisa di cosa viene richiesto.}

## Motivazione

{Perche' questa modifica e' necessaria. Quale problema risolve.}

## Criteri di Accettazione

{Come Team-A verifichera' che il lavoro soddisfi l'esigenza.}

---

## Response RFC

**Data risposta**:
**Stato**:
**Da**:
**A**:

### Decisione

### Lavoro svolto

### Deviazioni
```

### A6. Committa e registra il SHA

Dopo aver scritto il file, esegui il commit. Poi aggiorna il campo
`**Commit generazione**` nel file con il SHA del commit appena creato
e committa nuovamente con `--amend`.

### A7. Aggiorna la storia della questione

Aggiungi una nota nella storia della questione:
`{YYYY-MM-DD} — RFC generata e consegnata a {Team-B}, file: {nome-file}`

---

## Operazione B — Acquisizione risposta

### B1. Identifica il file RFC

Il file e' gia' stato copiato nella directory `rfc/` dall'utente.
Se il percorso e' specificato nel messaggio, usalo. Altrimenti cerca i file
RFC con campo `**Stato**:` vuoto nella sezione Response RFC.

### B2. Verifica integrita' della sezione di richiesta

Leggi il campo `**Commit generazione**` dal file. Se presente, esegui:

```
git diff {commit-sha} HEAD -- {percorso-file}
```

Verifica che nessuna riga modificata appartenga alla sezione di richiesta
(tutto cio' che precede `## Response RFC`). Se ci sono modifiche alla
sezione di richiesta, interrompi e avvisa l'utente.

Se il campo `**Commit generazione**` non e' presente, avvisa l'utente che
la verifica automatica non e' possibile e chiedi conferma prima di procedere.

### B3. Committa il file aggiornato

Esegui il commit del file RFC con la risposta acquisita.

### B4. Identifica la questione collegata

Cerca in questioni.md la questione con `**Stato**: pending-rfc` collegata
a questa RFC (tramite ID nel nome file o nel campo Questione di origine).

### B5. Aggiorna la storia della questione

Aggiungi una nota nella storia della questione senza cambiare lo stato
(la questione resta `pending-rfc` fino all'avvio effettivo del lavoro):

`{YYYY-MM-DD} — Risposta ricevuta da {Team-B}: {sintesi della decisione}`

Se la risposta contiene blocchi o una RFC inbound allegata, segnalarlo
esplicitamente nella nota.

### B6. Aggiungi la sintesi RFC come commento nella questione

Aggiungi un commento nella questione con la sintesi del ciclo RFC.
Il commento rende la questione autocontenuta: al momento della chiusura
il mastro ricevera' tutto il contesto rilevante senza dover leggere il file RFC.

```markdown
COMMENTO-NNN — {YYYY-MM-DD}
RFC {nome-file}

Richiesta: {sintesi di una o due righe della sezione Richiesta}
Risposta ({Team-B}): {sintesi della Decisione e del Lavoro svolto}
Deviazioni: {sintesi, ometti se assente}
```

---

## Operazione C — Ricezione inbound

### C1. Acquisisce il file RFC inbound

Il file e' gia' presente o viene fornito dall'utente. Copialo nella
directory `rfc/` se non e' gia' li'. Committalo.

### C2. Valuta la RFC prima di aprire questioni

Leggi la RFC per capire cosa viene richiesto e in quale fase del progetto
ricade il lavoro. La valutazione precede l'apertura di qualsiasi questione.

### C3. Apri le questioni necessarie

Per ciascuna decisione o lavoro richiesto dalla RFC, apri una questione
nella fase appropriata seguendo il normale ciclo Hodos.

### C4. Informa l'utente

Riepiloga le questioni aperte. Rammenta che al completamento del lavoro
e' obbligatorio eseguire il passo C5 prima di chiudere qualsiasi questione.

### C5. Compila e consegna la Response RFC (gate obbligatorio)

Questo passo deve essere completato prima di chiudere qualsiasi questione
aperta in C3. Eseguire in ordine:

1. Compila la sezione `## Response RFC` del file:
   - `**Data risposta**`, `**Stato**`, `**Da**`, `**A**`
   - `### Decisione` — cosa e' stato fatto o deciso
   - `### Lavoro svolto` — sintesi delle questioni risolte
   - `### Deviazioni` — eventuali scostamenti dalla richiesta (ometti se assente)

2. Esegui il commit del file RFC compilato.

3. Consegna il file al mittente (Team-A).

4. Aggiungi una nota nella storia di **ciascuna** questione aperta in C3:
   `{YYYY-MM-DD} — RFC restituita a {Team-A}, file: {nome-file}`

Solo dopo il completamento di tutti i punti precedenti e' possibile procedere
con la chiusura delle questioni aperte in C3.

---

## Regole

- La sezione di richiesta di una RFC e' immutabile dopo la generazione;
  i contributi successivi avvengono solo tramite Response RFC e commenti
- La RFC deve essere autocontenuta: Team-B non deve conoscere il progetto
  richiedente per capire cosa gli viene chiesto
- I Criteri di Accettazione descrivono il punto di vista di Team-A,
  non le istruzioni realizzative per Team-B
- La questione resta in `pending-rfc` fino all'avvio effettivo del lavoro
  da parte del team ricevente (semantica estesa: copre l'intero ciclo RFC)
- Le questioni aperte in C3 non possono essere chiuse prima che C5 sia
  completato: compilazione Response RFC, commit, consegna a Team-A, nota
  nella storia di ciascuna questione
