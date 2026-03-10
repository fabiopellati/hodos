---
skill: aggiorna-questione
client: Claude Code CLI
invocazione: /hodos-aggiorna-questione
tipo: operativo
locale: it_IT
---

Aggiorna lo stato di una questione esistente in questioni.md.
Quando lo stato di destinazione e' `closed`, esegue anche la chiusura completa:
verifica precondizioni, scrive l'entry nel mastro, rimuove la questione dal file.

## 1. Trova i file

Cerca `questioni.md` nella directory corrente e nelle sottodirectory immediate.
Se non esiste, interrompi e avvisa l'utente.

Se il nuovo stato sara' `closed`, cerca anche `mastro.md`. Se non esiste,
interrompi e avvisa l'utente.

## 2. Identifica la questione

Se il messaggio specifica un ID (es. QUESTIONE-003) o un titolo, individua la
questione direttamente.

Altrimenti, mostra la lista delle questioni presenti nell'indice tramite
AskUserQuestion e chiedi quale aggiornare.

## 3. Determina il nuovo stato

Stati validi:

| Stato | Quando usarlo |
|---|---|
| `in-progress` | analisi avviata o ripresa dopo blocco |
| `pending-approval` | proposta redatta, in attesa di approvazione umana |
| `pending-rfc` | RFC inviata a Team-B, in attesa di risposta |
| `in-verification` | risposta RFC ricevuta, verifica in corso |
| `deferred` | rimandato con motivazione esplicita |
| `closed` | risolto — avvia il ramo di chiusura completa |

Se il nuovo stato non e' chiaro dal contesto, chiedi tramite AskUserQuestion.

## 4. Richiedi la motivazione

Ogni cambio di stato richiede una nota che risponde al "perche'".
Se il messaggio non la contiene, chiedila prima di procedere.

---

## Ramo standard (stato != closed)

### 5a. Aggiorna il file

Modifica il campo **Stato** della questione e aggiungi una riga in fondo alla
sezione **Storia**:

```markdown
- {YYYY-MM-DD} {nuovo-stato} — {motivazione}
```

Aggiorna la riga corrispondente nell'indice con il nuovo stato.

---

## Ramo chiusura (stato == closed)

### 5b. Verifica precondizione chiusura rilievo

Se la questione e' di tipo **rilievo** e il campo `Impatto` e' non vuoto:

- Verifica che il campo `Questioni collegate` esista e contenga almeno un
  riferimento a una questione di tipo *revisione* in stato aperto (qualsiasi
  stato diverso da `closed`).
- Se la precondizione non e' soddisfatta, **interrompi** e avvisa l'utente:
  > Impossibile chiudere: rilievo con impatto non vuoto richiede almeno una
  > questione di revisione collegata aperta. Aggiungere il campo
  > `Questioni collegate` con il riferimento alla revisione prima di procedere.

Se la questione non e' di tipo rilievo, o l'impatto e' vuoto, procedi direttamente.

Se la questione ha domande ancora aperte, avvisa l'utente prima di procedere.

### 6b. Raccogli le informazioni per il mastro

Se non presenti nel contesto, chiedi:

- **Decisioni prese**: cosa e' stato risolto e perche' (una o piu' voci)
- **Impatto**: quali artefatti sono stati modificati o lo saranno

Poi chiedi esplicitamente:

> La questione ha avuto un percorso decisionale significativo — stati multipli,
> ripensamenti, alternative valutate o scartate? Se si', descrivilo in una o
> due righe. Se no, ometti.

Se il percorso e' presente nel contesto (storia della questione, commenti),
puoi proporlo tu sintetizzato per approvazione invece di chiederlo.

### 7b. Scrivi l'entry in mastro.md

Inserisci in cima al file (prepend) la nuova entry:

```markdown
## {YYYY-MM-DD} — Chiusura {QUESTIONE-ID}: {Titolo}

**Questione**: {QUESTIONE-ID} — {Titolo}

**Percorso** (opzionale — ometti se la decisione e' stata diretta)

{arco sintetico: aperta per X, bloccata per Y, reindirizzata per Z}

**Decisioni prese**

- {decisione con motivazione}

**Impatto**

- `{artefatto}` — {descrizione della modifica applicata}

---
```

### 8b. Rimuovi la questione da questioni.md

- Rimuovi l'intero blocco della questione (dal titolo `## QUESTIONE-{ID}` fino al `---` finale)
- Rimuovi la riga corrispondente dalla tabella dell'indice
- Aggiorna la nota:

```
> Ultima questione chiusa: QUESTIONE-{ID} — {YYYY-MM-DD}.
```

### 8c. Elimina il file RFC se presente

Cerca in `rfc/` un file il cui nome contiene l'ID della questione appena chiusa.
Se trovato:
- Verifica che la questione contenga un commento con la sintesi RFC (step B6 di hodos-rfc).
  Se il commento e' assente, avvisa l'utente prima di procedere.
- Elimina il file con `git rm`.

### 9b. Valuta se suggerire /compact

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

- Non modificare mai il corpo della questione (Descrizione, Domande aperte, Impatto) tramite questa skill: usa un commento (COMMENTO-NNN) per rettifiche o integrazioni
- La motivazione e' obbligatoria per qualsiasi cambio di stato
- Nel ramo chiusura: scrivi l'entry nel mastro prima di rimuovere la questione da questioni.md
- L'entry nel mastro e' immutabile dopo la scrittura: non modificarla mai
- Se la questione e' di tipo rilievo: il rilievo non puo' modificare artefatti nel corso del suo ciclo. Se durante l'analisi emerge una soluzione pronta ad essere eseguita, l'operatore deve aprire una revisione prima di agire. Segnalare questa regola se l'operatore intende agire su un artefatto nel contesto di un rilievo aperto.
